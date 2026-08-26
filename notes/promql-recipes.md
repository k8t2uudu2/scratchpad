# PromQL Recipes

Useful queries for Kubernetes troubleshooting.

## CPU throttling
```
sum by (pod) (rate(container_cpu_cfs_throttled_periods_total{namespace="prod"}[5m]))
/
sum by (pod) (rate(container_cpu_cfs_periods_total{namespace="prod"}[5m]))
```

## Memory working set
```
sum by (pod) (
  container_memory_working_set_bytes{namespace="prod", container!="POD"}
)
```

## OOM Killed Restarts
```
increase(kube_pod_container_status_restarts_total{namespace="prod"}[1h]) > 0
```
