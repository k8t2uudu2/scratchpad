# kubectl notes

Useful commands for debugging crashloops and restarts.

## Get pod restarts

```
kubectl get pods -A | grep -v Running
```

## Describe a specific pod

```
kubectl describe pod <pod> -n <namespace>
```

## Show previous container logs

```
kubectl logs <pod> -n <namespace> --previous
```

## Watch events

```
kubectl get events --sort-by=.lastTimestamp -n <namespace>
```
