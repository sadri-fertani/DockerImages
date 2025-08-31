# Introduction
Des images docker pour faciliter le developpement local.

# Images 
- &check; AzureBusEmulator
- &check; Camunda
- &check; ElasticSearch
- &check; Kafka
- &check; Kong
- &check; MongoDB
- &check; Nginx
- &check; PostgreSQL
- &check; RabbitMQ
- &check; Redis
- &check; Smtp
- &check; SonarQube
- &check; SqlServer 2022
- &check; Vault-HashiCorp

# Chargement
Pour charger une image, il faut se positionner dans le repertoire cible puis executer cette commande :
```
docker compose up -d
```

# Fix error 
## SourceTree
```
git config --global --add safe.directory "{FolderFullPath}"
```