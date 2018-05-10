---
title: xe_sessions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_xe_sessions_TSQL
- dm_xe_sessions
- sys.dm_xe_sessions_TSQL
- sys.dm_xe_sessions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_sessions dynamic management view
- extended events [SQL Server], views
ms.assetid: defd6efb-9507-4247-a91f-dc6ff5841e17
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d7d8f7e1d66290aba8fbbebeb0306d308e1171be
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmxesessions-transact-sql"></a>sys.dm_xe_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre uma sessão de eventos estendida ativa. Esta sessão é uma coleção de eventos, ações e destinos.  
    
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|address|**varbinary(8)**|O endereço da memória da sessão. endereço é exclusivo em todo o sistema local. Não permite valor nulo.|  
|nome|**nvarchar(256)**|O nome da sessão. nome é exclusivo em todo o sistema local. Não permite valor nulo.|  
|pending_buffers|**Int**|O número de buffers cheios que são processamento pendente. Não permite valor nulo.|  
|total_regular_buffers|**Int**|O número total de buffers normais associados à sessão. Não permite valor nulo.<br /><br /> Observação: Os buffers normais são usados na maioria das vezes. Esses buffers não têm tamanho suficiente para manter muitos eventos. Normalmente, há três ou mais buffers por sessão. O número de buffers normais é determinado automaticamente pelo servidor, baseado no particionamento de memória definido por meio da opção MEMORY_PARTITION_MODE. O tamanho dos buffers normais é igual ao valor da opção MAX_MEMORY (padrão de 4 MB), dividido pelo número de buffers. Para obter mais informações sobre o MEMORY_PARTITION_MODE e MAX_MEMORY opções, consulte [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md).|  
|regular_buffer_size|**bigint**|O tamanho do buffer normal, em bytes. Não permite valor nulo.|  
|total_large_buffers|**Int**|O número total de buffers grandes. Não permite valor nulo.<br /><br /> Observação: Os buffers grandes são usadas quando um evento é maior do que um buffer normal. Eles são definidos à parte explicitamente para esse fim. Buffers grandes são alocados quando a sessão de evento é iniciada e são dimensionados de acordo com a opção MAX_EVENT_SIZE. Para obter mais informações sobre a opção MAX_EVENT_SIZE, consulte [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md).|  
|large_buffer_size|**bigint**|O tamanho do buffer grande, em bytes. Não permite valor nulo.|  
|total_buffer_size|**bigint**|O tamanho total do buffer de memória usado para armazenar eventos da sessão, em bytes. Não permite valor nulo.|  
|buffer_policy_flags|**Int**|Um bitmap que indica como os buffers de evento de sessão se comportam quando todos os buffers estão cheios e um evento novo é acionado. Não permite valor nulo.|  
|buffer_policy_desc|**nvarchar(256)**|Uma descrição que indica como os buffers de evento de sessão se comportam quando todos os buffers estão cheios e um evento novo é acionado.  Não permite valor nulo. buffer_policy_desc pode ser um dos seguintes:<br /><br /> Descartar evento<br /><br /> Não descartar eventos<br /><br /> Descartar buffer cheio<br /><br /> Alocar buffer novo|  
|sinalizadores|**Int**|Um bitmap que indica sinalizadores que foram configurados na sessão. Não permite valor nulo.|  
|flag_desc|**nvarchar(256)**|Uma descrição do conjunto de sinalizadores na sessão.  Não permite valor nulo. flag_desc pode ser qualquer combinação das seguintes opções:<br /><br /> Liberar buffers ao fechar<br /><br /> Despachante dedicado<br /><br /> Permitir eventos recursivos|  
|dropped_event_count|**Int**|O número de eventos que foram descartados quando os buffers estavam cheios. Esse valor é **0** se a política de buffer for "Descartar buffer cheio" ou "Não descartar eventos". Não permite valor nulo.|  
|dropped_buffer_count|**Int**|O número de buffers que foram descartados quando os buffers estavam cheios. Esse valor é **0** se a política de buffer é definida como "Descartar evento" ou "Não descartar eventos". Não permite valor nulo.|  
|blocked_event_fire_time|**Int**|O período de tempo durante o qual acionamentos de evento foram bloqueados quando os buffers estavam cheios. Esse valor é **0** se a política de buffer for "Descartar buffer cheio" ou "Descartar eventos". Não permite valor nulo.|  
|create_time|**datetime**|A hora em que a sessão foi criada. Não permite valor nulo.|  
|largest_event_dropped_size|**Int**|O tamanho do maior evento que não se ajustou ao buffer da sessão. Não permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="change-history"></a>Histórico de alterações  
  
|Conteúdo atualizado|  
|---------------------|  
|Corrigido o tipo de dados para o nome e as colunas blocked_event_fire_time.|  
|Removidas as colunas buffer_size e total_buffers.|  
|Adicionadas as colunas de colunas total_regular_buffers, regular_buffer_size, total_large_buffers, large_buffer_size e total_buffer_size.|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

