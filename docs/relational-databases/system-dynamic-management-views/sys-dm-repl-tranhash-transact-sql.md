---
description: sys.dm_repl_tranhash (Transact-SQL)
title: sys. dm_repl_tranhash (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_repl_tranhash
- sys.dm_repl_tranhash_TSQL
- dm_repl_tranhash_TSQL
- dm_repl_tranhash
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_repl_tranhash dynamic management view
ms.assetid: 0cc52338-e805-4ed4-9835-b19bbf72448e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 35bb540ff2b73a44de324a51937552ae7cc3ec56
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536876"
---
# <a name="sysdm_repl_tranhash-transact-sql"></a>sys.dm_repl_tranhash (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações sobre transações sendo replicadas em uma publicação transacional.  
  
|column_name|data_type|description|  
|------------------|----------------|-----------------|  
|**buckets**|**bigint**|Número de partições de memória na tabela hash.|  
|**hashed_trans**|**bigint**|Número de transações confirmadas replicadas no lote atual.|  
|**completed_trans**|**bigint**|Número de transações disputadas até o momento.|  
|**compensated_trans**|**bigint**|Número de transações que contêm reversões parciais.|  
|**first_begin_lsn**|**nvarchar (64)**|Número de sequência de log de início mais antigo (LSN) no lote atual.|  
|**last_commit_lsn**|**nvarchar (64)**|Último LSN de confirmação no lote atual.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE no banco de dados de publicação para chamar **dm_repl_tranhash**.  
  
## <a name="remarks"></a>Comentários  
 As informações só serão retornadas para objetos de banco de dados replicados atualmente armazenados no cache de artigo de replicação.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas à replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)  
  
  
