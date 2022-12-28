FROM grafana/grafana:9.0.1
LABEL maintainer="amuhammad@ctacorp.com"
USER root

RUN apk update \
    && apk upgrade \
    && apk add --no-cache curl \
    && chown -R grafana:  /var/lib/grafana

COPY grafana/config/provisioning /var/lib/grafana/provisioning
COPY grafana/config/dashboards /var/lib/grafana/dashboards

EXPOSE 3000
VOLUME [ "/var/lib/grafana" ]
