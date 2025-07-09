# Commandes Docker 


#### Commandes générales

```zsh
docker version         # Affiche la version client/serveur Docker.
docker info            # Infos sur le démon Docker en cours (conteneurs, images, etc.).
docker help            # ide globale ou docker <commande> --help pour une commande spécifique.
```



```zsh
docker compose up      # Lancer
```
```zsh
docker compose down    # Arrêter et supprimer
```
```zsh
docker compose ps      # Voir les conteneurs actifs
```

#### Images docker

```zsh
docker pull <image>    # Télécharger une image depuis Docker Hub.
docker images          # Liste les images locales.
docker rmi <image>     # Supprimer une image.
docker build -t <nom>:<tag> .  # Construire une image depuis un Dockerfile.
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



#### Se connecter à PostgreSQL dans un conteneur
```zsh
docker exec -it postgres-container psql -U mon_user -d ma_base
```

Aide psql

# Une fois connecté :
```zsh
	•	Lister les bases : \l
	•	Lister les tables : \dt
	•	Afficher les colonnes : \d nom_table
	•	Quitter : \q
```

https://docs.docker.com/reference/cli/docker/
```zsh
docker start <nom_du_container>  // relancer un container
docker stop <nom_du_container>  // stopper un container
```

# Docker compose exemple 
```yaml
version: "3.9"

services:
  db:
    image: postgres:16
    container_name: postgres-db
    restart: unless-stopped
    env_file:
      - .env
    volumes:
      - pgdata:/var/lib/postgresql/data
    ports:
      - "5432:5432"
    networks:
      - app-network

  backend:
    build:
      context: ./backend
    image: backend:1.0.0
    container_name: nest-backend
    restart: unless-stopped
    env_file:
      - .env
    depends_on:
      - db
    ports:
      - "3001:3001"
    networks:
      - app-network

  frontend:
    build:
      context: ./frontend
    image: frontend:1.0.0
    container_name: next-frontend
    restart: unless-stopped
    env_file:
      - .env
    depends_on:
      - backend
    ports:
      - "3000:3000"
    networks:
      - app-network

volumes:
  pgdata:

networks:
  app-network:
```
