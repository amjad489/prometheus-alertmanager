# prometheus-alertmanager
## CPU Utilization alert
```yaml
- alert: CriticalCPUUtilisation
  expr: (100 - (avg by(instance) (irate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)) > 80
  for: 10m
  labels:
    threshold: page
  annotations:
    summary: "Instance *{{ $labels.instance }}* CPU Utilisation"
    description: 'High CPU utilisation detected for instance {{ $labels.instance}}, the utilisation is currently: {{ humanize $value }}%'
```
## Memory Utilization alert
```yaml
- alert: CriticalMemoryUtilisation
  expr: ((node_memory_MemTotal_bytes - node_memory_MemFree_bytes) / (node_memory_MemTotal_bytes)) * 100 > 90
  for: 10m
  labels:
    threshold: page
  annotations:
    summary: "Instance *{{ $labels.instance }}* memory utilisation"
    description: "*{{ $labels.instance }}* high memory usage, the utilisation is currently: {{ humanize $value }}%"
```
## Disk Utilization alert
```yaml
- alert: CriticalDISKUtilisation
  expr: (node_filesystem_size_bytes - node_filesystem_free_bytes) / node_filesystem_size_bytes  * 100 > 80
  for: 10m
  labels:
    threshold: page
  annotations:
    summary: "Instance *{{ $labels.instance }}* disk utilisation"
    description: 'High DISK utilisation detected for instance {{ $labels.instance}}, the utilisation is currently: {{ humanize $value }}%'
```
## Load Utilization alert

```yaml
- alert: CriticalLoadUtilisation
  expr: node_load1 > 2
  for: 10m
  labels:
    threshold: page
  annotations:
    summary: "Instance *{{ $labels.instance }}* load"
    description: "*{{ $labels.instance }}* is under high load, the utilisation is currently: {{ humanize $value }}"
```
