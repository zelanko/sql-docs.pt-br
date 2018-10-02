---
title: SQL Server, objeto Estatísticas Resp do Lote | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Batch Resp Statistics
ms.assetid: a58e8733-6a8d-4b47-b5cb-042e813d808a
author: dagiro
ms.author: v-dagir
manager: craigg
ms.openlocfilehash: a35437442460a8f987921f17da26e40d67f02a8e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47685574"
---
# <a name="sql-server-batch-resp-statistics-object"></a>SQLServer, Objeto Batch Resp Statistics
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
O objeto de desempenho **SQLServer:Batch Resp Statistics** fornece contadores para acompanhar os tempos de resposta de lote do SQL Server.

A tabela a seguir descreve os objetos de desempenho de **Estatística de resposta de lote** do SQL Server.


|**Estatísticas de resposta de lote do SQL Server**|Descrição|  
|-------------|-----------------|  
|**Lotes >=000000ms e \<000001ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 0 ms, porém menor que 1 ms|
|**Lotes >=000001ms e \<000002ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 1 ms, porém menos de 2 ms|
|**Lotes >=000002ms e \<000005ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 2 ms, porém menos de 5 ms|
|**Lotes >=000005ms e \<000010ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 5 ms, porém menos de 10 ms|
|**Lotes >=000010ms e \<000020ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 10 ms, porém menos de 20 ms|
|**Lotes >=000020ms e \<000050ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 20 ms, porém menos de 50 ms|
|**Lotes >=000050ms e \<000100ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 50 ms, porém menos de 100 ms|
|**Lotes >=000100ms e \<000200ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 100 ms, porém menos de 200 ms|
|**Lotes >=000200ms e \<000500ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 200 ms, porém menos de 500 ms|
|**Lotes >=000500ms e \<001000ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 500 ms, porém menos de 1.000 ms|
|**Lotes >=001000ms e \<002000ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 1.000 ms, porém menos de 2.000 ms|
|**Lotes >=002000ms e \<005000ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 2.000 ms, porém menos de 5.000 ms|
|**Lotes >=005000ms e \<010000ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 5.000 ms, porém menos de 10.000 ms|
|**Lotes >=010000ms e \<020000ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 10.000 ms, porém menos de 20.000 ms|
|**Lotes >=020000ms e \<050000ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 20.000 ms, porém menos de 50.000 ms|
|**Lotes >=050000ms e \<100000ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 50.000 ms, porém menos de 100.000 ms| 
|**Lotes > = 100000 ms**|Número de Lotes SQL com tempo de resposta maior ou igual a 100.000 ms| 

Cada contador no objeto contém as seguintes instâncias:  
  
|Item|Descrição|  
|----------|-----------------|  
|**Tempo de CPU:Solicitações**|O tempo de CPU gasto na solicitação.|  
|**Tempo de CPU:Total(ms)**|O tempo total de CPU gasto no lote.|  
|**Tempo Decorrido:Solicitações**|O tempo decorrido da solicitação.|  
|**Tempo Decorrido:Total(ms)**|O tempo decorrido do lote.|  

## <a name="see-also"></a>Consulte Também
[SQL Server, objeto Cache de planos](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md)  
[Monitorar o uso de recursos (Monitor do Sistema)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
