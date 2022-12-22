FROM public.ecr.aws/docker/library/alpine:3.17 AS base

ARG TOOL=${TOOL:-alertmanager}
ARG VERSION=${VERSION:-0.24.0}
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
    https://github.com/prometheus/${TOOL}/releases/download/v${VERSION}/${TOOL}-${VERSION}.${OS}-${ARCH}.tar.gz \
    && cd /tmp \
    && tar -zxf /tmp/${TOOL}.tar.gz --strip-components=1 \
    && mv ${TOOL}  /usr/local/bin/ \
    && rm -rf /tmp/ \
    && apk del tar \
    && rm -rf /var/cache/apk/*

COPY ${TOOL}/${TOOL}.yml /etc/${TOOL}/

# Container Configurations
EXPOSE 9093
CMD ["/usr/local/bin/alertmanager", "--config.file=/etc/alertmanager/alertmanager.yml", "--storage.path=/var/lib/alertmanager", "--web.external-url=http://alertmanager"]
