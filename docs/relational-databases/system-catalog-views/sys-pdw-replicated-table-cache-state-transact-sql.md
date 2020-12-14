---
description: sys.pdw_replicated_table_cache_state (Transact-SQL)
title: sys.pdw_replicated_table_cache_state (Transact-SQL)
ms.custom: seo-dt-2019
ms.date: 07/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
monikerRange: = azure-sqldw-latest
ms.openlocfilehash: 76b5f9ec684b4733934a8cdd703942f12cf1b541
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97404424"
---
# <a name="syspdw_replicated_table_cache_state-transact-sql"></a>sys.pdw_replicated_table_cache_state (Transact-SQL)
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

  Retorna o estado do cache associado a uma tabela replicada por **object_id**.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|A ID de objeto da tabela. Consulte [Sys. objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).<br /><br /> **object_id** é a chave para essa exibição.||  
|state|**nvarchar(40)**|O estado do cache da tabela replicada para esta tabela.|' Não lido ', ' pronto '|  
  
## <a name="example"></a>Exemplo
Este exemplo une sys.pdw_replicated_table_cache_state com sys. Tables para recuperar o nome da tabela e o estado do cache da tabela replicada.

```sql
SELECT t.[name], p.[object_id], p.[state]
  FROM sys.pdw_replicated_table_cache_state p 
  JOIN sys.tables t ON t.object_id = p.object_id
```



## <a name="next-steps"></a>Próximas etapas  
 Para obter uma lista de todas as exibições de catálogo para o Azure Synapse Analytics e Parallel data warehouse, consulte [Azure Synapse Analytics e exibições do catálogo de data warehouse paralela](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md).   
  
