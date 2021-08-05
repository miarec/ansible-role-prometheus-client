# ansible-role-prometheus-client
Ansible role to install node_exporter client

Node_exporter is a client that collects real time data about the server it is installed on and reports that data to a Prometheus database

## Role Variables

### Version information:

    node_exporter_version: "1.2.0"
    node_exporter_download_url: "https://github.com/prometheus/node_exporter/releases/download/v{{ node_exporter_version }}/node_exporter-{{ node_exporter_version }}.linux-amd64.tar.gz"


node_exporter binary is manually installed, Choose the version of node_exporter to be installed and the URL to download from, more information can be found at https://prometheus.io/download/ for latest downloads

### OS prep

    node_exporter_user: node-exporter
    node_exporter_group: "{{ node_exporter_user }}"
    node_exporter_bin: /usr/local/bin/node_exporter
    node_exporter_dir_conf: /etc/node_exporter

These settings prep the user, owner and location of the node_exporter install

## Dependencies

None.

## Example Playbook

    ---
    - name: Install node_exporter
      hosts: all
      pre_tasks:
        - include_vars: vars/firewall.yml
          failed_when: false
      become: yes
      roles:
        - role: 'prometheus-client'
          tags: 'prometheus-client'

## Reloading / restarting

To restart the service

    sudo systemctl restart node_exporter