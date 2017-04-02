---
title: "SQL Server, HTTP_STORAGE_OBJECT | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ae849f79-c581-42a5-a5cc-0a9ebea171b9
caps.latest.revision: 7
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 7
---
# SQL Server, HTTP_STORAGE_OBJECT
  O objeto de desempenho **SQLServer:HTTP_STORAGE_OBJECT** consiste nos contadores de desempenho que monitoram a conta de Armazenamento do Microsoft Azure. Com o recurso [Arquivos de dados do SQL Server no Microsoft Azure](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md), você pode armazenar arquivos de banco de dados nos Blobs de Armazenamento do Microsoft Azure. Esse objeto de desempenho trata cada conta de Armazenamento do Windows Azure como uma unidade diferente.  
  
|Nome do contador|Descrição|  
|------------------|-----------------|  
|**Leitura de bytes/s**|Quantidade de dados que estão sendo transferidos do armazenamento HTTP por segundo durante operações de leitura.|  
|**Gravação de bytes/s**|Quantidade de dados que estão sendo transferidos do armazenamento HTTP por segundo durante operações de gravação.|  
|**Total de bytes/s**|Quantidade de dados que estão sendo transferidos do armazenamento HTTP por segundo durante operações de leitura ou gravação.|  
|**Leituras/s**|Número de leituras por segundo no armazenamento HTTP.|  
|**Gravações/s**|Número de gravações por segundo no armazenamento HTTP.|  
|**Transferências/s**|Número de operações de leitura e gravação por segundo no armazenamento HTTP.|  
|**Média Bytes/leitura**|Número médio de bytes transferidos do armazenamento HTTP por leitura.|  
|**Média Bytes/leitura BASE**|Somente para uso interno.|
|**Média Bytes/transferência**|Número médio de bytes transferidos do armazenamento HTTP durante operações de leitura ou gravação.|  
|**Média Bytes/transferência BASE**|Somente para uso interno.|
|**Média Bytes/gravação**|Número médio de bytes transferidos do armazenamento HTTP por gravação.|  
|**Média Bytes/gravação BASE**|Somente para uso interno.|
|**Média microssegundos/leitura**|O número médio de microssegundos que leva para realizar cada leitura do armazenamento HTTP.|  
|**Média Microssegundos/leitura BASE**|Somente para uso interno.|
|**Média Microssegundos/Leitura Comp**|O número médio de microssegundos que leva para que o HTTP conclua a leitura para armazenamento.| 
|**Média Microssegundos/Leitura Comp BASE**|Somente para uso interno.|
|**Média microssegundos/gravação**|O número médio de microssegundos que leva para realizar cada gravação no armazenamento HTTP.|  
|**Média microssegundos/transferência**|O número médio de microssegundos que leva para realizar cada transferência para o armazenamento HTTP.|  
|**Média Microssegundos/transferência BASE**|Somente para uso interno.|
|**Média Microssegundos/gravação BASE**|Somente para uso interno.|
|**Média Microssegundos/gravação Comp**|O número médio de microssegundos que leva para o HTTP concluir a gravação no armazenamento.|  
|**Média Microssegundos/gravação Comp BASE**|Somente para uso interno.|
|**E/S de armazenamento HTTP pendente**|O número total de E/S pendente para um armazenamento HTTP.|  
|**Falha/s de E/S de Armazenamento HTTP**|Número de solicitações de gravação com falha enviadas ao armazenamento HTTP por segundo.| 
|**Tentativa/s de E/S de armazenamento HTTP**|Número de solicitações de tentativa enviadas para o armazenamento HTTP por segundo.|  
  
## Consulte também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  