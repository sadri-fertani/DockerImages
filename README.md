# Introduction
Des images docker pour faciliter le developpement local.

# Images 
- &check; AzureBusEmulator
- &#x2610; ElasticSearch
- &check; Kafka
- &check; MongoDB
- &check; Nginx
- &check; PostgreSQL
- &check; RabbitMQ
- &check; Redis
- &#x2610; SonarQube
- &#x2610; SqlServer2017

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