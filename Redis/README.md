```
kompose convert
```

```
kubectl apply -f redis-deployment.yaml
kubectl apply -f redis-service.yaml
kubectl apply -f redis-data-persistentvolumeclaim.yaml
```

```
kubectl port-forward svc/redis 6379:6379
```