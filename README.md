# Deploy a Xronos Grafana server

Provision a host with Grafana configured for Xronos dashboards.

This role performs the following steps:

- Deploys a Grafana docker image
- Deploys a grafana dashboard template to a remote host.

## Requirements

Provisioning host:

- Ansible 2.15

Remote host:

- Ubuntu 22.04 or 24.04
- docker

## Example playbook

```yaml
- hosts: grafana
  gather_facts: true
  roles:
    - name: xronos_grafana_ansible
      role: xronos_grafana_ansible
      vars:
        # set your influxdb URI here
        grafana_influxdb_url: "http://influxdb:8086"
        # set your influxdb token here
        grafana_influxdb_token: ""
        # set your grafana admin password here
        grafana_admin_password: ""
```

After running, the following services should be running:

- Grafana: `http://grafana:3000`

## Variables

- `deployment`: The name of this deployment. Used to prefix filesystem and docker resources so that more than once instance of this service may coexist on the same host. Defaults to `xronos`.
- `grafana_version`: The version of the grafana-enterprise image to install. Defaults to `latest`.
- `grafana_path`: The path to store grafana configuration. Defaults to `/opt/{{ deployment }}/grafana`.
- `grafana_docker_network`: The docker network for the grafana instance. Defaults to `{{ deployment }}`.
- `grafana_influxdb_url`: The URL of the InfluxDB instance to query. Defaults to `http://influxdb:8086`.
- `grafana_influxdb_token`: The API token for InfluxDB
- `grafana_admin_password`: The admin password for the Grafana web interface
