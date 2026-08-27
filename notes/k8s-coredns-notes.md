# CoreDNS Debugging Notes

Quick reference for local cluster DNS issues.

## Common checks

- Check CoreDNS pods are running: `kubectl -n kube-system get pods -l k8s-app=kube-dns`
- View logs: `kubectl -n kube-system logs -l k8s-app=kube-dns --tail=50`
- Test DNS from a pod: `kubectl run -it --rm dns-test --image=busybox -- nslookup kubernetes.default.svc.cluster.local`

## Things that bite

- NodeLocal DNSCache can mask upstream issues; check `nodelocaldns` logs too.
- If cluster uses a custom search domain, verify `/etc/resolv.conf` inside pods.
- CoreDNS config lives in the `coredns` ConfigMap in `kube-system`.
