---
title: sys.pdw_nodes_indexes (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
ms.assetid: 261bcb7f-a906-4979-b274-bc5f1aa66426
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a9dcf0c5cc21d01359c13f13b33914d73a0a7b5f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwnodesindexes-transact-sql"></a>sys.pdw_nodes_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Retorna os índices para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|ID do objeto ao qual este índice pertence.||  
|name|**sysname**|Nome do índice. Nome é exclusivo somente dentro do objeto. NULL = Heap||  
|index_id|**int**|ID do índice. index_id só é exclusivo dentro do objeto.<br /><br /> 0 = Heap<br /><br /> 1 = Índice clusterizado<br /><br /> > 1 = índice não clusterizado||  
|Tipo|**tinyint**|Tipo de índice:<br /><br /> 0 = Heap<br /><br /> 1 = Clusterizado<br /><br /> 2 = não clusterizado<br /><br /> 5 = índice clusterizado xVelocity de columnstore otimizado de memória|  
|type_desc|**nvarchar (60)**|Descrição de tipo de índice:<br /><br /> HEAP<br /><br /> CLUSTERED<br /><br /> NONCLUSTERED<br /><br /> COLUMNSTORE CLUSTERIZADO||  
|is_unique|**bit**|0 = O índice não é exclusivo.|Sempre 0.|  
|data_space_id|**int**|ID do espaço de dados para este índice. O espaço de dados é um grupo de arquivos ou um esquema de partição.<br /><br /> 0 = object_id é uma função com valor de tabela.||  
|ignore_dup_key|**bit**|0 = IGNORE_DUP_KEY está OFF.|Sempre 0.|  
|is_primary_key|**bit**|1 = O índice faz parte de uma restrição PRIMARY KEY.|Sempre 0.|  
|is_unique_constraint|**bit**|1 = O índice faz parte de uma restrição UNIQUE.|Sempre 0.|  
|fill_factor|**tinyint**|>0 = Porcentagem de FILLFACTOR usada quando o índice foi criado ou reconstruído.<br /><br /> 0 = Valor padrão|Sempre 0.|  
|is_padded|**bit**|0 = PADINDEX está OFF.|Sempre 0.|  
|is_disabled|**bit**|1 = O índice está desabilitado.<br /><br /> 0 = O índice não está desabilitado.||  
|is_hypothetical|**bit**|0 = O índice não é hipotético.|Sempre 0.|  
|allow_row_locks|**bit**|1 = O índice permite bloqueios de linha.|Sempre 1.|  
|allow_page_locks|**bit**|1 = O índice permite bloqueios de página.|Sempre 1.|  
|has_filter|**bit**|0 = O índice não tem um filtro.|Sempre 0.|  
|filter_definition|**nvarchar(max)**|Expressão do subconjunto de linhas incluído no índice filtrado.|Sempre NULL.|  
|pdw_node_id|**int**|Identificador exclusivo de um [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nó.|NOT NULL|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL SERVER.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e exibições de catálogo do Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
