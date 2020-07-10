---
title: sys. pdw_nodes_column_store_segments (Transact-SQL)
ms.custom: seo-dt-2019
ms.date: 03/28/2018
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: e2fdf8e9-1b74-4682-b2d4-c62aca053d7f
author: julieMSFT
ms.author: jrasnick
manager: jrj
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: fc1e04718ea9db16d3b0c2a1cc59b14f906c6f31
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86197188"
---
# <a name="syspdw_nodes_column_store_segments-transact-sql"></a>sys. pdw_nodes_column_store_segments (Transact-SQL)

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

Contém uma linha para cada coluna em um índice columnstore.

| Nome da coluna                 | Tipo de dados  | Descrição                                                  |
| :-------------------------- | :--------- | :----------------------------------------------------------- |
| **partition_id**            | **bigint** | Indica a ID da partição. É exclusivo em um banco de dados.     |
| **hobt_id**                 | **bigint** | A ID do heap ou o índice de árvore B (hobt) para a tabela que tem seu índice columnstore. |
| **column_id**               | **int**    | ID da coluna columnstore.                                |
| **segment_id**              | **int**    | ID do segmento de coluna. Para compatibilidade com versões anteriores, o nome da coluna continua sendo chamado segment_id embora seja a ID do rowgroup. Você pode identificar exclusivamente um segmento usando <hobt_id, partition_id, column_id>, <segment_id>. |
| **version**                 | **int**    | Versão de formato do segmento de coluna.                        |
| **encoding_type**           | **int**    | Tipo de codificação usado para esse segmento:<br /><br /> 1 = VALUE_BASED-não cadeia de caracteres/binário sem dicionário (semelhante a 4 com algumas variações internas)<br /><br /> 2 = VALUE_HASH_BASED-coluna não cadeia de caracteres/binária com valores comuns no dicionário<br /><br /> 3 = STRING_HASH_BASED-cadeia de caracteres/coluna binária com valores comuns no dicionário<br /><br /> 4 = STORE_BY_VALUE_BASED-não cadeia de caracteres/binário sem dicionário<br /><br /> 5 = STRING_STORE_BY_VALUE_BASED-cadeia de caracteres/binário sem dicionário<br /><br /> Todas as codificações aproveitam a codificação de bits e de tamanho de execução quando possível. |
| **row_count**               | **int**    | Número de linhas no grupo de linhas.                             |
| **has_nulls**               | **int**    | 1 se o segmento de coluna tiver valores nulos.                     |
| **base_id**                 | **bigint** | ID do valor de base se o tipo de codificação 1 estiver sendo usado.  Se o tipo de codificação 1 não estiver sendo usado, base_id será definido como 1. |
| **magnitude**               | **float**  | Magnitude se o tipo de codificação 1 estiver sendo usado.  Se o tipo de codificação 1 não estiver sendo usado, a magnitude será definida como 1. |
| **primary__dictionary_id**  | **int**    | ID do dicionário principal. Um valor diferente de zero aponta para o dicionário local para esta coluna no segmento atual (ou seja, o rowgroup). Um valor de-1 indica que não há nenhum dicionário local para este segmento. |
| **secondary_dictionary_id** | **int**    | ID do dicionário secundário. Um valor diferente de zero aponta para o dicionário local para esta coluna no segmento atual (ou seja, o rowgroup). Um valor de-1 indica que não há nenhum dicionário local para este segmento. |
| **min_data_id**             | **bigint** | A ID de dados mínima no segmento de coluna.                       |
| **max_data_id**             | **bigint** | ID de dados máximo no segmento de coluna.                       |
| **null_value**              | **bigint** | Valor usado para representar nulos.                               |
| **on_disk_size**            | **bigint** | Tamanho do segmento em bytes.                                    |
| **pdw_node_id**             | **int**    | Identificador exclusivo de um [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nó. |
| &nbsp; | &nbsp; | &nbsp; |

## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

Ingresse em sys. pdw_nodes_column_store_segments com outras tabelas do sistema para determinar o número de segmentos columnstore por tabela lógica.

```sql
SELECT  sm.name           as schema_nm
,       tb.name           as table_nm
,       nc.name           as col_nm
,       nc.column_id
,       COUNT(*)          as segment_count
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb                   ON  sm.[schema_id]          = tb.[schema_id]
JOIN    sys.[pdw_table_mappings] mp       ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt         ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[pdw_nodes_partitions] np     ON  np.[object_id]          = nt.[object_id]
                                          AND np.[pdw_node_id]        = nt.[pdw_node_id]
                                          AND np.[distribution_id]    = nt.[distribution_id]
JOIN    sys.[pdw_nodes_columns] nc        ON  np.[object_id]          = nc.[object_id]
                                          AND np.[pdw_node_id]        = nc.[pdw_node_id]
                                          AND np.[distribution_id]    = nc.[distribution_id]
JOIN    sys.[pdw_nodes_column_store_segments] rg  ON  rg.[partition_id]         = np.[partition_id]
                                                      AND rg.[pdw_node_id]      = np.[pdw_node_id]
                                                      AND rg.[distribution_id]  = np.[distribution_id]
                                                      AND rg.[column_id]        = nc.[column_id]
GROUP BY    sm.name
,           tb.name
,           nc.name
,           nc.column_id  
ORDER BY    table_nm
,           nc.column_id
,           sm.name ;
```

## <a name="permissions"></a>Permissões

Requer a permissão **VIEW SERVER STATE**.

## <a name="see-also"></a>Consulte Também

[Exibições de Catálogo do SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
[CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)  
[sys. pdw_nodes_column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)  
[sys. pdw_nodes_column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)
