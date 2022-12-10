FROM public.ecr.aws/docker/library/alpine:3.17 AS base

ARG TOOL=${TOOL:-blackbox_exporter}
ARG VERSION=${VERSION:-0.23.0}
ARG OS=${OS:-linux}
ARG ARCH=${ARCH:-amd64}

# Empty vars - only to be set when running behind proxy
ENV http_proxy=
ENV https_proxy=
ENV no_proxy=
# Empty vars - only to be set when running behind proxy

RUN apk update \
    && apk upgrade \
    && apk add --no-cache curl tar \
    && mkdir -p /etc/${TOOL} \
    && curl -L -o /tmp/${TOOL}.tar.gz \
    https://github.com/prometheus/${TOOL}/releases/download/v${VERSION}/${TOOL}-${VERSION}.${OS}-${ARCH}.tar.gz &> /dev/null \
    && cd /tmp \
    && tar -zxf /tmp/${TOOL}.tar.gz --strip-components=1 \
    && mv blackbox_exporter  /usr/local/bin/ \
    && rm -rf /tmp/ \
    && apk del tar \
    && rm -rf /var/cache/apk/*

ADD blackbox_exporter/blackbox_exporter.yml /etc/blackbox_exporter/

# Container Configurations
EXPOSE 9115
CMD ["/usr/local/bin/blackbox_exporter", "--config.file=/etc/blackbox_exporter/blackbox_exporter.yml", "--web.external-url=https://blackbox"]
