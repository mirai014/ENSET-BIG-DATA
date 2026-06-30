
## 1. Description du projet

Dans le cadre du module Big Data à l'ENSET Mohammedia, nous avons réalisé cet atelier. Il s'agit de pipelines de données avec Apache Airflow, déployé via Docker Compose.

Apache Airflow permet de définir, exécuter et surveiller des pipelines sous forme de DAGs. Il ne remplace pas les outils de traitement comme Spark, Hadoop ou Flink. Son rôle est de coordonner ces outils dans un pipeline automatisé.


## 2. Objectifs de l'atelier (énoncé de TP:)

- comprendre le rôle d'Apache Airflow dans les pipelines Big Data
- expliquer ce qu'est un DAG
- créer un pipeline simple avec plusieurs tâches
- utiliser PythonOperator pour exécuter des fonctions Python
- simuler les étapes d'un pipeline Big Data
- définir l'ordre d'exécution des tâches
- exécuter un DAG depuis l'interface Web
- consulter les logs d'une tâche
- comprendre la planification automatique
- comprendre la gestion des erreurs et des reprises
- créer des dépendances parallèles dans un DAG
- expliquer pourquoi Airflow est important dans une architecture Data Engineering


## 3. Lancement de l'environnement

**Démarrage de Airflow :**
> docker compose up -d


**Vérifier les conteneurs actifs :**

>docker ps

**Accéder à l'interface Web :**
```
http://localhost:8080
Identifiants : airflow / airflow
```
| Tâche | Rôle dans le pipeline Big Data |
|---|---|
| `ingestion_donnees` | Simule la récupération des données depuis une source externe. Crée le fichier `ventes_raw.csv`. |
| `stockage_zone_brute` | Simule le stockage dans une zone brute du Data Lake. Vérifie l'existence du fichier et affiche sa taille. |
| `validation_donnees` | Vérifie l'existence du fichier et la structure des colonnes. |
| `transformation_donnees` | Nettoie les données et calcule la colonne `montant = prix × quantité`. Produit `ventes_clean.csv`. |
| `traitement_analytique` | Calcule le chiffre d'affaires total par ville. Produit `resultats_ventes.json`. |
| `chargement_resultats` | Simule le chargement des résultats dans une base analytique. |
| `generation_rapport` | Génère le rapport final `rapport_pipeline.txt`. |
