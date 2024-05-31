AAP-AC-OBSERVABILITY
=========

This Ansible role sets up observability for Ansible Automation Platform by deploying Prometheus, Grafana, and Node Exporter using Podman containers. It ensures Prometheus is configured to scrape metrics from the Automation Controller and Node Exporter, and imports a pre-configured Grafana dashboard.

Requirements
------------

- Ansible 2.9+
- Podman installed on the target hosts
- Firewalld installed and running on the target hosts
- Collection containers.podman

Role Variables
--------------

These are the default variables defined in `defaults/main.yml`:

```yaml
prometheus_image: "docker.io/prom/prometheus:latest"
grafana_image: "docker.io/grafana/grafana:latest"
prometheus_container_name: "prometheus"
grafana_container_name: "grafana"
prometheus_config_dir: "/opt/prometheus"
grafana_data_dir: "/opt/grafana"
node_exporter_version: "1.8.1"
node_exporter_user: "node_exporter"
node_exporter_group: "node_exporter"
node_exporter_config_dir: "/opt/node_exporter"
controller_host: "your_controller_host" #change
bearer_token: "your_bearer_token" #change
grafana_admin_user: "admin" 
grafana_admin_password: "admin" #change
grafana_url: "http://localhost:3000" #change
dashboard_file: "files/dashboard.json"
```

### Variables Description

- `prometheus_image`: Docker image for Prometheus.
- `grafana_image`: Docker image for Grafana.
- `prometheus_container_name`: Name of the Prometheus container.
- `grafana_container_name`: Name of the Grafana container.
- `prometheus_config_dir`: Directory to store Prometheus configuration files.
- `grafana_data_dir`: Directory to store Grafana data.
- `node_exporter_version`: Version of Node Exporter to install.
- `node_exporter_user`: User to run Node Exporter.
- `node_exporter_group`: Group to run Node Exporter.
- `node_exporter_config_dir`: Directory to store Node Exporter configuration files.
- `controller_host`: Hostname or IP address of the Automation Controller.
- `bearer_token`: Bearer token for accessing the Automation Controller metrics.
- `grafana_admin_user`: Admin username for Grafana.
- `grafana_admin_password`: Admin password for Grafana.
- `grafana_url`: URL of the Grafana instance.
- `dashboard_file`: Path to the JSON file containing the Grafana dashboard configuration.

Dependencies
------------

- Collection containers.podman

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- name: Setup Observability with Prometheus, Grafana, and Node Exporter
  hosts: all
  become: true
  roles:
    - role: setup_observability
      prometheus_image: "prom/prometheus:v2.26.0"
      grafana_image: "grafana/grafana:7.5.3"
      grafana_admin_user: "admin"
      grafana_admin_password: "supersecret"
      controller_host: "controller.example.com"
      bearer_token: "your_generated_token"
```

License
-------

MIT

Author Information
------------------

This role was created by Allan Roque. For any issues, please contact allanrafaelroque@gmail.com.
