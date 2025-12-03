# 🌍 Analyse de données climatiques NOAA (2020 2024)
 
## 📌 Objectif du projet

Ce projet consiste à concevoir une architecture DataLake big data dédiée à l’ingestion, la persistance et au traitement de données climatiques issues du dataset GSOD – Global Summary of the Day (NOAA).
L’objectif final est de produire un dashboard interactif permettant d’analyser les tendances climatiques, détecter les anomalies et visualiser des statistiques pertinentes par station et par période.

## 🗂 Source des données

Les données utilisées proviennent de la NOAA :
🔗 https://www.ncei.noaa.gov/data/global-summary-of-the-day/archive/

## 🏗 Architecture DataLake

Le DataLake est organisé en quatre couches principales selon les bonnes pratiques Big Data.

#### 1.RAW – Ingestion

Stockage brut et immuable des données téléchargées.

Formats : .tar.gz → CSV extraits.

Conservation des données sources pour audit et reprise.

Volume : climat.raw.gsod_raw

Contenu : fichiers CSV annuels non nettoyés.

#### 2.BRONZE / SILVER – Structuration & nettoyage

Lecture des fichiers CSV et persistances des données structurées.

Colonnes sélectionnées :
STATION, NAME, DATE, TEMP, PRCP, LATITUDE, LONGITUDE

Table Delta BRONZE : climat.bronze.gsod_bronze_2020_2024

#### 3.SILVER – Nettoyage avancé

Filtre des valeurs aberrantes :
TEMP < -80°C ou > 60°C, PRCP > 500mm

Suppression des lignes incomplètes.

Normalisation des noms de stations + extraction de YEAR.

Table Delta SILVER : climat.silver.gsod_silver_2020_2024

Préparation des données pour EDA & GOLD.

#### 4. GOLD – Insights & Analytique

Données agrégées et enrichies pour reporting.

Ajout des colonnes : MONTH, TEMP_ANOMALY, PRCP_ANOMALY

Agrégations mensuelles et annuelles par station.

Tables générées :

Table	Description
climat.gold.gsod_gold_yearly2	Moyenne annuelle + nombre d’anomalies
climat.gold.gsod_gold_monthly2	Moyenne mensuelle par station

➡ Facilite les dashboards, visualisations et analyses temporelles.

## 📊 Dashboard & Visualisations

<img width="1603" height="536" alt="image" src="https://github.com/user-attachments/assets/65e19f80-98c4-4d33-9403-9b3f4f0d9845" />

Lien :

🔗 https://dbc-7075e14c-3009.cloud.databricks.com/dashboardsv3/01f0cf065db11e01911237e03c34b2aa/published?o=2009109254176417

#### Visualisations disponibles :

➡ Températures et précipitations moyennes par station/période

➡ Histogrammes et distribution des anomalies

➡ Analyse temporelle mensuelle & annuelle

## 🛠 Technologies utilisées

#### Databricks

<img width="1200" height="630" alt="image" src="https://github.com/user-attachments/assets/fb8c0b6b-58f0-45cf-8b5b-6762cf0a4b37" />


## 🚧 Limites & Contraintes

📉 Données

Stations parfois incomplètes ou bruitées.

Dataset limité à 2020–2024 (analyses longues limitées).

Anomalies identifiées mais nécessitent parfois validation métier.

🔎 Analyse

Carte interactive non finalisée.

Pas de heatmap ni étude spatiale approfondie.

Corrélation spatiale inter-stations non réalisée.

⚙ Partie technique

Géospatial avancé non exploité (GeoAnalytics, Kepler.gl, Folium…).

Dashboard centré sur statistiques temporelles, peu cartographique.

🔬 Fonctionnel

Aucune IA/ML intégrée pour la prédiction climatique.

Dashboard exploratoire, non décisionnel ou prédictif.

## 📥 Prochaines améliorations possibles

✔ Ajout de visualisations cartographiques (heatmaps, densité)

✔ Intégration de librairies géospatiales (geopandas, folium…)

✔ Ajout d’un modèle de détection/prédiction climatique (ML)

✔ Automatisation complète de la pipeline (Airflow / Databricks Jobs)

