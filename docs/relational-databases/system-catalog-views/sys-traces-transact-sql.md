---
title: Traces (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- traces
- sys.traces_TSQL
- sys.traces
- traces_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.traces catalog view
ms.assetid: 4a03be22-b7da-4e2a-97ff-94bed890a620
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8cabef6e979c613c977d7e5636f46a10b447fbbe
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37981522"
---
# <a name="systraces-transact-sql"></a>sys.traces (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **Traces** exibição do catálogo contém os rastreamentos em execução atuais no sistema. Essa exibição foi planejada como uma substituição para o **fn_trace_getinfo** função.  
  
 Para obter uma lista completa de eventos de rastreamento com suporte, consulte [SQL Server Event Class Reference](../../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use exibições do catálogo de Eventos Estendidos.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID do rastreamento.|  
|**status**|**int**|Status do rastreamento:<br /><br /> 0 = parado<br /><br /> 1 = em execução|  
|**path**|**nvarchar(260)**|Caminho do arquivo de rastreamento. Este valor será nulo quando o rastreamento for referente a um conjunto de linhas.|  
|**max_size**|**bigint**|Limite máximo do tamanho do arquivo de rastreamento em megabytes (MB). Este valor será nulo quando o rastreamento for referente a um conjunto de linhas.|  
|**stop_time**|**datetime**|Hora em que o rastreamento em execução será parado.|  
|**max_files**|**int**|Número máximo de arquivos de substituição. Este valor será nulo se o número máximo não for definido.|  
|**is_rowset**|**bit**|1 = rastreamento de conjunto de linhas.|  
|**is_rollover**|**bit**|1 = a opção de substituição está habilitada.|  
|**is_shutdown**|**bit**|1 = a opção de desligamento está habilitada.|  
|**is_default**|**bit**|1 = rastreamento padrão.|  
|**buffer_count**|**int**|Número de buffers em memória usados pelo rastreamento.|  
|**buffer_size**|**int**|Tamanho de cada buffer (KB).|  
|**file_position**|**bigint**|Última posição do arquivo de rastreamento. Este valor será nulo quando o rastreamento for referente a um conjunto de linhas.|  
|**reader_spid**|**int**|ID da sessão do leitor do rastreamento de conjunto de linhas. Esse valor será nulo quando o rastreamento for referente a um arquivo.|  
|**start_time**|**datetime**|Hora de início do rastreamento.|  
|**last_event_time**|**datetime**|Hora em que o último evento foi acionado.|  
|**event_count**|**bigint**|Número total de eventos ocorridos.|  
|**dropped_event_count**|**int**|Número total de eventos descartados.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys.trace_categories &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-categories-transact-sql.md)   
 [sys.trace_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-columns-transact-sql.md)   
 [sys.trace_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-events-transact-sql.md)   
 [sys.trace_event_bindings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-event-bindings-transact-sql.md)   
 [sys.trace_subclass_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-subclass-values-transact-sql.md)  
  
  
