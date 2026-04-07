# 🔵 RetailSense — Analyse Churn & Segmentation Client E-commerce

> Projet personnel réalisé dans le cadre d'une formation MBA Big Data & IA,
> pour développer des compétences concrètes en analyse de données et ML.

## 📌 Problématique

Dans le secteur e-commerce, acquérir un nouveau client coûte 5 à 7 fois plus
cher que d'en fidéliser un existant. Pourtant, la majorité des enseignes
ne disposent pas d'un système pour identifier les clients sur le point de partir.

RetailSense répond à cette problématique en analysant le comportement d'achat
de 4 338 clients réels sur 1 an, en les segmentant par valeur, et en prédisant
leur risque de churn avec un modèle Machine Learning.

**Résultat : 96% de précision sur la prédiction du churn.**

## 📊 Dataset

- **Source** : Online Retail II — UCI Machine Learning Repository (Kaggle)
- **Période** : Décembre 2010 — Décembre 2011
- **Volume** : 541 910 transactions → 397 885 après nettoyage
- **Marché** : E-commerce UK

## 🔍 Méthodologie

### 1. Nettoyage des données
- Suppression des lignes sans Customer ID (135 080 lignes)
- Suppression des retours et annulations
- Création de la colonne TotalPrice

### 2. Segmentation RFM
Calcul de 3 métriques par client :
- **Récence** — jours depuis le dernier achat
- **Fréquence** — nombre de commandes
- **Montant** — chiffre d'affaires total généré

| Segment | Clients | Montant Moyen |
|---|---|---|
| Champion | 932 | 6 705£ |
| Fidèle | 1 007 | 1 396£ |
| À risque | 1 092 | 816£ |
| Perdu | 1 307 | 280£ |

### 3. Modèle de prédiction du churn
- **Algorithme** : Random Forest (100 arbres)
- **Accuracy** : 96%
- **Variable la plus prédictive** : Récence (36%)

### 4. Dashboard Power BI
Restitution décideur avec 5 visuels : segmentation, CA par pays,
clients à risque haute valeur, montant moyen par segment.

## 🖼️ Aperçu

### Segmentation RFM
![Segmentation RFM](docs/segmentation_rfm.png)

### Analyse RFM complète
![Analyse RFM](docs/analyse_rfm.png)

### Importance des variables
![Importance variables](docs/importance_variables.png)

## 🛠️ Stack technique

| Outil | Rôle |
|---|---|
| Python (pandas) | Chargement et nettoyage des données |
| Python (scikit-learn) | Modèle Random Forest |
| SQLite | Requêtes analytiques SQL |
| Matplotlib / Seaborn | Visualisations |
| Power BI | Dashboard décideur |
| Git | Versioning |

## 📂 Structure du repo
