# K8s Debug Cheatsheet

Quick reference for common issues.

- Pod stuck in `Pending`: check `kubectl describe pod <name>` for resource limits or node selectors.
- CrashLoopBackOff: `kubectl logs <pod> --previous` to see the last attempt.
- Node NotReady: `kubectl get nodes -o wide` and check kubelet status on the node.
- Service not resolving: `kubectl get endpoints <svc>` — if empty, check selectors.
- PersistentVolume not binding: `kubectl get pv pvc -o yaml` and verify storage class.

_Add more as we hit them._