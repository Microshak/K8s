# INStall helm
https://helm.sh/docs/using_helm/#installing-helm
sudo snap install helm --classic

# Apply the cluster
```
kubectl apply -f helm-rbac.yaml 
```
---
>>> Helm is unsucure be default

---
# Need to create a Cert using a CA
1. Create a CA
```
openssl genrsa -out ./ca.key.pem 4096
openssl req -key ca.key.pem -new -x509 -days 7300 -sha256 -out ca.cert.pem -extensions v3_ca

```
2. Generate a Tiller Key
```
 openssl genrsa -out ./tiller.key.pem 4096

```
3. Generates Helm Client Key
```

 openssl genrsa -out ./helm.key.pem 4096
```
5. Create Certs for Keys
```
openssl req -key tiller.key.pem -new -sha256 -out tiller.csr.pem
```
6. Helm Client cert -- repeat for every user
```
openssl req -key helm.key.pem -new -sha256 -out helm.csr.pem
```
7. Sign csr with CA - repeat for every user
```
openssl x509 -req -CA ca.cert.pem -CAkey ca.key.pem -CAcreateserial -in tiller.csr.pem -out tiller.cert.pem -days 365
```
8. Tille
```
openssl x509 -req -CA ca.cert.pem -CAkey ca.key.pem -CAcreateserial -in helm.csr.pem -out helm.cert.pem  -days 365

```
---
# We now have
```
# The CA. Make sure the key is kept secret.
ca.cert.pem
ca.key.pem
# The Helm client files
helm.cert.pem
helm.key.pem
# The Tiller server files.
tiller.cert.pem
tiller.key.pem

```

# Service Account for Helm
```
kubectl create -f ./namespace.yaml
kubectl create -f ./serviceaccount.yaml


```

# helm init
```
helm init  --tiller-tls --tiller-tls-cert ./tiller.cert.pem --tiller-tls-key ./tiller.key.pem --tiller-tls-verify --tls-ca-cert ca.cert.pem --tiller-namespace=helmns --service-account=helm-service-account
```

# helm ls
```
helm ls --tls --tls-ca-cert ca.cert.pem --tls-cert helm.cert.pem --tls-key helm.key.pem

```


https://helm.sh/docs/using_helm/#using-ssl-between-helm-and-tiller