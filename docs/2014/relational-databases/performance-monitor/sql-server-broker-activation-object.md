---
title: SQL Server, objeto de Ativação do Broker | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLServer:Broker Activation
- Broker Activation object
ms.assetid: cd9b6880-c924-42c7-b333-09c303317c0b
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 641769c00de48f5acadc69816071893fb6594050
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007926"
---
# <a name="sql-server-broker-activation-object"></a>SQL Server, objeto Broker Activation
  O objeto de desempenho **SQLServer:BrokerActivation** contém contadores de desempenho que relatam informações sobre a ativação de procedimentos armazenados. A tabela a seguir lista os contadores contidos nesse objeto.  
  
|Contadores do SQL Server:BrokerActivation|Description|  
|-------------------------------------------|-----------------|  
|**Procedimentos Armazenados Invocados/s**|Este contador informa o número total de procedimentos armazenados de ativação invocados por todos os monitores de fila na instância, por segundo.|  
|**Limite de Tarefas Atingido**|Este contador informa o número total de vezes que um monitor de fila teria iniciado uma nova tarefa, mas não o fez porque o número máximo de tarefas da fila já se encontra em execução.|  
|**Limite de Tarefas Atingido/s**|Este contador informa o número total de vezes, por segundo, que um monitor de fila teria iniciado uma nova tarefa, mas não o fez porque o número máximo de tarefas da fila já se encontra em execução.|  
|**Tarefas Anuladas/s**|Este contador informa o número total de tarefas de procedimentos armazenados de ativação que acabaram em erro ou foram anuladas por um monitor de fila devido a falha em receber mensagens.|  
|**Tarefas em Execução**|Este contador informa o número de procedimentos armazenados de ativação que se encontram atualmente em execução.|  
|**Tarefas Iniciadas/s**|Este contador informa o número total de procedimentos armazenados de ativação iniciados, por segundo, por todos os monitores de fila na instância.|  
  
## <a name="see-also"></a>Consulte também  
 [.dm_broker_activated_tasks &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-broker-activated-tasks-transact-sql)   
 [sys.dm_broker_queue_monitors &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-broker-queue-monitors-transact-sql)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
