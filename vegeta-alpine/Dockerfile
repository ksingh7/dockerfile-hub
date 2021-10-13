## This dockerfile uses alpine as base image and installs vegeta (https://github.com/tsenart/vegeta)
## The final image size is just 15.9MB

FROM alpine:3.14.1

ENV VEGETA_VERSION 12.8.4

LABEL \
    maintainer="Karan Singh <karan.singh731987@gmail.com>" \
    org.opencontainers.image.title="vegeta" \
    org.opencontainers.image.description="Docker image for the Vegeta HTTP load testing tool." \
    org.opencontainers.image.authors="Karan Singh <karan.singh731987@gmail.com>" \
    org.opencontainers.image.url="https://github.com/peter-evans/vegeta-docker" 

RUN set -ex \
    && apk add --no-cache ca-certificates jq \
    && apk add --no-cache --virtual .build-deps \
    openssl \
    && wget -q "https://github.com/tsenart/vegeta/releases/download/v${VEGETA_VERSION}/vegeta_${VEGETA_VERSION}_linux_amd64.tar.gz" -O /tmp/vegeta.tar.gz \
    && cd bin \
    && tar xzf /tmp/vegeta.tar.gz \
    && rm /tmp/vegeta.tar.gz \
    && apk del .build-deps

CMD [ "/bin/vegeta", "-help" ]