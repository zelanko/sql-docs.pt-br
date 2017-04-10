---
title: "SQLServer, Objeto Batch Resp Statistics | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQLServer:Batch Resp Statistics"
ms.assetid: a58e8733-6a8d-4b47-b5cb-042e813d808a
caps.latest.revision: 3
author: "dagiro"
ms.author: "v-dagir"
manager: "jhubbard"
caps.handback.revision: 3
---
# SQLServer, Objeto Batch Resp Statistics
O objeto de desempenho **SQLServer:Batch Resp Statistics** fornece contadores para acompanhar os tempos de resposta de lote do SQL Server.

A tabela a seguir descreve os objetos de desempenho de **Estatística de resposta de lote** do SQL Server.


|**Estatísticas de resposta de lote do SQL Server**|Description|  
|-------------|-----------------|  
|**Lotes >= 000000 ms e \< 000001 ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 0 ms, porém menor que 1 ms|
|**Lotes >= 000001 ms e \< 000002 ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 1 ms, porém menos de 2 ms|
|**Lotes >= 000002 ms e \< 000005 ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 2 ms, porém menos de 5 ms|
|**Lotes >= 000005 ms e \< 000010 ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 5 ms, porém menos de 10 ms|
|**Lotes >= 000010 ms e \< 000020 ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 10 ms, porém menos de 20 ms|
|**Lotes >= 000020 ms e \< 000050 ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 20 ms, porém menos de 50 ms|
|**Lotes >= 000050 ms e \< 000100 ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 50 ms, porém menos de 100 ms|
|**Lotes >= 000100 ms e \< 000200 ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 100 ms, porém menos de 200 ms|
|**Lotes >= 000200 ms e \< 000500 ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 200 ms, porém menos de 500 ms|
|**Lotes >= 000500 ms e \< 001000 ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 500 ms, porém menos de 1.000 ms|
|**Lotes >= 001000 ms e \< 002000 ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 1.000 ms, porém menos de 2.000 ms|
|**Lotes >= 002000 ms e \< 005000 ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 2.000 ms, porém menos de 5.000 ms|
|**Lotes >= 005000 ms e \< 010000 ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 5.000 ms, porém menos de 10.000 ms|
|**Lotes >= 010000 ms e \< 020000 ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 10.000 ms, porém menos de 20.000 ms|
|**Lotes >= 020000 ms e \< 050000 ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 20.000 ms, porém menos de 50.000 ms|
|**Lotes >= 050000 ms e \< 100000 ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 50.000 ms, porém menos de 100.000 ms| 
|**Lotes > = 100000 ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 100.000 ms| 

Cada contador no objeto contém as seguintes instâncias:  
  
|Item|Description|  
|----------|-----------------|  
|**Tempo de CPU:Solicitações**|O tempo de CPU gasto na solicitação.|  
|**Tempo de CPU:Total(ms)**|O tempo total de CPU gasto no lote.|  
|**Tempo Decorrido:Solicitações**|O tempo decorrido da solicitação.|  
|**Tempo Decorrido:Total(ms)**|O tempo decorrido do lote.|  

## Consulte também
[SQL Server, objeto Cache de planos](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md)  
[Monitorar o uso de recursos (Monitor do Sistema)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  