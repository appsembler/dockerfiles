FROM alpine:3.4
MAINTAINER Appsembler <ops@appsembler.com>

ENV VERSION 0.15.0
ENV OS linux
ENV ARCH amd64

WORKDIR /tmp/consul-template
RUN BASE_URL=https://releases.hashicorp.com/consul-template; \
    ARCHIVE=consul-template_${VERSION}_${OS}_${ARCH}.zip; \
    SHA256SUMS=consul-template_${VERSION}_SHA256SUMS; \
    SHA256SUMS_SIG=consul-template_${VERSION}_SHA256SUMS.sig; \
    apk update \
    && apk add bash ca-certificates gnupg wget \
    && update-ca-certificates \
    && wget $BASE_URL/${VERSION}/$ARCHIVE \
    && wget $BASE_URL/${VERSION}/$SHA256SUMS \
    && wget $BASE_URL/${VERSION}/$SHA256SUMS_SIG \
    && wget https://keybase.io/hashicorp/key.asc \
    && gpg --import key.asc \
    && gpg --verify $SHA256SUMS_SIG \
    && cat $SHA256SUMS | grep $ARCHIVE | grep $(sha256sum $ARCHIVE | cut -d' ' -f1) \
    && unzip $ARCHIVE -d /usr/local/bin/ \
    && rm -rf /tmp/consul-template/* \
    && rm -rf /var/cache/apk/*

VOLUME /etc/consul-template/conf.d/
VOLUME /etc/consul-template/templates/
VOLUME /etc/consul-template/rendered/

ENTRYPOINT ["/usr/local/bin/consul-template"]
