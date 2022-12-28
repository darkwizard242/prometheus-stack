# prometheus-stack

Demo repository containing containerized stack based on Prometheus, Grafana, AlertManager and Blackbox Exporter.

It code for containerizing the components to local development/testing.

## 1\. Provisioning

This section contains steps on how to utilize the containers locally.

**Note:** _It is assumed that you have git, docker and docker-compose installed_.

- Checkout the repository:

```shell
git clone https://github.com/darkwizard242/prometheus-stack.git
```

- Change to repository directory:

```shell
cd prometheus-stack
```

- Building container images (preferably without cache):

```shell
docker-compose build --no-cache
```

- Running stack (detached mode):

```shell
docker-compose up -d
```

### URL(s):

Default URL's to access apps on browsers unless you have modified anything would be the following:

Application       | URL                     | Username/Password
----------------- | ----------------------- | -----------------
Alert Manager     | <http://localhost:9093> | Does not apply.
BlackBox Exporter | <http://localhost:9115> | Does not apply.
Prometheus        | <http://localhost:9090> | Does not apply.
Grafana           | <https://localhost>     | admin/admin

## 2\. Configuration Files:

Application       | Relative Path                                 | Comment
----------------- | --------------------------------------------- | --------------------------------------------------------------------
Alert Manager     | **./alertmanager/alertmanager.yml**           |
BlackBox Exporter | **./blackbox_exporter/blackbox_exporter.yml** |
Prometheus        | **./prometheus/prometheus.yml**               |
Grafana           | _None_                                        | Environment variables in `docker-compose` used are used to override)

Relative path from repository - for configuration files of monitoring stack apps.
