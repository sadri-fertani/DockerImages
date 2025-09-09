```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update

kubectl create namespace kafka

helm install my-kafka bitnami/kafka --namespace kafka --set replicaCount=1 --set auth.enabled=false --set zookeeper.replicaCount=1 --set zookeeper.auth.enabled=false
```

``` powershell
$secret = kubectl get secret kafka-user-passwords --namespace kafka -o jsonpath="{.data.client-passwords}"
PS C:\Dev\DockerImages> $decoded = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($secret))
PS C:\Dev\DockerImages> $firstPassword = $decoded.Split(",")[0]
PS C:\Dev\DockerImages> $firstPassword
```

