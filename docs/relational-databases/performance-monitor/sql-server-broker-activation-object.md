---
title: "SQL Server, objeto Broker Activation | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQLServer:Broker Activation"
  - "objeto Broker Activation"
ms.assetid: cd9b6880-c924-42c7-b333-09c303317c0b
caps.latest.revision: 20
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 20
---
# SQL Server, objeto Broker Activation
  O objeto de desempenho **SQLServer:BrokerActivation** contém contadores de desempenho que relatam informações sobre a ativação de procedimentos armazenados. A tabela a seguir lista os contadores contidos nesse objeto.  
  
|Contadores do SQL Server:BrokerActivation|Descrição|  
|-------------------------------------------|-----------------|  
|**Procedimentos Armazenados Invocados/s**|Este contador informa o número total de procedimentos armazenados de ativação invocados por todos os monitores de fila na instância, por segundo.|  
|**Limite de Tarefas Atingido**|Este contador informa o número total de vezes que um monitor de fila teria iniciado uma nova tarefa, mas não o fez porque o número máximo de tarefas da fila já se encontra em execução.|  
|**Limite de Tarefas Atingido/s**|Este contador informa o número total de vezes, por segundo, que um monitor de fila teria iniciado uma nova tarefa, mas não o fez porque o número máximo de tarefas da fila já se encontra em execução.|  
|**Tarefas Anuladas/s**|Este contador informa o número total de tarefas de procedimentos armazenados de ativação que acabaram em erro ou foram anuladas por um monitor de fila devido a falha em receber mensagens.|  
|**Tarefas em Execução**|Este contador informa o número de procedimentos armazenados de ativação que se encontram atualmente em execução.|  
|**Tarefas Iniciadas/s**|Este contador informa o número total de procedimentos armazenados de ativação iniciados, por segundo, por todos os monitores de fila na instância.|  
  
## Consulte também  
 [.dm_broker_activated_tasks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-broker-activated-tasks-transact-sql.md)   
 [sys.dm_broker_queue_monitors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-broker-queue-monitors-transact-sql.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  