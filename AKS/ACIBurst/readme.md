# Create ACI Deployment
```
kubectl apply -f ACIDeployment.yaml


kubectl get pods -o wide
```
---

# Test Virtual Node Pod
```
kubectl run -it --rm virtual-node-test --image=debian
```


