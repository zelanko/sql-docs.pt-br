---
title: sys. trace_events (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trace_events_TSQL
- trace_events
- sys.trace_events
- sys.trace_events_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trace_events catalog view
ms.assetid: e7d2c5df-0e17-4e94-9d41-d36c7ee60662
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 17bf8ff345e2869d6189491cbf09df49312e1f75
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68106659"
---
# <a name="systrace_events-transact-sql"></a>sys.trace_events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A exibição de catálogo **Sys. trace_events** contém uma lista de todos os eventos de rastreamento do SQL. Esses eventos de rastreamento não são diferentes para uma determinada versão do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
> **IMPORTANTE:** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use exibições do catálogo de Eventos Estendidos.  
  
 Para obter mais informações sobre esses eventos de rastreamento, consulte [SQL Server referência de classe de evento](../../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**trace_event_id**|**smallint**|ID exclusiva do evento. Essa coluna também está nas exibições de catálogo **Sys. trace_event_bindings** e **Sys. trace_subclass_values** .|  
|**category_id**|**smallint**|A ID de categoria do evento. Essa coluna também está na exibição de catálogo **Sys. trace_categories** .|  
|**name**|**nvarchar(128)**|Nome exclusivo deste evento. Este parâmetro não é localizado.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Confira também  
 [Exibições de catálogo de objetos &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys. TRACES &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-traces-transact-sql.md)   
 [sys. trace_categories &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-categories-transact-sql.md)   
 [sys. trace_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-columns-transact-sql.md)   
 [sys. trace_event_bindings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-event-bindings-transact-sql.md)   
 [sys. trace_subclass_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-subclass-values-transact-sql.md)  
  
  
