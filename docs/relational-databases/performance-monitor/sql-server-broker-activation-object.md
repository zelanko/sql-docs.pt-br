---
title: SQL Server, objeto de Ativação do Broker | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
s.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Broker Activation
- Broker Activation object
ms.assetid: cd9b6880-c924-42c7-b333-09c303317c0b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 44c71b7b8ce6dd9625a7add7c8403dd7718e4e42
ms.sourcegitcommit: ca038f1ef180e4e1b27910bbc5d87822cd1ed176
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52158694"
---
# <a name="sql-server-broker-activation-object"></a>SQL Server, objeto Broker Activation
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O objeto de desempenho **SQLServer:BrokerActivation** contém contadores de desempenho que relatam informações sobre a ativação de procedimentos armazenados. A tabela a seguir lista os contadores contidos nesse objeto.  
  
|Contadores do SQL Server:BrokerActivation|Descrição|  
|-------------------------------------------|-----------------|  
|**Procedimentos Armazenados Invocados/s**|Este contador informa o número total de procedimentos armazenados de ativação invocados por todos os monitores de fila na instância, por segundo.|  
|**Limite de Tarefas Atingido**|Este contador informa o número total de vezes que um monitor de fila teria iniciado uma nova tarefa, mas não o fez porque o número máximo de tarefas da fila já se encontra em execução.|  
|**Limite de Tarefas Atingido/s**|Este contador informa o número total de vezes, por segundo, que um monitor de fila teria iniciado uma nova tarefa, mas não o fez porque o número máximo de tarefas da fila já se encontra em execução.|  
|**Tarefas Anuladas/s**|Este contador informa o número total de tarefas de procedimentos armazenados de ativação que acabaram em erro ou foram anuladas por um monitor de fila devido a falha em receber mensagens.|  
|**Tarefas em Execução**|Este contador informa o número de procedimentos armazenados de ativação que se encontram atualmente em execução.|  
|**Tarefas Iniciadas/s**|Este contador informa o número total de procedimentos armazenados de ativação iniciados, por segundo, por todos os monitores de fila na instância.|  
  
## <a name="see-also"></a>Consulte Também  
 [.dm_broker_activated_tasks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-broker-activated-tasks-transact-sql.md)   
 [sys.dm_broker_queue_monitors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-broker-queue-monitors-transact-sql.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
