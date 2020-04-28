---
title: sys. dm_pdw_nodes_database_encryption_keys (Transact-SQL)
ms.custom: seo-dt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: e7fd02b2-5d7e-4816-a0af-b58ae2ac3f7a
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c319259d8997db2ff39d90b408056d03eb008782
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401647"
---
# <a name="sysdm_pdw_nodes_database_encryption_keys-transact-sql"></a>sys. dm_pdw_nodes_database_encryption_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Retorna informações sobre o estado de criptografia de um banco de dados e suas chaves de criptografia de banco de dados associadas. **Sys. dm_pdw_nodes_database_encryption_keys** fornece essas informações para cada nó. Para obter mais informações sobre criptografia de banco de dados, consulte [Transparent Data Encryption (SQL Server PDW)](../../analytics-platform-system/transparent-data-encryption.md).  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|  
|database_id|**int**|ID do banco de dados físico em cada nó.|  
|encryption_state|**int**|Indica se o banco de dados neste nó está criptografado ou não está criptografado.<br /><br /> 0 = Nenhuma chave de criptografia de banco de dados presente, nenhuma criptografia<br /><br /> 1 = Sem-criptografia<br /><br /> 2 = Criptografia em andamento<br /><br /> 3 = Criptografado<br /><br /> 4 = Alteração de chave em andamento<br /><br /> 5 = Descriptografia em andamento<br /><br /> 6 = alteração de proteção em andamento (o certificado que está criptografando a chave de criptografia de banco de dados está sendo alterado).|  
|create_date|**datetime**|Exibe a data em que a chave de criptografia foi criada.|  
|regenerate_date|**datetime**|Exibe a data em que a chave de criptografia foi gerada novamente.|  
|modify_date|**datetime**|Exibe a data em que a chave de criptografia foi modificada.|  
|set_date|**datetime**|Exibe a data em que a chave de criptografia foi aplicada ao banco de dados.|  
|opened_date|**datetime**|Mostra quando a chave de banco de dados foi aberta pela última vez.|  
|key_algorithm|**varchar (?)**|Exibe o algoritmo que é usado para a chave.|  
|key_length|**int**|Exibe o comprimento da chave.|  
|encryptor_thumbprint|**varbin**|Mostra a impressão digital do criptografador.|  
|percent_complete|**real**|Porcentagem concluída da alteração de estado da criptografia do banco de dados. Será 0 se não houver nenhuma alteração de estado.|  
|node_id|**int**|ID numérica exclusiva associada ao nó.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW SERVER STATE no servidor.  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir une `sys.dm_pdw_nodes_database_encryption_keys` outras tabelas do sistema para indicar o estado de criptografia para cada nó dos bancos de dados protegidos por TDE.  
  
```  
SELECT D.database_id AS DBIDinMaster, D.name AS UserDatabaseName,   
PD.pdw_node_id AS NodeID, DM.physical_name AS PhysDBName,   
keys.encryption_state  
FROM sys.dm_pdw_nodes_database_encryption_keys AS keys  
JOIN sys.pdw_nodes_pdw_physical_databases AS PD  
    ON keys.database_id = PD.database_id AND keys.pdw_node_id = PD.pdw_node_id  
JOIN sys.pdw_database_mappings AS DM  
    ON DM.physical_name = PD.physical_name  
JOIN sys.databases AS D  
    ON D.database_id = DM.database_id  
ORDER BY D.database_id, PD.pdw_node_ID;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico de SQL Data Warehouse e paralelo data warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [CRIAR chave de criptografia de banco de dados &#40;&#41;Transact-SQL](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [A chave de criptografia ALTER DATABASE &#40;&#41;Transact-SQL](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)  
  
  

