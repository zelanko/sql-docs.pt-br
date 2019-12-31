---
title: sys. pdw_nodes_pdw_physical_databases (Transact-SQL)
ms.custom: seo-dt-2019
ms.date: 03/09/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 70e0939d-4d97-4ae0-ba16-934e0a80e718
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 48f2a2d485f99b91b0f30a6a707a900ccbbeea96
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399914"
---
# <a name="syspdw_nodes_pdw_physical_databases-transact-sql"></a>sys. pdw_nodes_pdw_physical_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Contém uma linha para cada banco de dados físico em um nó de computação. Agregue informações do banco de dados físico para obter informações detalhadas sobre bancos de dados. Para combinar informações, ingresse nas `sys.pdw_nodes_pdw_physical_databases` tabelas `sys.pdw_database_mappings` e `sys.databases` .  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|  
|database_id|**inteiro**|A ID de objeto do banco de dados. Observe que esse valor não é o mesmo que um database_id na exibição de [&#41;sys. databases &#40;Transact-SQL](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) .|  
|physical_name|**sysname**|O nome físico do banco de dados nos nós de shell/computação. Esse valor é o mesmo que um valor na coluna physical_name no modo de exibição [pdw_database_mappings &#40;do Transact-&#41;SQL](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md) .|  
|pdw_node_id|**inteiro**|ID numérica exclusiva associada ao nó.|  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-returning"></a>R. VOLUÇÃO  
 A consulta a seguir retorna o nome e a ID de cada banco de dados no mestre e o nome do banco de dados correspondente em cada nó de computação.  
  
```  
SELECT D.database_id AS DBID_in_master, D.name AS UserDatabaseName,   
PD.pdw_node_id AS NodeID, DM.physical_name AS PhysDBName   
FROM sys.databases AS D  
JOIN sys.pdw_database_mappings AS DM  
    ON D.database_id = DM.database_id  
JOIN sys.pdw_nodes_pdw_physical_databases AS PD  
    ON DM.physical_name = PD.physical_name  
ORDER BY D.database_id, PD.pdw_node_ID;  
```  
  
### <a name="b-using-syspdw_nodes_pdw_physical_databases-to-gather-detailed-object-information"></a>B. Usando sys. pdw_nodes_pdw_physical_databases para coletar informações detalhadas do objeto  
 A consulta a seguir mostra informações sobre índices e inclui informações úteis sobre o banco de dados que os objetos pertencem a objetos no banco de dados.  
  
```  
SELECT D.name AS UserDatabaseName, D.database_id AS DBIDinMaster,  
DM.physical_name AS PhysDBName, PD.pdw_node_id AS NodeID,   
IU.object_id, IU.index_id, IU.user_seeks, IU.user_scans, IU.user_lookups, IU.user_updates  
FROM sys.databases AS D  
JOIN sys.pdw_database_mappings AS DM  
    ON D.database_id = DM.database_id  
JOIN sys.pdw_nodes_pdw_physical_databases AS PD  
    ON DM.physical_name = PD.physical_name  
JOIN sys.dm_pdw_nodes_db_index_usage_stats AS IU  
    ON PD.database_id = IU.database_id  
ORDER BY D.database_id, IU.object_id, IU.index_id, PD.pdw_node_ID;  
```  
  
### <a name="c-using-syspdw_nodes_pdw_physical_databases-to-determine-the-encryption-state"></a>C. Usando sys. pdw_nodes_pdw_physical_databases para determinar o estado de criptografia  
 A consulta a seguir fornece o estado de criptografia do banco de dados AdventureWorksPDW2012.  
  
```  
WITH dek_encryption_state AS   
(  
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id, encryption_state  
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek  
        INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map  
            ON dek.database_id = node_db_map.database_id AND dek.pdw_node_id = node_db_map.pdw_node_id  
        LEFT JOIN sys.pdw_database_mappings AS db_map  
            ON node_db_map .physical_name = db_map.physical_name  
        INNER JOIN sys.dm_pdw_nodes AS nodes  
            ON nodes.pdw_node_id = dek.pdw_node_id  
    WHERE dek.encryptor_thumbprint <> 0x  
)  
SELECT TOP 1 encryption_state  
       FROM  dek_encryption_state  
       WHERE dek_encryption_state.database_id = DB_ID('AdventureWorksPDW2012 ')  
       ORDER BY (CASE encryption_state WHEN 3 THEN -1 ELSE encryption_state END) DESC;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do catálogo de data warehouse SQL Data Warehouse e paralelas](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [&#41;sys. databases &#40;Transact-SQL](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys. pdw_database_mappings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)  
  
  

