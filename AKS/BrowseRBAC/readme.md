az login

az aks get-credentials --resource-group K8s --name MicroKube                                                                  

kubectl create clusterrolebinding kubernetes-dashboard -n kube-system --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard


az aks browse --resource-group K8s --name MicroKube  

