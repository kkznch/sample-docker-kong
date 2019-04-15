FROM alpine:latest

# Kong
ENV KONG_VERSION 1.1.1
ENV KONG_SHA256 3f07c30c6902ec0dd17e9777f5f479076c65c634b677402072414ca9d31dc810
RUN adduser -Su 1337 kong \
    && mkdir -p "/usr/local/kong" \
    && apk add --no-cache --virtual .build-deps wget tar ca-certificates \
    && apk add --no-cache libgcc openssl pcre perl tzdata curl libcap su-exec \
    && wget -O kong.tar.gz "https://bintray.com/kong/kong-alpine-tar/download_file?file_path=kong-$KONG_VERSION.apk.tar.gz" \
    && echo "$KONG_SHA256 *kong.tar.gz" | sha256sum -c - \
    && tar -xzf kong.tar.gz -C /tmp \
    && rm -f kong.tar.gz \
    && cp -R /tmp/usr / \
    && rm -rf /tmp/usr \
    && cp -R /tmp/etc / \
    && rm -rf /tmp/etc \
    && apk del .build-deps

# Dockerize
ENV DOCKERIZE_VERSION v0.6.1
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && rm dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz

# Kong config file
COPY kong.conf /etc/kong/
