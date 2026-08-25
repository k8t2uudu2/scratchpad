# Kubernetes Debugging Checklist

Quick reference for common cluster issues.

## Pod stuck in Pending
- Check `kubectl describe pod <name>` for events.
- Verify resource requests vs. node allocatable.
- Look for taints/tolerations and node selectors.
- Ensure PersistentVolumeClaims are bound.

## CrashLoopBackOff
- Inspect logs: `kubectl logs <pod> --previous`.
- Check configmaps/secrets for recent changes.
- Validate liveness/readiness probe paths and timeouts.
- Test locally with the same image and args.

## Service not reachable
- Confirm selector matches pod labels.
- Check endpoints: `kubectl get endpoints <svc>`.
- For headless services, verify DNS and port names.
- Review NetworkPolicy rules in the namespace.

## Node NotReady
- SSH to node, check kubelet status: `systemctl status kubelet`.
- Inspect `journalctl -u kubelet -n 100`.
- Verify container runtime is healthy.
- Look at disk/memory pressure and eviction thresholds.

## Persistent volume issues
- Check PV status: `kubectl get pv`.
- Verify storage class and reclaim policy.
- Confirm accessModes match workload usage.
- Test NFS/Ceph connectivity from the node.

## Useful one-liners

```bash
# Show unhealthy pods
kubectl get pods -A -o wide | grep -Ev 'Running|Completed'

# Top resource consumers in a namespace
kubectl top pods -n <namespace> --sort-by=cpu

# Recent events sorted by time
kubectl get events -A --sort-by=.lastTimestamp
```

Remember to check the obvious first: image tags, namespaces, and typos in selectors.