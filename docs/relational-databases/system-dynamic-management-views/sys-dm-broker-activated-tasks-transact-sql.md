---
title: . dm_broker_activated_tasks (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_broker_activated_tasks
- sys.dm_broker_activated_tasks_TSQL
- dm_broker_activated_tasks
- dm_broker_activated_tasks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_broker_activated_tasks dynamic management view
ms.assetid: 17e6f87f-8f56-489d-9aed-216afc8ef310
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5cc4c56a55b99c424ea6f6c89a6b3b3796b9b516
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmbrokeractivatedtasks-transact-sql"></a>sys.dm_broker_activated_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada procedimento armazenado ativado pelo Service Broker.  
 

|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**spid**|**Int**|ID da sessão do procedimento armazenado ativado. É NULLABLE.|  
|**database_id**|**smallint**|ID do banco de dados no qual a fila está definida. É NULLABLE.|  
|**queue_id**|**Int**|ID do objeto da fila para a qual o procedimento armazenado foi ativado. É NULLABLE.|  
|**procedure_name**|**nvarchar(650)**|Nome do procedimento armazenado ativado. É NULLABLE.|  
|**execute_as**|**Int**|ID do usuário com o qual o procedimento armazenado é executado. É NULLABLE.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="physical-joins"></a>Junções físicas  
 ![Junções para sys.DM broker_queue_monitors](../../relational-databases/system-dynamic-management-views/media/join-dm-broker-activated-tasks-1.gif "junções para sys.DM broker_queue_monitors")  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
|De|Para|Relação|  
|----------|--------|------------------|  
|dm_broker_activated_tasks.spid|dm_exec_sessions.session_id|Um para um|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico & #40; relacionadas ao Service Broker Transact-SQL & #41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
  

