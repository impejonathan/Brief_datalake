
# Projet Azure Data Lake Gen2 - Sécurité et Configuration

## Description
Ce projet est conçu pour mettre en pratique la sécurisation et la configuration d'Azure Data Lake Storage Gen2. Il comprend différentes phases d'implémentation, de la veille technologique à la mise en place d'un système de monitoring, en passant par l'ingestion sécurisée des données.

## Prérequis
- Python 3.x
- Un compte Azure avec accès aux services suivants :
  - Azure Data Lake Storage Gen2
  - Azure Key Vault
  - Azure Databricks
- Variables d'environnement configurées (voir section Configuration)

## Installation
1. Cloner le repository
```bash
git clone [URL_DU_REPO]
```

2. Créer un environnement virtuel
```bash
python -m venv env
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows
```

3. Installer les dépendances
```bash
pip install -r requirements.txt
```

## Structure du Projet
```
├── Partie 1 Veille_doc/
│   └── Documentation et veille technologique (.md)
├── Partie 2/
│   ├── DATA/
│   ├── Documentation/
│   │   ├── LOG/ --> les logs en .json du data lake   ## (non disponible dans le .gitigonre) ##
│   │   └── blob_screen/ --> dossier avec screen du blog 
│   │   └── Screen/ --> dossier avec screen des SP , des logs .json , liste des RG pour tout le projet ,
│   ├── phase_1_1_super_user.ipynb
│   ├── phase_1_2_Read.ipynb
│   ├── phase_1_3_SPAIN.ipynb
│   ├── phase_2_Parquet.ipynb
│   └── Explication approche globale SP .md  
└── Partie 3/
    └── Screenshots Databricks/
```

## Configuration
Créer un fichier `.env` à la racine du projet avec les variables suivantes :
```
KEY_VAULT_URL=xxxxxxxxxxxxxxxxxxxx
WRITE_SECRET_NAME=xxxxxxxxxxxxxxxxxxxx
WRITE_CLIENT_ID=xxxxxxxxxxxxxxxxxxxx
READ_SECRET_NAME=xxxxxxxxxxxxxxxxxxxx
READ_CLIENT_ID=xxxxxxxxxxxxxxxxxxxx
TENANT_ID=xxxxxxxxxxxxxxxxxxxx
STORAGE_ACCOUNT_NAME=xxxxxxxxxxxxxxxxxxxx
CONTAINER_NAME=xxxxxxxxxxxxxxxxxxxx
```

## Description des Parties

### Partie 1 : Veille sur les Systèmes de Sécurité
Documentation et recherche sur les meilleures pratiques de sécurité pour Azure Data Lake.

### Partie 2 : Création et Ingestion Sécurisée
- Configuration des accès via Azure Key Vault
- Implémentation de différents niveaux d'accès
- Gestion des permissions granulaires
- Conversion et stockage en format Parquet
- Dans `Documentation` la journalisation des information sont cacher par le `.gitignore` + 3 screen shot

### Partie 3 : Configuration d'Azure Databricks
Screenshots et documentation de la configuration Databricks (Code non inclus pour des raisons de sécurité)

### Partie 4 : Monitoring et Alertes
Mise en place du système de surveillance et configuration des alertes

### Partie 5 : Bonus
Options disponibles :
- Ingestion Avancée (niveau 2)
- Exploration des Données avec Spark
- Révocation des Accès en Cas d'Incident
- Inspection du Pricing
- Utilisation de Terraform

## Sécurité
Les informations sensibles sont gérées via Azure Key Vault. Les credentials ne doivent jamais être exposés dans le code.

---








## Copie du PROJET 📚 voir [PDF "Data_Lake_partie_2__ingestion_avance_monitoring_et_scurit.pdf"](./PDF_Data_Lake_partie_2__ingestion_avance_monitoring_et_scurit.pdf) 🔍




## Copie du PROJET  voir PDF "Data_Lake_partie_2__ingestion_avance_monitoring_et_scurit.pdf"

