---
title: sys.pdw_replicated_table_cache_state (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 9d3d2880c390dc627db7009662f72ccec6e9700f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33179542"
---
# <a name="syspdwreplicatedtablecachestate-transact-sql"></a>sys.pdw_replicated_table_cache_state (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  Retorna o estado do cache associado a uma tabela replicada por **object_id**.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**Int**|A ID de objeto para a tabela. Consulte [sys. Objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).<br /><br /> **object_id** é a chave para este modo de exibição.||  
|state|**nvarchar(40)**|O estado do cache de tabela replicada para essa tabela.|'NotReady', 'Pronto'|  
  
## <a name="example"></a>Exemplo
Este exemplo une sys.pdw_replicated_table_cache_state com Sys. Tables para recuperar o nome da tabela e o estado do cache de tabela replicada.

```sql
SELECT t.[name], p.[object_id], p.[state]
  FROM sys.pdw_replicated_table_cache_state p 
  JOIN sys.tables t ON t.object_id = p.object_id
```



## <a name="next-steps"></a>Próximas etapas  
 Para obter uma lista de todas as exibições de catálogo para o SQL Data Warehouse e o Parallel Data Warehouse, consulte [SQL Data Warehouse e exibições do catálogo Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md).   
  
