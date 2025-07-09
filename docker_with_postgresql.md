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

