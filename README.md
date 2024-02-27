# Deploy a Xronos Grafana server

Provision a host with Grafana configured for Xronos dashboards.

This role performs the following steps:

- Deploys a Grafana docker image
- Deploys a grafana dashboard template to a remote host
- Deploys custom configuration and security tokens to the remote host

## Requirements

Provisioning host:

- Ansible 2.15

Remote host:

- Ubuntu 22.04 or later
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

- `deployment` (= `xronos` ): The name of this deployment. Used to prefix filesystem and docker resources so that more than once instance of this service may coexist on the same host.
- `grafana_path` (= `/opt/{{ deployment }}/grafana` ): The path to store grafana configuration.
- `grafana_docker_network` (= `{{ deployment }}`): The docker network for the grafana instance.
- `grafana_influxdb_url` (= `http://influxdb:8086`): The URL of the InfluxDB instance to query.
- `grafana_influxdb_token`: The API token for InfluxDB
- `grafana_admin_password`: The admin password for the Grafana web interface
