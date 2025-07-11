# Commandes Docker 


#### Commandes générales
```zsh
docker version         # Affiche la version client/serveur Docker.
docker info            # Infos sur le démon Docker en cours (conteneurs, images, etc.).
docker help            # ide globale ou docker <commande> --help pour une commande spécifique.
```

#### Execution et logs
```zsh
docker exec -it <nom> bash                 # Ouvrir un shell dans un conteneur en cours
docker logs <nom>                          # Voir les logs d’un conteneur
docker inspect <nom>                       # Voir les détails techniques d’un conteneur
```

#### Volumes
```zsh
docker volume ls                           # Lister les volumes
docker volume create <nom>                 # Créer un volume
docker volume rm <nom>                     # Supprimer un volume
```

#### Réseaux
```zsh
docker network ls                          # Lister les réseaux
docker network create <nom>                # Créer un réseau
```

#### Nettoyage
```zsh
docker system prune                        # Supprimer les ressources inutilisées (⚠️)
docker volume prune                        # Supprimer les volumes non utilisés
docker image prune                         # Supprimer les images inutilisées
```
#### Docker compose
```zsh
docker compose up                         # Lancer les services définis dans docker-compose.yml
docker compose up -d                      # Lancer en arrière-plan
docker compose down                       # Stopper et supprimer les services
docker compose ps                         # Lister les services en cours
docker compose logs -f                    # Suivre les logs en temps réel
docker compose exec <service> bash        # Entrer dans un conteneur d’un service
```

#### Images docker
```zsh
docker pull <image>    # Télécharger une image depuis Docker Hub.
docker images          # Liste les images locales.
docker rmi <image>     # Supprimer une image.
docker build -t <nom>:<tag> .  # Construire une image depuis un Dockerfile.
```

#### container docker
```zsh
docker run <image>                          # Lancer un conteneur simple (en mode foreground).
docker run -it <image> bash                 # Lancer un conteneur interactif avec un shell.
docker run -d --name <nom> <image>          # Lancer un conteneur en arrière-plan.
docker ps                                   # Liste les conteneurs en cours d’exécution.
docker ps -a                                # Liste tous les conteneurs (même arrêtés).
docker stop <id|nom>                        # Arrêter un conteneur
docker start <id|nom>                       # Démarrer un conteneur
docker restart <id|nom>                     # Redémarrer un conteneur
docker rm <id|nom>                          # Supprimer un conteneur
```

#### Créer une base PostgreSQL avec docker run
```zsh
  docker run -d \
  --name postgres-container \
  -e POSTGRES_DB=ma_base \
  -e POSTGRES_USER=mon_user \
  -e POSTGRES_PASSWORD=mon_mot_de_passe \
  -p 5432:5432 \
  -v pgdata:/var/lib/postgresql/data \
  postgres:16
```

```zsh
-d                                  # Détache le conteneur (mode arrière-plan)
--name postgres-container           # Nom du conteneur
-e POSTGRES_DB=ma_base              # Nom de la base à créer automatiquement
-e POSTGRES_USER=mon_user           # Nom de l’utilisateur
-e POSTGRES_PASSWORD=...            # Mot de passe de l’utilisateur
-p 5432:5432                        # Expose le port local 5432 vers le conteneur
-v pgdata:/var/lib/postgresql/data  # Volume persistant nommé pgdata
postgres:16                         # Image utilisée (PostgreSQL version 16)
```

https://docs.docker.com/reference/cli/docker/
