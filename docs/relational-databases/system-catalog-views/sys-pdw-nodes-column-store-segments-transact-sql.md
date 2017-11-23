---
title: sys.pdw_nodes_column_store_segments (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: e2fdf8e9-1b74-4682-b2d4-c62aca053d7f
caps.latest.revision: "9"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 79944f54d12681ab7a430362ec0204a8d54bf477
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwnodescolumnstoresegments-transact-sql"></a>sys.pdw_nodes_column_store_segments (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém uma linha para cada coluna em um índice columnstore.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|Indica a ID da partição. É exclusivo em um banco de dados.|  
|**hobt_id**|**bigint**|A ID do heap ou o índice de árvore B (hobt) para a tabela que tem seu índice columnstore.|  
|**column_id**|**int**|ID da coluna columnstore.|  
|**segment_id**|**int**|ID do segmento de coluna.|  
|**version**|**int**|Versão de formato do segmento de coluna.|  
|**encoding_type**|**int**|Tipo de codificação usada para esse segmento.|  
|**row_count**|**int**|Número de linhas no grupo de linhas.|  
|**has_nulls**|**int**|1 se o segmento de coluna tiver valores nulos.|  
|**base_id**|**bigint**|Id do valor base se tipo de codificação 1 estiver sendo usado.  Se o tipo de codificação 1 não está sendo usado, base_id será definido como 1.|  
|**magnitude**|**float**|Magnitude se o tipo de codificação 1 estiver sendo usado.  Se o tipo de codificação 1 não está sendo usado, magnitude é definido como 1.|  
|**primary__dictionary_id**|**int**|ID do dicionário primário.|  
|**secondary_dictionary_id**|**int**|ID do dicionário secundário. Retornará -1 se não houver um dicionário secundário.|  
|**min_data_id**|**bigint**|Id de dados mínimo no segmento de coluna.|  
|**max_data_id**|**bigint**|Id de dados máximo no segmento de coluna.|  
|**null_value**|**bigint**|Valor usado para representar nulos.|  
|**on_disk_size**|**bigint**|Tamanho do segmento em bytes.|  
|**pdw_node_id**|**int**|Identificador exclusivo de um [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Observação.|  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 A consulta a seguir retorna informações sobre segmentos de um índice columnstore.  
  
```tsql  
SELECT i.name, p.object_id, p.index_id, i.type_desc,   
    COUNT(*) AS number_of_segments  
FROM sys.column_store_segments AS s   
INNER JOIN sys.partitions AS p   
    ON s.hobt_id = p.hobt_id   
INNER JOIN sys.indexes AS i   
    ON p.object_id = i.object_id  
WHERE i.type = 6  
GROUP BY i.name, p.object_id, p.index_id, i.type_desc ;  
```  
  
 Una sys.pdw_nodes_column_store_segments com outras tabelas do sistema para determinar a contagem de linhas e o tamanho dos segmentos no disco.  
  
```  
SELECT o.name, css.hobt_id, css. column_id, css.pdw_node_id, css.row_count, css.on_disk_size  
FROM sys.pdw_nodes_column_store_segments AS css  
JOIN sys.pdw_nodes_partitions AS pnp  
    ON css.partition_id = pnp.partition_id  
JOIN sys.pdw_nodes_tables AS part  
    ON pnp.object_id = part.object_id   
    AND pnp.pdw_node_id = part.pdw_node_id  
JOIN sys.pdw_table_mappings AS TMap  
    ON part.name = TMap.physical_name  
JOIN sys.objects AS o  
    ON TMap.object_id = o.object_id  
ORDER BY css.hobt_id, css.column_id;  
```  
  
## <a name="permissions"></a>Permissões  
 Requer **VIEW SERVER STATE** permissão.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e exibições de catálogo do Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [Criar índice COLUMNSTORE &#40; Transact-SQL &#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [sys.pdw_nodes_column_store_row_groups &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)   
 [sys.pdw_nodes_column_store_dictionaries &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)  
  
  

