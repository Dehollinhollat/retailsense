# 📋 Méthodologie — RetailSense

## 1. Contexte et objectif

Le churn client est l'un des enjeux majeurs du e-commerce. Ce projet
avait pour objectif de construire un pipeline Data complet — du
nettoyage des données brutes à la restitution décideur — sur un
dataset réel de 541 910 transactions.

## 2. Choix du dataset

Le dataset Online Retail II (UCI / Kaggle) a été choisi pour trois
raisons :
- Données réelles d'un e-commerce UK sur 1 an
- Volume suffisant pour un modèle ML crédible
- Présence de cas concrets : retours, annulations, clients anonymes

## 3. Nettoyage des données

| Problème identifié | Traitement appliqué | Impact |
|---|---|---|
| 135 080 lignes sans Customer ID | `dropna` sur Customer ID | Impossible d'analyser sans identifiant |
| Quantités négatives (retours) | Filtre `Quantity > 0` | Évite de biaiser les montants |
| Factures annulées (préfixe "C") | Filtre `~startswith('C')` | Exclut les transactions non réalisées |
| Prix nuls ou négatifs | Filtre `Price > 0` | Données incohérentes |
| Encodage Latin-1 | `encoding='latin-1'` | Le fichier contient des caractères £ |

Résultat : 397 885 lignes exploitables soit 73% du dataset initial.

## 4. Segmentation RFM

### Pourquoi la méthode RFM ?
La RFM est la méthode standard en marketing client. Elle est
interprétable par des non-techniciens (managers, directeurs
commerciaux) et produit des segments actionnables directement.

### Définition du churn
Un client est considéré churné s'il appartient au segment "Perdu"
(Score Total ≤ 6/15). Ce seuil a été défini par quintiles sur
les 3 métriques RFM.

## 5. Modèle Machine Learning

### Pourquoi Random Forest ?
- Robuste aux outliers (ex: client 12346 avec 77 183£) 
- Pas besoin de normalisation des données. Les données ne sont pas linéaires, La régression logistique suppose une
relation linéaire entre les variables et le churn. Dans mon dataset, un client avec une récence de 30 jours n'a pas exactement
deux fois moins de risque qu'un client à 60 jours. La relation est plus complexe et non-linéaire.
- Fournit une importance des variables interprétable
- Excellentes performances sans tuning complexe

### Résultats
- Accuracy : 96%
- Recall Churné : 93% — le modèle détecte 93% des churns réels
- Variable la plus prédictive : Récence (35.7%)

### Interprétation business
La Récence domine car un client qui n'achète plus depuis longtemps
envoie le signal le plus fort de désengagement, indépendamment
de son historique de dépenses.

## 6. Analyse SQL

SQLite a été utilisé pour reproduire les analyses en SQL,
compétence attendue dans les postes Data. Les requêtes ont permis
d'identifier :
- La concentration géographique du CA (UK = 94%)
- Les clients à risque haute valeur (priorité de rétention)
- Le comportement moyen par segment

## 7. Difficultés rencontrées

| Difficulté | Solution |
|---|---|
| Encodage UTF-8 invalide | Paramètre `encoding='latin-1'` |
| Fichier xlsx introuvable | Le fichier Kaggle était en CSV |
| Modules non installés | `pip install scikit-learn matplotlib seaborn` |
| Cellules exécutées dans le mauvais ordre | Run All Cells depuis le début |

## 8. Améliorations possibles

- Ajout d'un modèle XGBoost pour comparer les performances en ML
- Calcul d'un score de valeur vie client (CLV) par segment
- Automatisation du pipeline avec n8n (connexion avec FlowReport)
- Déploiement d'une API de scoring churn en temps réel

## 9. Compétences développées

- Nettoyage de données réelles (541 910 lignes)
- Segmentation RFM appliquée au e-commerce
- Modélisation prédictive avec scikit-learn
- Requêtes analytiques SQL sur SQLite
- Restitution décideur avec Power BI
- Documentation technique professionnelle
