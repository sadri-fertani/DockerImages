```
helm repo add hashicorp https://helm.releases.hashicorp.com
helm repo update

kubectl create namespace vault
helm install vault hashicorp/vault --namespace vault --set "server.dev.enabled=true"
```

```
kubectl exec -n vault -it vault-0 -- /bin/sh
```

```
vault status
vault login (root)
```

# Important

## Avec persistance
```
helm install vault hashicorp/vault -n vault --create-namespace --set "server.dev.enabled=false" --set "server.dataStorage.enabled=true" --set "server.dataStorage.size=2Gi" --set "server.dataStorage.storageClass=vault-local"
```


## VSO
```
helm install vault-secrets-operator hashicorp/vault-secrets-operator --namespace vault-secrets-operator-system --create-namespace

```