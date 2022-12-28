FROM public.ecr.aws/docker/library/alpine:3.17 AS base

ARG TOOL=${TOOL:-prometheus}
ARG VERSION=${VERSION:-2.36.2}
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
    && curl -sSL -o /tmp/${TOOL}.tar.gz \
    https://github.com/${TOOL}/${TOOL}/releases/download/v${VERSION}/${TOOL}-${VERSION}.${OS}-${ARCH}.tar.gz \
    && cd /tmp \
    && tar -zxf /tmp/${TOOL}.tar.gz --strip-components=1 \
    && rm /tmp/prometheus.yml /tmp/prometheus.tar.gz \
    && mv prom* /usr/local/bin/ \
    && mv console* /etc/prometheus/ \
    && rm -rf /tmp/ \
    && apk del tar \
    && rm -rf /var/cache/apk/*

COPY ${TOOL}/${TOOL}.yml /etc/${TOOL}/
COPY ${TOOL}/alerts /etc/${TOOL}/alerts

# Container Configurations
EXPOSE 9090
VOLUME [ "/var/lib/prometheus" ]
CMD ["/usr/local/bin/prometheus", "--config.file=/etc/prometheus/prometheus.yml", "--storage.tsdb.path=/var/lib/prometheus", "--web.console.libraries=/etc/prometheus/console_libraries", "--web.console.templates=/etc/prometheus/consoles", "--web.listen-address=0.0.0.0:9090", "--storage.tsdb.retention.time=30d", "--web.external-url=http://prometheus:9090/", "--storage.tsdb.no-lockfile"]
