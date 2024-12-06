# Documentation des Services Principaux Azure

## Vue d'ensemble des Services
Deux services principaux ont été configurés pour ce projet :
- **IJ-service-principale-get-post** --> `exemple ICI le service principale du respsable DATA `
- **IJ-service-principale-post**  --> `exemple ICI le service principale du stagiaire  `

## Détail des Services Principaux pour le projet

### 1. IJ-service-principale-get-post
#### Permissions Complètes
- ✅ Lecture des fichiers
- ✅ Écriture des fichiers
- ✅ Suppression des fichiers

#### Usage
- Service dédié à la gestion complète du data lake
- Manipulation totale des données
- Opérations administratives

### 2. IJ-service-principale-post
#### Permissions Limitées
- ✅ Lecture des fichiers
- ❌ Écriture des fichiers
- ❌ Suppression des fichiers

#### Usage
- Consultation des données uniquement
- Extraction sécurisée
- Audit et monitoring
______________

## Stratégie d'Accès

### Justification des Permissions

#### IJ-service-principale-get-post
- Opérations complètes sur les données
- Gestion administrative du data lake
- Maintenance et mise à jour

#### IJ-service-principale-post
- Accès en lecture seule
- Protection contre les modifications
- Consultation sécurisée

## Sécurité
- Principe du `moindre privilège`
- Audit régulier des accès
- Gestion par groupes et rôles

## Azure Key Vault

### Structure des Secrets
```
keyvault-ij-prod
├── IJ-service-principale-get-post
│   ├── client-id
│   ├── client-secret
│   └── tenant-id
└── IJ-service-principale-post
    ├── client-id
    ├── client-secret
    └── tenant-id
```

### Avantages Key Vault
1. **Sécurité**
   - Centralisation des secrets
   - Chiffrement complet
   - Contrôle d'accès via Microsoft Entra ID

2. **Gestion**
   - Interface centralisée
   - Rotation simplifiée des secrets
   - Traçabilité des accès

3. **Intégration**
   - Pas de secrets en dur dans le code
   - Utilisation du .env pour les liens Key Vault uniquement
   - Récupération sécurisée des secrets 