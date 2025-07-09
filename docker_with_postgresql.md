#### Se connecter à PostgreSQL dans un conteneur
```zsh
docker exec -it postgres-container psql -U mon_user -d ma_base
```

#### Enregistrer une vue en base :

####  Depuis l’extérieur du conteneur (client psql installé sur la machine hôte)
```zsh
psql -h localhost -U postgres -d ma_base -f ma_vue.sql
```

####  Depuis un fichier .sql injecté dans la base via Docker (conteneur PostgreSQL)
```zsh
docker exec -i nom_du_conteneur \
  psql -U utilisateur -d base \
  < fichier.sql
```


Aide psql

# Une fois connecté :
```zsh
	•	Lister les bases : \l
	•	Lister les tables : \dt
	•	Afficher les colonnes : \d nom_table
	•	Quitter : \q
```

