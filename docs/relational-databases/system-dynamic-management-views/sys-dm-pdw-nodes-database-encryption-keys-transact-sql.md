---
title: sys.dm_pdw_nodes_database_encryption_keys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: e7fd02b2-5d7e-4816-a0af-b58ae2ac3f7a
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: ea3221e859093667883109c1e3977daa753230c1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmpdwnodesdatabaseencryptionkeys-transact-sql"></a>sys.dm_pdw_nodes_database_encryption_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Retorna informações sobre o estado de criptografia de um banco de dados e suas chaves de criptografia de banco de dados associadas. **sys.dm_pdw_nodes_database_encryption_keys** fornece essas informações para cada nó. Para obter mais informações sobre criptografia de banco de dados, consulte [criptografia transparente de dados (SQL Server PDW)](http://msdn.microsoft.com/en-us/b82ad21d-09dd-43dd-8fab-bcf2c8c3ac6d).  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|database_id|**Int**|ID do banco de dados físico em cada nó.|  
|encryption_state|**Int**|Indica se o banco de dados neste nó estiver criptografado ou não criptografado.<br /><br /> 0 = Nenhuma chave de criptografia de banco de dados presente, nenhuma criptografia<br /><br /> 1 = Sem-criptografia<br /><br /> 2 = Criptografia em andamento<br /><br /> 3 = Criptografado<br /><br /> 4 = Alteração de chave em andamento<br /><br /> 5 = Descriptografia em andamento<br /><br /> 6 = alteração de proteção em andamento (o certificado que está criptografando a chave de criptografia do banco de dados está sendo alterado.)|  
|create_date|**datetime**|Exibe a data em que a chave de criptografia foi criada.|  
|regenerate_date|**datetime**|Exibe a data em que a chave de criptografia foi gerada novamente.|  
|modify_date|**datetime**|Exibe a data em que a chave de criptografia foi modificada.|  
|set_date|**datetime**|Exibe a data em que a chave de criptografia foi aplicada ao banco de dados.|  
|opened_date|**datetime**|Mostra quando a chave de banco de dados foi aberta pela última vez.|  
|key_algorithm|**varchar(?)**|Exibe o algoritmo que é usado para a chave.|  
|key_length|**Int**|Exibe o comprimento da chave.|  
|encryptor_thumbprint|**varbin**|Mostra a impressão digital do criptografador.|  
|percent_complete|**real**|Porcentagem concluída da alteração de estado da criptografia do banco de dados. Será 0 se não houver nenhuma alteração de estado.|  
|node_id|**Int**|Id numérico exclusivo associado ao nó.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW SERVER STATE no servidor.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 A exemplo a seguir adiciona `sys.dm_pdw_nodes_database_encryption_keys` a outras tabelas do sistema para indicar o estado de criptografia para bancos de dados protegidos de cada nó da TDE.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse Parallel Data Warehouse e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)  
  
  

