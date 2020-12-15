---
description: sys.pdw_database_mappings (Transact-SQL)
title: sys.pdw_database_mappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 4ae2c71e-dd56-41ea-a16b-64936175b459
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: 8c93497ad0fd1c51a5422b80c835f3dbc8f1aff7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477367"
---
# <a name="syspdw_database_mappings-transact-sql"></a>sys.pdw_database_mappings (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Mapeia o **database_id** s de bancos de dados para o nome físico usado em nós de computação e fornece a **ID da entidade de segurança** do proprietário do banco de dados no sistema. Ingresse **Sys.pdw_database_mappings** em **Sys. databases** e **Sys.pdw_nodes_pdw_physical_databases**.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|physical_name|**nvarchar (36)**|O nome físico do banco de dados nos nós de computação.<br /><br /> **physical_name** e **database_id** formate a chave para essa exibição.||  
|database_id|**int**|A ID de objeto do banco de dados. Consulte [Sys. databases &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).<br /><br /> **physical_name** e **database_id** formate a chave para essa exibição.||  
  
## <a name="examples-sspdw"></a>Exemplos: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir une sys.pdw_database_mappings a outras tabelas do sistema para mostrar como os bancos de dados são mapeados.  
  
```  
SELECT DB.database_id, DB.name, Map.*, Phys.*   
FROM sys.databases AS DB  
JOIN sys.pdw_database_mappings AS Map  
    ON DB.database_id = Map.database_id  
JOIN sys.pdw_nodes_pdw_physical_databases AS Phys  
    ON Map.physical_name = Phys.physical_name  
ORDER BY DB.database_id, Phys.pdw_node_id;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de Catálogo do Azure Synapse Analytics e do Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [&#41;&#40;Transact-SQL de sys.pdw_index_mappings ](../../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.pdw_table_mappings ](../../relational-databases/system-catalog-views/sys-pdw-table-mappings-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.pdw_nodes_pdw_physical_databases ](../../relational-databases/system-catalog-views/sys-pdw-nodes-pdw-physical-databases-transact-sql.md)  
  
  

