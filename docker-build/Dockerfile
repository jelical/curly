ARG SDK_VER="2.1.300"
FROM microsoft/dotnet:$SDK_VER-sdk-alpine
ARG DOCKER_CLI_VERSION="18.09.0"
ENV DOWNLOAD_URL="https://download.docker.com/linux/static/stable/x86_64/docker-$DOCKER_CLI_VERSION.tgz"

# install docker client
RUN apk --update add curl nodejs bash git \
    && mkdir -p /tmp/download \
    && curl -L $DOWNLOAD_URL | tar -xz -C /tmp/download \
    && mv /tmp/download/docker/docker /usr/local/bin/ \
    && rm -rf /tmp/download \
    && apk del curl \
    && rm -rf /var/cache/apk/*

COPY ./docker-entrypoint.sh /
RUN chmod 777 /docker-entrypoint.sh
ENV NUGET_HTTP_CACHE_PATH=/build-cache/cache
ENV NUGET_PACKAGES=/build-cache/packages
ENV YARN_CACHE_FOLDER=/build-cache/.yarn-cache
WORKDIR /work
ENTRYPOINT ["/docker-entrypoint.sh"]
#CMD dotnet msbuild /t:$TARGETS /p:$PROPS $PROJECT
