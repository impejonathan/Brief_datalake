# Veille Technologique : Microsoft Entra ID (ex-Azure Active Directory)

## Vue d'ensemble
[[1](https://learn.microsoft.com/en-us/entra/fundamentals/whats-new)][[2](https://learn.microsoft.com/en-us/entra/identity-platform/reference-breaking-changes)]
Microsoft Entra ID est le service d'identité cloud de Microsoft qui gère l'authentification et l'autorisation pour les ressources Azure, notamment les Data Lakes. Il remplace Azure Active Directory avec des fonctionnalités étendues de sécurité et de gestion des identités.

## Fonctionnalités Clés pour Data Lake
[[1](https://learn.microsoft.com/en-us/entra/fundamentals/whats-new)]
- Authentification unique (SSO)
- Authentification multifacteur (MFA)
- Gestion des accès conditionnels
- Contrôle d'accès basé sur les rôles (RBAC)
- Intégration avec les services Azure

## Nouveautés Importantes (2024)
[[1](https://learn.microsoft.com/en-us/entra/fundamentals/whats-new)]
1. **Authentification Renforcée**
   - Support des Passkeys dans Microsoft Authenticator
   - MFA obligatoire pour l'accès au centre d'administration
   - Détection améliorée des attaques "Man-in-the-Middle"

2. **Sécurité Améliorée**
   - Protection contre les menaces internes
   - Nouvelles politiques d'accès conditionnel
   - Support FIPS 140 pour l'authentification Android

## Exemple Pratique 1 : Configuration RBAC pour Data Lake
```powershell
# Attribution d'un rôle pour l'accès au Data Lake
New-AzRoleAssignment `
    -SignInName "utilisateur@entreprise.com" `
    -RoleDefinitionName "Storage Blob Data Reader" `
    -Scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-account}"
```

## Exemple Pratique 2 : Authentification dans une Application
[[1](https://learn.microsoft.com/en-us/entra/fundamentals/whats-new)]
```python
from azure.identity import DefaultAzureCredential
from azure.storage.filedatalake import DataLakeServiceClient

# Utilisation de l'authentification moderne
credential = DefaultAzureCredential()
service_client = DataLakeServiceClient(
    account_url="https://{account}.dfs.core.windows.net",
    credential=credential
)
```

## Bonnes Pratiques
[[1](https://learn.microsoft.com/en-us/entra/fundamentals/whats-new)][[2](https://learn.microsoft.com/en-us/entra/identity-platform/reference-breaking-changes)]
1. **Sécurité**
   - Activer MFA pour tous les utilisateurs
   - Utiliser l'accès conditionnel
   - Implémenter le principe du moindre privilège

2. **Gestion des Identités**
   - Créer des groupes pour la gestion des accès
   - Utiliser des identités managées pour les services
   - Réviser régulièrement les accès

3. **Surveillance**
   - Activer les journaux d'audit
   - Configurer les alertes de sécurité
   - Surveiller les tentatives d'accès suspectes

## Changements Importants à Venir
[[1](https://learn.microsoft.com/en-us/entra/fundamentals/whats-new)]
- Migration obligatoire vers Microsoft Graph avant juillet 2025
- Retrait des PowerShell AzureAD et MSOnline en mars 2025
- Nouvelle expérience d'authentification pour les applications

## Points de Vigilance
[[1](https://learn.microsoft.com/en-us/entra/fundamentals/whats-new)]
- MFA obligatoire pour l'administration à partir d'octobre 2024
- Nécessité de mettre à jour les scripts PowerShell existants
- Révision des pratiques d'authentification héritées

## Documentation Officielle
- [Documentation Microsoft Entra ID](https://learn.microsoft.com/fr-fr/entra/fundamentals/whats-new)
- [Guide d'implémentation pour Data Lake](https://learn.microsoft.com/fr-fr/azure/storage/blobs/data-lake-storage-access-control)

Microsoft Entra ID est fondamental pour la sécurisation d'un Data Lake, offrant une gestion centralisée des identités et des accès avec des fonctionnalités avancées de sécurité et de conformité. 