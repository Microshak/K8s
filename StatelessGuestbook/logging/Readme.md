https://kubernetes.io/docs/tutorials/stateless-application/guestbook-logs-metrics-with-elk/

# Add a Cluster role binding
kubectl create clusterrolebinding cluster-admin-binding \
 --clusterrole=cluster-admin --user=v-roshmi@microsoft.com


---
# Install kube-state-metrics
## Check to see if kube-state-metrics is running
```
kubectl get pods --namespace=kube-system | grep kube-state
```

## install
```
git clone https://github.com/kubernetes/kube-state-metrics.git kube-state-metrics
kubectl create -f kube-state-metrics/kubernetes
kubectl get pods --namespace=kube-system | grep kube-state
```

## Verify
```
kubectl get pods -n kube-system -l k8s-app=kube-state-metrics
```

---
# Clone example

```
git clone https://github.com/elastic/examples.git
cd examples/beats-k8s-send-anywhere
```
---
