---

# Ansible Roles for Monitoring and Logging Stack

This repository contains a set of Ansible roles for deploying and configuring a monitoring and logging stack outside of Kubernetes. The stack includes Prometheus, Node Exporter, ElasticSearch, Kibana, and Fluentbit. Each component is installed and configured with best practices, ensuring idempotency and ease of customization.

## Overview

The repository contains four Ansible roles:

1. **Prometheus**: Installs and configures Prometheus to monitor external hosts.
2. **Node Exporter**: Installs Node Exporter for system metrics collection and integrates it with Prometheus.
3. **ElasticSearch & Kibana**: Installs ElasticSearch for log storage and Kibana for log visualization.
4. **Fluentbit**: Installs Fluentbit to collect system logs (from journald) and sends them to ElasticSearch.

## Project Structure

```
ansible-roles-monitoring/
├── playbooks/
│   ├── prometheus.yml
│   ├── node_exporter.yml
│   ├── elasticsearch_kibana.yml
│   └── fluentbit.yml
├── roles/
│   ├── prometheus/
│   ├── node_exporter/
│   ├── elasticsearch_kibana/
│   └── fluentbit/
└── inventory/
    └── hosts.ini
```

- **playbooks/**: Contains playbooks for deploying each component.
- **roles/**: Contains individual Ansible roles for Prometheus, Node Exporter, ElasticSearch, Kibana, and Fluentbit.
- **inventory/**: Hosts file for defining servers to which roles will be applied.

## Requirements

- Ansible 2.9 or later.
- Root or sudo access to the target hosts.

## Usage

### 1. Clone the repository

```bash
git clone https://github.com/yourusername/ansible-roles-monitoring.git
cd ansible-roles-monitoring
```

### 2. Update Inventory

Edit `inventory/hosts.ini` to define your hosts:

```ini
[prometheus_server]
your_prometheus_host

[elk_server]
your_elasticsearch_host

[all]
your_fluentbit_and_node_exporter_hosts
```

### 3. Run the Playbooks

Run each playbook in the correct order. For example:

1. Install Prometheus:

```bash
ansible-playbook -i inventory/hosts.ini playbooks/prometheus.yml
```

2. Install Node Exporter:

```bash
ansible-playbook -i inventory/hosts.ini playbooks/node_exporter.yml
```

3. Install ElasticSearch and Kibana:

```bash
ansible-playbook -i inventory/hosts.ini playbooks/elasticsearch_kibana.yml
```

4. Install Fluentbit:

```bash
ansible-playbook -i inventory/hosts.ini playbooks/fluentbit.yml
```

### 4. Access Web Interfaces

- **Prometheus**: `http://your_prometheus_host:9090`
- **Kibana**: `http://your_elasticsearch_host:5601`

## Customization

Each role has its own set of defaults that can be customized in the `defaults/main.yml` files within the respective roles. These settings include version numbers, installation directories, and service configurations.

For example, to change the Prometheus web listen address, update the following variable in `roles/prometheus/defaults/main.yml`:

```yaml
prometheus_web_listen_address: '0.0.0.0:9090'
```

## Best Practices

- The roles are designed to be idempotent, meaning you can run them multiple times without making unnecessary changes.
- Handlers are used to reload or restart services when configuration changes are detected.
- The roles are modular and can be reused in other projects by copying the relevant role folders.



## Authors

- Alexey Yashin - (https://github.com/alexey-yashin)

---
