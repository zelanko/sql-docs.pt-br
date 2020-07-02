---
title: sys. internal_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.internal_tables
- internal_tables
- sys.internal_tables_TSQL
- internal_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- internal tables
- sys.internal_tables catalog view
ms.assetid: a5821c70-f150-4676-8476-3a31f7403dca
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: bf1406488424febe0ea98a686b91068fe2d07eda
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85725773"
---
# <a name="sysinternal_tables-transact-sql"></a>sys.internal_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha para cada objeto que é uma tabela interna. As tabelas internas são geradas automaticamente por meio do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para oferecer suporte a vários recursos. Por exemplo, quando você cria um índice XML primário, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria automaticamente uma tabela interna para manter os dados fragmentados do documento XML. As tabelas internas aparecem no esquema **Sys** de cada banco de dados e têm nomes exclusivos, gerados pelo sistema, que indicam sua função, por exemplo, **xml_index_nodes_2021582240_32001** ou **queue_messages_1977058079**  
  
 As tabelas internas não contêm dados acessíveis ao usuário, e seus esquemas são fixos e inalteráveis. Você não pode fazer referências a nomes de tabelas internas em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. Por exemplo, você não pode executar uma instrução como SELECT \* from *\<sys.internal_table_name>* . Entretanto, você pode consultar as exibições do catálogo para ver os metadados das tabelas internas.   
  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**\<Columns inherited from sys.objects>**||Para obter uma lista de colunas que essa exibição herda, consulte [Sys. objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**internal_type**|**tinyint**|Tipo da tabela interna:<br /><br /> 3 = **query_disk_store_query_hints**<br /><br /> 4 = **query_disk_store_query_template_parameterization**<br /><br /> 6 = **query_disk_store_wait_stats**<br /><br /> 201 = **queue_messages**<br /><br /> 202 = **xml_index_nodes**<br /><br /> 203 = **fulltext_catalog_freelist**<br /><br /> 205 = **query_notification**<br /><br /> 206 = **service_broker_map**<br /><br /> 207 = **extended_indexes** (como um índice espacial)<br /><br /> 208 = **filestream_tombstone**<br /><br /> 209 = **CHANGE_TRACKING**<br /><br /> 210 = **tracked_committed_transactions**<br /><br /> 220 = **contained_features**<br /><br /> 225 = **filetable_updates**<br /><br /> 236 = **selective_xml_index_node_table**<br /><br /> 240 = **query_disk_store_query_text**<br /><br /> 241 = **query_disk_store_query**<br /><br /> 242 = **query_disk_store_plan**<br /><br /> 243 = **query_disk_store_runtime_stats**<br /><br /> 244 = **query_disk_store_runtime_stats_interval**<br /><br /> 245 = **query_context_settings**|  
|**internal_type_desc**|**nvarchar(60)**|Descrição do tipo de tabela interna:<br /><br /> QUERY_DISK_STORE_QUERY_HINTS<br /><br /> QUERY_DISK_STORE_QUERY_TEMPLATE_PARAMETERIZATION<br /><br /> QUERY_DISK_STORE_WAIT_STATS<br /><br /> QUEUE_MESSAGES<br /><br /> XML_INDEX_NODES<br /><br /> FULLTEXT_CATALOG_FREELIST<br /><br /> FULLTEXT_CATALOG_MAP<br /><br /> QUERY_NOTIFICATION<br /><br /> SERVICE_BROKER_MAP<br /><br /> EXTENDED_INDEXES<br /><br /> FILESTREAM_TOMBSTONE<br /><br /> CHANGE_TRACKING<br /><br /> TRACKED_COMMITTED_TRANSACTIONS<br /><br /> CONTAINED_FEATURES<br /><br /> FILETABLE_UPDATES<br /><br /> SELECTIVE_XML_INDEX_NODE_TABLE<br /><br /> QUERY_DISK_STORE_QUERY_TEXT<br /><br /> QUERY_DISK_STORE_QUERY<br /><br /> QUERY_DISK_STORE_PLAN<br /><br /> QUERY_DISK_STORE_RUNTIME_STATS<br /><br /> QUERY_DISK_STORE_RUNTIME_STATS_INTERVAL<br /><br /> QUERY_CONTEXT_SETTINGS|  
|**parent_id**|**int**|ID do pai, independentemente de ser um escopo de esquema ou não. Caso contrário, 0 se não houver nenhum pai.<br /><br /> **queue_messages**  =  **object_id** da fila<br /><br /> **xml_index_nodes**  =  **object_id** do índice XML<br /><br /> **fulltext_catalog_freelist**  =  **fulltext_catalog_id** do catálogo de texto completo<br /><br /> **fulltext_index_map**  =  **object_id** do índice de texto completo<br /><br /> **query_notification**ou **service_broker_map** = 0<br /><br /> **extended_indexes**  =  **object_id** de um índice estendido, como um índice espacial<br /><br /> **object_id** da tabela para a qual o rastreamento de tabela está habilitado = **CHANGE_TRACKING**|  
|**parent_minor_id**|**int**|ID secundária do pai.<br /><br /> **xml_index_nodes**  =  **index_id** do índice XML<br /><br /> **extended_indexes**  =  **index_id** de um índice estendido, como um índice espacial<br /><br /> 0 = **queue_messages**, **fulltext_catalog_freelist**, **fulltext_index_map**, **query_notification**, **service_broker_map**ou **CHANGE_TRACKING**|  
|**lob_data_space_id**|**int**|O valor diferente de zero é a ID do espaço de dados (esquema de partição ou grupo de arquivos) que armazena os dados de objeto grandes (LOB) dessa tabela.|  
|**filestream_data_space_id**|**int**|Reservado para uso futuro.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Comentários  
 Tabelas internas são colocadas no mesmo grupo de arquivos da entidade de pai. Você pode usar a consulta de catálogo mostrada no Exemplo F abaixo para retornar o número de páginas que as tabelas internas consomem para dados de dentro da linha, fora da linha, e de objetos grandes (LOB).  
  
 Você pode usar o procedimento do sistema [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) para retornar dados de uso de espaço para tabelas internas. **sp_spaceused** relata o espaço de tabela interna das seguintes maneiras:  
  
-   Quando um nome de fila é especificado, a tabela interna subjacente associada à fila é referenciada, e seu consumo de armazenamento é reportado.  
  
-   As páginas usadas pelas tabelas internas de índices XML, índices espaciais e índices de texto completo são incluídas na coluna **index_size** . Quando um nome de tabela ou exibição indexada é especificado, as páginas dos índices XML, dos índices espaciais e dos índices de texto completo desse objeto são incluídas nas colunas **reservadas** e **index_size**.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos seguintes demonstram como consultar metadados de tabela interna usando as exibições do catálogo.  
  
### <a name="a-show-internal-tables-that-inherit-columns-from-the-sysobjects-catalog-view"></a>a. Mostrar tabelas internas que herdam colunas da exibição do catálogo sys.objects  
  
```  
SELECT * FROM sys.objects WHERE type = 'IT';  
```  
  
### <a name="b-return-all-internal-table-metadata-including-that-which-is-inherited-from-sysobjects"></a>B. Retorna todos os metadados de tabela interna (inclusive os herdados de sys.objects)  
  
```  
SELECT * FROM sys.internal_tables;  
```  
  
### <a name="c-return-internal-table-columns-and-column-data-types"></a>C. Retorna as colunas de tabela interna e os tipos de dados da coluna  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    ,itab.name AS internal_table_name  
    ,typ.name AS column_data_type   
    ,col.*  
FROM sys.internal_tables AS itab  
JOIN sys.columns AS col ON itab.object_id = col.object_id  
JOIN sys.types AS typ ON typ.user_type_id = col.user_type_id  
ORDER BY itab.name, col.column_id;  
```  
  
### <a name="d-return-internal-table-indexes"></a>D. Retorna os índices de tabela interna  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    , itab.name AS internal_table_name  
    , idx.*  
FROM sys.internal_tables AS itab  
JOIN sys.indexes AS idx ON itab.object_id = idx.object_id  
ORDER BY itab.name, idx.index_id;  
```  
  
### <a name="e-return-internal-table-statistics"></a>E. Retorna as estatísticas da tabela interna  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    ,itab.name AS internal_table_name  
    , s.*  
FROM sys.internal_tables AS itab  
JOIN sys.stats AS s ON itab.object_id = s.object_id  
ORDER BY itab.name, s.stats_id;  
```  
  
### <a name="f-return-internal-table-partition-and-allocation-unit-information"></a>F. Retorna a partição da tabela interna e informações da unidade de alocação  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    ,itab.name AS internal_table_name  
    ,idx.name AS heap_or_index_name  
    ,p.*  
    ,au.*  
FROM sys.internal_tables AS itab  
JOIN sys.indexes AS idx  
--     JOIN to the heap or the clustered index  
    ON itab.object_id = idx.object_id AND idx.index_id IN (0,1)  
JOIN   sys.partitions AS p   
    ON p.object_id = idx.object_id AND p.index_id = idx.index_id  
JOIN   sys.allocation_units AS au  
--     IN_ROW_DATA (type 1) and ROW_OVERFLOW_DATA (type 3) => JOIN to partition's Hobt  
--     else LOB_DATA (type 2) => JOIN to the partition ID itself.  
ON au.container_id =    
    CASE au.type   
        WHEN 2 THEN p.partition_id   
        ELSE p.hobt_id   
    END  
ORDER BY itab.name, idx.index_id;  
```  
  
### <a name="g-return-internal-table-metadata-for-xml-indexes"></a>G. Retorna os metadados da tabela interna para os índices XML  
  
```  
SELECT t.name AS parent_table  
    ,t.object_id AS parent_table_id  
    ,it.name AS internal_table_name  
    ,it.object_id AS internal_table_id  
    ,xi.name AS primary_XML_index_name  
    ,xi.index_id as primary_XML_index_id  
FROM sys.internal_tables AS it  
JOIN sys.tables AS t   
    ON it.parent_id = t.object_id  
JOIN sys.xml_indexes AS xi   
    ON it.parent_id = xi.object_id  
    AND it.parent_minor_id  = xi.index_id  
WHERE it.internal_type_desc = 'XML_INDEX_NODES';  
GO  
```  
  
### <a name="h-return-internal-table-metadata-for-service-broker-queues"></a>H. Retorna os metadados da tabela interna para as filas do Service Broker  
  
```  
SELECT q.name AS queue_name  
    ,q.object_id AS queue_id  
    ,it.name AS internal_table_name  
    ,it.object_id AS internal_table_id  
FROM sys.internal_tables AS it  
JOIN sys.service_queues  AS  q ON it.parent_id = q.object_id  
WHERE it.internal_type_desc = 'QUEUE_MESSAGES';  
GO  
```  
  
## <a name="i-return-internal-table-metadata-for-all-service-broker-services"></a>I. Retorna os metadados de tabela interna para todos os serviços do Service Broker  
  
```  
SELECT *   
FROM tempdb.sys.internal_tables   
WHERE internal_type_desc = 'SERVICE_BROKER_MAP';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
