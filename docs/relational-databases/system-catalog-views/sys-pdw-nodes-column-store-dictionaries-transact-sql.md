---
title: sys.pdw_nodes_column_store_dictionaries (Transact-SQL) | Microsoft Docs
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.custom: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 7ae1c2e4-45c0-4880-a692-1f299fbcfd19
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 618a92cfd0f1602753b9fcfd61ac232eff5cecd4
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305188"
---
# <a name="syspdw_nodes_column_store_dictionaries-transact-sql"></a>sys.pdw_nodes_column_store_dictionaries (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém uma linha para cada dicionário usado em índices columnstore. Dicionários são usados para codificar alguns, mas não todos os tipos de dados; portanto, nem todas as colunas em um índice columnstore têm dicionários. Um dicionário pode existir como um dicionário primário (para todos os segmentos) e, possivelmente, para outros dicionários secundários usados para um subconjunto de segmentos da coluna.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|Indica a ID da partição. É exclusivo em um banco de dados.|  
|**hobt_id**|**bigint**|ID do índice de heap ou árvore B (HoBT) para a tabela que tem este índice columnstore.|  
|**column_id**|**int**|ID da coluna columnstore.|  
|**dictionary_id**|**int**|ID do dicionário.|  
|**version**|**int**|Versão de formato do dicionário.|  
|**tipo**|**int**|Tipo de dicionário:<br /><br /> 1-dicionário de hash contendo valores **int**<br /><br /> 2-não usado<br /><br /> 3-dicionário de hash contendo valores de cadeia de caracteres<br /><br /> 4-dicionário de hash que contém valores **float**|  
|**last_id**|**int**|O último id de dados no dicionário.|  
|**entry_count**|**bigint**|Número de entradas no dicionário.|  
|**on_disc_size**|**bigint**|Tamanho do dicionário em bytes.|  
|**pdw_node_id**|**int**|Identificador exclusivo de um nó de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `VIEW SERVER STATE`.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de Catálogo do SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [sys.pdw_nodes_column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-segments-transact-sql.md)   
 [sys.pdw_nodes_column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)  
  
  
