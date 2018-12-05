# Ansible Role: prometheus-memcached-exporter

An Ansible role that installs Prometheus memcached Exporter on Ubuntu|Debian|Redhat-based machines with systemd|Upstart|sysvinit.

## Requirements

All needed packages will be installed with this role.

## Role Variables

| Variable                                    | Type   | Choices                                                                            | Default                                                                                                                     | Comment                                                                                                                    |
|---------------------------------------------|--------|------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| prometheus_memcached_exporter_version            | string | See [memcached_exporter](https://github.com/prometheus/memcached_exporter/releases) releases | 0.15.1                                                                                                                      | Version of memcached_exporter that will be installed. Minimal supported version: 0.15                                           |
| prometheus_memcached_exporter_release_name       | string |                                                                                    | memcached_exporter-{{ prometheus_memcached_exporter_version }}.linux-amd64                                                            | Name of the binary that will be downloaed from the   [release](https://github.com/prometheus/memcached_exporter/releases)  page |
| prometheus_memcached_exporter_enabled_collectors | list   | [List of flags](https://github.com/prometheus/memcached_exporter)                       | conntrack, diskstats, entropy, filefd, filesystem, loadavg,   mdadm, meminfo, netdev, netstat, stat, textfile, time, vmstat | List of enabled collector                                                                                                  |
| prometheus_memcached_exporter_config_flags       | dict   |                                                                                    |                                                                                                                             | Dict of key, value options to add to the start command line                                                                |
| prometheus_memcached_exporter_url                | string |                                                                                    | not defined                                                                                                                      | Custom URL to download memcached_exporter if you can't access to github                                       |


## Dependencies

- UnderGreen.prometheus-exporters-common

## Example Playbook

```yaml
- hosts: memcached-exporters
  roles:
    - role: UnderGreen.prometheus-memcached-exporter
      prometheus_memcached_exporter_version: 0.15.1
      prometheus_memcached_exporter_enabled_collectors:
        - conntrack
        - cpu
        - diskstats
        - entropy
        - filefd
        - filesystem
        - loadavg
        - mdadm
        - meminfo
        - netdev
        - netstat
        - stat
        - textfile
        - time
        - vmstat
      prometheus_memcached_exporter_config_flags:
        'web.listen-address': '0.0.0.0:9100'
        'log.level': 'info'
```

## License

GPLv2
Based on UnderGreen's ansible-prometheus-memcached-exporter role (https://github.com/UnderGreen/ansible-prometheus-memcached-exporter)