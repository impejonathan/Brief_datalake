# Veille Technologique : IAM et Role-Based Access Control (RBAC) Azure 2024

## Vue d'ensemble
[[1](https://learn.microsoft.com/fr-fr/azure/role-based-access-control/best-practices)][[2](https://learn.microsoft.com/en-us/azure/role-based-access-control/best-practices)]
IAM (Identity and Access Management) et RBAC dans Azure permettent de gérer finement les accès aux ressources cloud, particulièrement crucial pour les Data Lakes. Le système RBAC d'Azure offre une gestion des autorisations basée sur les rôles, permettant un contrôle granulaire des accès.

## Évolutions Majeures 2024
[[3](https://learn.microsoft.com/en-us/answers/questions/1920555/transition-to-role-based-access-control-(rbac)-in)]
- Retrait des rôles d'administrateur classiques Azure prévu pour le 31 août 2024
- Transition obligatoire vers le nouveau modèle RBAC
- Nouvelles fonctionnalités de gestion des accès conditionnels

## Principes Fondamentaux
[[2](https://learn.microsoft.com/en-us/azure/role-based-access-control/best-practices)][[7](https://www.strongdm.com/blog/iam-best-practices)]
1. **Composants Clés**
   - Rôles (définitions des permissions)
   - Portées (scope des autorisations)
   - Attributions (association rôle-utilisateur)

2. **Types de Contrôle d'Accès**
   - RBAC (basé sur les rôles)
   - ABAC (basé sur les attributs)
   - Accès Just-in-Time

## Exemple Pratique 1 : Attribution de Rôle Data Lake
[[1](https://learn.microsoft.com/fr-fr/azure/role-based-access-control/best-practices)][[2](https://learn.microsoft.com/en-us/azure/role-based-access-control/best-practices)]
```powershell
# Attribution d'un rôle de contributeur de données
New-AzRoleAssignment `
    -SignInName "analyste@entreprise.com" `
    -RoleDefinitionName "Storage Blob Data Contributor" `
    -ResourceGroupName "DataLakeGroup" `
    -ResourceName "monDatalake" `
    -ResourceType "Microsoft.Storage/storageAccounts"
```

## Exemple Pratique 2 : Création d'un Rôle Personnalisé
[[1](https://learn.microsoft.com/fr-fr/azure/role-based-access-control/best-practices)]
```json
{
    "Name": "Data Lake Reader Custom",
    "Description": "Permet la lecture des données uniquement",
    "Actions": [
        "Microsoft.Storage/storageAccounts/blobServices/containers/read",
        "Microsoft.Storage/storageAccounts/blobServices/generateUserDelegationKey/action"
    ],
    "NotActions": [],
    "AssignableScopes": [
        "/subscriptions/{subscription-id}/resourceGroups/{resource-group}"
    ]
}
```

## Meilleures Pratiques 2024
[[1](https://learn.microsoft.com/fr-fr/azure/role-based-access-control/best-practices)][[2](https://learn.microsoft.com/en-us/azure/role-based-access-control/best-practices)]

1. **Sécurité**
   - Appliquer le principe du moindre privilège
   - Limiter le nombre de propriétaires d'abonnement
   - Utiliser des groupes plutôt que des attributions individuelles

2. **Gestion des Rôles**
   - Éviter l'utilisation de caractères génériques
   - Préférer les ID de rôle uniques aux noms
   - Implémenter des audits réguliers

3. **Administration**
   - Centraliser la gestion des logs
   - Automatiser les workflows d'attribution
   - Mettre en place des revues d'accès périodiques

## Points de Vigilance Critiques
[[7](https://www.strongdm.com/blog/iam-best-practices)][[1](https://learn.microsoft.com/fr-fr/azure/role-based-access-control/best-practices)]
- Limitation du nombre d'administrateurs privilégiés
- Utilisation de Microsoft Entra PIM pour les accès privilégiés
- Mise en place d'audits trimestriels des accès
- Documentation des attributions de rôles

## Recommandations Zero Trust
[[2](https://learn.microsoft.com/en-us/azure/role-based-access-control/best-practices)][[7](https://www.strongdm.com/blog/iam-best-practices)]
1. **Authentification**
   - Vérification continue
   - MFA obligatoire
   - Accès conditionnels

2. **Autorisation**
   - Just-in-Time Access
   - Privilèges minimaux
   - Révision régulière des accès

## Changements Importants
[[3](https://learn.microsoft.com/en-us/answers/questions/1920555/transition-to-role-based-access-control-(rbac)-in)][[4](https://github.com/MicrosoftDocs/azure-docs/blob/main/articles/role-based-access-control/best-practices.md)]
- Migration nécessaire des rôles classiques avant août 2024
- Nouvelles fonctionnalités de gestion des accès conditionnels
- Intégration renforcée avec Microsoft Entra ID

## Documentation Officielle
- [Guide des meilleures pratiques RBAC](https://learn.microsoft.com/fr-fr/azure/role-based-access-control/best-practices)
- [Documentation IAM Azure](https://learn.microsoft.com/fr-fr/azure/active-directory/fundamentals/identity-access-management)

L'IAM et le RBAC sont essentiels pour la sécurisation d'un Data Lake, offrant un contrôle précis des accès tout en maintenant la flexibilité nécessaire pour les équipes data. 