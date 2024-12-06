# Configuration Databricks pour Azure Storage

## Template Original Azure
```python
service_credential = dbutils.secrets.get(scope="<scope>",key="<service-credential-key>")

spark.conf.set("fs.azure.account.auth.type.<storage-account>.dfs.core.windows.net", "OAuth")
spark.conf.set("fs.azure.account.oauth.provider.type.<storage-account>.dfs.core.windows.net", "org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider")
spark.conf.set("fs.azure.account.oauth2.client.id.<storage-account>.dfs.core.windows.net", "<application-id>")
spark.conf.set("fs.azure.account.oauth2.client.secret.<storage-account>.dfs.core.windows.net", service_credential)
spark.conf.set("fs.azure.account.oauth2.client.endpoint.<storage-account>.dfs.core.windows.net", "https://login.microsoftonline.com/<directory-id>/oauth2/token")
```


## Explication des Composants

1. **Gestion des Secrets**
   - Récupération sécurisée des credentials via le scope service pricipale "xxxxxxx"

2. **Configuration OAuth**
   - Type d'authentification : OAuth
   - Provider : ClientCredsTokenProvider
   - Client ID : ID de l'application Microsoft Entra ID
   - Secret : Credential sécurisé
   - Endpoint : Point de terminaison OAuth Azure

Cette configuration établit une connexion sécurisée entre Databricks et Azure Storage en utilisant un service principal créé dans Microsoft Entra ID. 