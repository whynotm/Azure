# Azure Storage

https://docs.microsoft.com/fr-fr/learn/modules/create-azure-storage-account/2-decide-how-many-storage-accounts-you-need

## 


## 

## 





## Notes

- Au minimum, Azure gère automatiquement une copie de vos données dans le centre de données associé au compte de stockage.
Il s’agit du stockage localement redondant (LRS) qui vous protège contre les défaillances matérielles, mais non contre un événement qui endommage l’ensemble du centre de données
-  Hot/Cold : Cela s’applique uniquement aux objets blob et sert de valeur par défaut pour les nouveaux objets blob.
- Un compte de stockage représente un regroupement de paramètres tels que l’emplacement, la stratégie de réplication et le propriétaire de l’abonnement. Vous avez besoin d’un compte de stockage pour chaque groupe de paramètres que vous souhaitez appliquer à vos données.
- Chaque compte de stockage a un nom. Le nom doit être globalement unique dans Azure
- All data written to Azure Storage is encrypted by the service.
- A single Azure subscription can host up to 200 storage accounts, each of which can hold 500 TB of data
- Tables: A NoSQL store for schemaless storage of structured data. This service has been replaced by Azure Cosmos DB and will not be discussed here.
- 
