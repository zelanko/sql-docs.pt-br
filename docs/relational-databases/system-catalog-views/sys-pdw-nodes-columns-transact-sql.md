---
title: sys.pdw_nodes_columns (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 268c77b7-1d71-4197-a2ed-5e2b2b8fc260
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3316f6325cda3ad7683337ef4d5929e1e5369fb2
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="syspdwnodescolumns-transact-sql"></a>sys.pdw_nodes_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Mostra as colunas de tabelas definidas pelo usuário e exibições definidas pelo usuário.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**Int**|ID do objeto ao qual esta coluna pertence.||  
|name|**sysname**|Nome da coluna. Exclusiva no objeto.||  
|column_id|**Int**|ID da coluna. Exclusiva no objeto.||  
|system_type_id|**tinyint**|ID de coluna do tipo de sistema.||  
|user_type_id|**Int**|ID do tipo da coluna, como definido pelo usuário.||  
|max_length|**smallint**|Comprimento máximo (em bytes) da coluna.|Inclui -1 (inválido) para tipos de coluna sem suporte.|  
|precisão|**tinyint**|Precisão da coluna se tiver base numérica; Caso contrário, 0.||  
|scale|**tinyint**|Escala da coluna se numérica; caso contrário é 0.||  
|collation_name|**sysname**|Nome do agrupamento da coluna com base em caractere; Caso contrário, nulo.||  
|is_nullable|**bit**|1 = A coluna permite valor nulo.||  
|is_ansi_padded|**bit**|1 = A coluna usa o comportamento ANSI_PADDING ON se for de caractere, binária, ou variante.|Sempre 0.|  
|is_rowguidcol|**bit**|1 = A coluna é uma ROWGUIDCOL declarada.|Sempre 0.|  
|is_identity|**bit**|1 = A coluna tem valores de identidade.|Sempre 0.|  
|is_computed|**bit**|1 = A coluna é computada.|Sempre 0.|  
|is_filestream|**bit**|1 = A coluna é uma coluna de FILESTREAM.|Sempre 0.|  
|is_replicated|**bit**|1 = A coluna é replicada.|Sempre 0.|  
|is_non_sql_subscribed|**bit**|1 = a coluna tem um assinante não-SQL.|Sempre 0.|  
|is_merge_published|**bit**|1 = A coluna é publicada por mesclagem.|Sempre 0.|  
|is_dts_replicated|**bit**|1 = coluna é replicada usando o SSIS.|Sempre 0.|  
|is_xml_document|**bit**|1 = O conteúdo é um documento XML completo.|Sempre 0.|  
|xml_collection_id|**Int**|0 = Nenhuma coleção de esquemas XML.|Sempre 0.|  
|default_object_id|**Int**|ID do objeto padrão; 0 = sem padrão.|Sempre 0.|  
|rule_object_id|**Int**|ID da regra autônoma associada à coluna. <br />0 = Nenhuma regra autônoma.|Sempre 0.|  
|is_sparse|**bit**|1 = A coluna é esparsa.|Sempre 0.|  
|is_column_set|**bit**|1 = A coluna é um conjunto de colunas.|Sempre 0.|  
|pdw_node_id|**Int**|Identificador exclusivo de um [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nó.|NOT NULL|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL SERVER.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e exibições de catálogo do Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys.all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)  
  
  
