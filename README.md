# Introduction
Des images docker pour faciliter le developpement local.

# Images 
- &check; AzureBusEmulator
- &check; ElasticSearch
- &check; Kafka
- &check; MongoDB
- &check; Nginx
- &check; Kong
- &check; PostgreSQL
- &check; RabbitMQ
- &check; Redis
- &check; SonarQube
- &check; SqlServer 2022
- &check; Smtp

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