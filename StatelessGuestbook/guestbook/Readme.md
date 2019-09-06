
# Create Master
```sh
kubectl apply -f guestbook/redis-master-deployment.yaml


kubectl get pods
kubectl logs -f POD-NAME #from step 2

kubectl apply -f guestbook/redis-master-service.yaml

kubectl get service
```

# Start Slaves
```
kubectl apply -f guestbook/redis-slave-deployment.yaml
  kubectl get pods

kubectl apply -f guestbook/redis-slave-service.yaml
kubectl get services
```

# Deploy Frount end
```sh
kubectl apply -f guestbook/frontend-deployment.yaml
kubectl get pods -l app=guestbook -l tier=frontend

kubectl apply -f guestbook/frontend-service.yaml
kubectl get services
```


# View the service
```sh
kubectl service frontend --url
```

# see load balancer
```
kubectl get service frontend

```
#scale up
```sh
kubectl scale deployment frontend --replicas=5

kubectl get pods
```


# delete

```bash
kubectl delete deployment -l app=redis
kubectl delete service -l app=redis
kubectl delete deployment -l app=guestbook
kubectl delete service -l app=guestbook
```


