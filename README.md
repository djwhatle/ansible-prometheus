
prometheus playbook for RHUI support
============


### Optional variables: general settings


User-configurable defaults:

```yaml
# user and group
prometheus_user:   prometheus
prometheus_group:  prometheus


# directory for executable files
prometheus_install_path:   /opt/prometheus

# directory for configuration files
prometheus_config_path:    /etc/prometheus

# directory for logs
prometheus_log_path:       /var/log/prometheus

# directory for PID files
prometheus_pid_path:       /var/run/prometheus



# directory for temporary files
prometheus_download_path:  /tmp


# version of helper utility "gosu"
gosu_version:  "1.10"
```


User-installable rule files (see [doc](http://prometheus.io/docs/alerting/rules/) for details):


```yaml
# rule files to be installed to "{{ prometheus_rule_path }}" directory;
# dict fields:
#   - key: memo for this rule
#   - value:
#     - src:  file relative to `playbook_dir`
#     - dest: target file relative to `{{ prometheus_rule_path }}`
prometheus_rule_files
```


Alertmanager to be triggered:

```yaml
prometheus_alertmanager_url
```


Additional command-line arguments, if any (use `prometheus --help` to see the full list of arguments):

```yaml
prometheus_opts
```


### Optional variables: Node exporter

Additional command-line arguments, if any (use `node_exporter --help` to see the full list of arguments):

```yaml
prometheus_node_exporter_opts
```

# directory for runtime database (currently for `silences.json`)
prometheus_alertmanager_db_path: /var/lib/alertmanager
```

User-installable alertmanager conf file (see [doc](http://prometheus.io/docs/alerting/alertmanager/) for details):

```yaml
# main conf template relative to `playbook_dir`;
# to be installed to "{{ prometheus_config_path }}/alertmanager.yml"
prometheus_alertmanager_conf
```

Additional command-line arguments, if any (use `alertmanager --help` to see the full list of arguments):

```yaml
prometheus_alertmanager_opts
```

## Handlers

Prometheus server:

- `restart prometheus`

- `reload prometheus`

- `stop prometheus`


Node exporter:

- `restart node_exporter`

- `reload node_exporter` (actually, the same as `restart`)

- `stop node_exporter`


Alertmanager:

- `restart alertmanager`

- `reload alertmanager`

- `stop alertmanager`


### Browse the default Prometheus pages

Open the page in your browser:

- Prometheus - `http://HOST:9090` or `http://HOST:9090/consoles/node.html`

- Alertmanager - `http://HOST:9093`


## License

MIT License. See the [LICENSE file](LICENSE) for details.
