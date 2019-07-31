# Azure Storage

https://docs.microsoft.com/fr-fr/learn/modules/create-azure-storage-account/2-decide-how-many-storage-accounts-you-need

## 


## 

##  BLOB
- Block blobs :  are used to hold text or binary files up to ~5 TB (50,000 blocks of 100 MB) in size
- Pages Blobs : They are named page blobs because they provide random read/write access to 512-byte pages.
- Append blobs are made up of blocks like block blobs, but they are optimized for append operations ; A single append blob can be up to 195 GB.


## FILES
Azure Files enables you to set up highly available network file shares that can be accessed by using the standard Server Message Block (SMB) protocol. 


## Queues 
- The Azure Queue service is used to store and retrieve messages.
- Queue messages can be up to 64 KB in size, and a queue can contain millions of messages. 
- Queues are generally used to store lists of messages to be processed asynchronously. 
 
## Azure storage accounts
- To access any of these services from an application, you have to create a storage account

## Storage and key access

	- Key Vaults include support to synchronize directly to the Storage Account and automatically rotate the keys periodically. 
	- The REST endpoint is a combination of your storage account name, the data type, and a known domain. For example:
				-	Data type	Example endpoint
				-	Blobs	https://[name].blob.core.windows.net/
				-	Queues	https://[name].queue.core.windows.net/
				-	Table	https://[name].table.core.windows.net/
				-	Files	https://[name].file.core.windows.net/


## Notes

- Au minimum, Azure gère automatiquement une copie de vos données dans le centre de données associé au compte de stockage.
Il s’agit du stockage localement redondant (LRS) qui vous protège contre les défaillances matérielles, mais non contre un événement qui endommage l’ensemble du centre de données
-  Hot/Cold : Cela s’applique uniquement aux objets blob et sert de valeur par défaut pour les nouveaux objets blob.
- Un compte de stockage représente un regroupement de paramètres tels que l’emplacement, la stratégie de réplication et le propriétaire de l’abonnement. Vous avez besoin d’un compte de stockage pour chaque groupe de paramètres que vous souhaitez appliquer à vos données.
- Chaque compte de stockage a un nom. Le nom doit être globalement unique dans Azure
- All data written to Azure Storage is encrypted by the service.
- A single Azure subscription can host up to 200 storage accounts, each of which can hold 500 TB of data
- Tables: A NoSQL store for schemaless storage of structured data. This service has been replaced by Azure Cosmos DB and will not be discussed here.
-  For example, cool storage and archive storage are not supported in GPv1

