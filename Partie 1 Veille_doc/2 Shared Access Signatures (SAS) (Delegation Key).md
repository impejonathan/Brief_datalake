# Veille Technologique : Shared Access Signatures (SAS) pour Azure Data Lake

## Vue d'ensemble
[[1](https://learn.microsoft.com/en-us/azure/storage/common/storage-sas-overview)]
Les Shared Access Signatures (SAS) permettent un accès délégué sécurisé aux ressources dans Azure Storage. Elles offrent un contrôle granulaire sur :
- Les ressources accessibles
- Les permissions accordées
- La durée de validité de l'accès

## Types de SAS
[[1](https://learn.microsoft.com/en-us/azure/storage/common/storage-sas-overview)][[2](https://learn.microsoft.com/en-us/rest/api/storageservices/create-user-delegation-sas)]

1. **User Delegation SAS**
   - Sécurisé avec les identifiants Microsoft Entra (Azure AD)
   - Recommandé pour la meilleure sécurité
   - Supporté pour Blob Storage et Data Lake Storage

2. **Service SAS**
   - Sécurisé avec la clé du compte de stockage
   - Accès à une ressource spécifique

3. **Account SAS**
   - Sécurisé avec la clé du compte de stockage
   - Accès à plusieurs services

## Exemple Pratique 1 : Création d'un User Delegation SAS avec PowerShell
[[3](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-access-control-model)][[6](https://4sysops.com/archives/managing-user-delegation-in-azure-storage-with-shared-access-signature-sas-tokens/)]
```powershell
# Création du contexte de stockage
$strContext = New-AzStorageContext -StorageAccountName "monDataLake" -UseConnectedAccount

# Attribution du rôle nécessaire
New-AzRoleAssignment -SignInName "user@domain.com" `
  -RoleDefinitionName "Storage Blob Data Contributor" `
  -Scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-account}"

# Création du token SAS
New-AzStorageContainerSASToken -Context $strContext `
  -Name "monContainer" `
  -Permission "racwdl" `
  -ExpiryTime (Get-Date).AddDays(7)
```

## Exemple Pratique 2 : Utilisation d'un SAS Token
[[1](https://learn.microsoft.com/en-us/azure/storage/common/storage-sas-overview)][[2](https://learn.microsoft.com/en-us/rest/api/storageservices/create-user-delegation-sas)]
```python
# URL avec SAS token
url = "https://moncompte.blob.core.windows.net/container/fichier.csv?sv=2021-06-08&st=2024-01-01T00%3A00%3A00Z&se=2024-12-31T23%3A59%3A59Z&sr=b&sp=r&sig=XXXXX"

# Utilisation avec le SDK Azure
from azure.storage.blob import BlobClient
blob_client = BlobClient.from_blob_url(url)
```

## Bonnes Pratiques
[[1](https://learn.microsoft.com/en-us/azure/storage/common/storage-sas-overview)]
1. **Sécurité renforcée**
   - Toujours utiliser HTTPS
   - Privilégier User Delegation SAS
   - Définir des délais d'expiration courts

2. **Gestion des accès**
   - Appliquer le principe du moindre privilège
   - Implémenter un plan de révocation
   - Configurer une politique d'expiration

3. **Surveillance**
   - Utiliser Azure Monitor
   - Activer les logs de stockage
   - Suivre les échecs d'autorisation

## Points de Vigilance
[[1](https://learn.microsoft.com/en-us/azure/storage/common/storage-sas-overview)][[6](https://4sysops.com/archives/managing-user-delegation-in-azure-storage-with-shared-access-signature-sas-tokens/)]
- Durée maximale de 7 jours pour les User Delegation SAS
- Impossibilité d'auditer la génération des tokens SAS
- Facturation basée sur l'utilisation, même via SAS
- Nécessité de renouveler les tokens avant expiration

## Documentation Officielle
- [Vue d'ensemble des SAS](https://learn.microsoft.com/fr-fr/azure/storage/common/storage-sas-overview)
- [Guide d'implémentation des User Delegation SAS](https://learn.microsoft.com/fr-fr/azure/storage/blobs/storage-blob-user-delegation-sas-create-dotnet)

Ce mécanisme est particulièrement utile pour un Data Lake car il permet de donner un accès temporaire et contrôlé aux données sans exposer les clés principales du compte de stockage. 