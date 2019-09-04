minikube start
minikube dashboard



# Build and Run
```bash
docker build -t hellonode .
```
---


# Create a repository
[Create Repository](https://cloud.docker.com/repository/create)

---
# push local image to repository
```sh
docker login

docker tag hellonode microshak/hellonode:v1
docker push microshak/hellonode:v1
```
---

# Deploy from repository
```bash
kubectl create deployment hellonode --image=microshak/hellonode:v1

kubectl expose deployment hellonode --type=LoadBalancer --port=8080

kubectl get services
```
# Update deployment
```sh

kubectl set image deployment.apps/hellonode  hellonode=microshak/hellonode:v2
```

#Start Service
```sh
minikube service hellonode
```
# Scale Up

```sh
kubectl scale deployment/hellonode --replicas=4
```

# Load Balencing

```
kubectl describe  deployment/hellonode

export NODE_PORT=$(kubectl get services/hellonode -o go-template='{{(index .spec.ports 0).nodePort}}')
echo NODE_PORT=$NODE_PORT


curl $(minikube ip):$NODE_PORT

```
#Scale Down
```
kubectl scale deployments/hellonode --replicas=2
kubectl get deployments
kubectl get pods -o wide
```


#Clean Up
```
kubectl delete service hellonode
kubectl delete deployment hellonode
```