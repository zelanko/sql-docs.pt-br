---
title: SQL Server, HTTP_STORAGE_OBJECT | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ae849f79-c581-42a5-a5cc-0a9ebea171b9
caps.latest.revision: "7"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eeac17b8e62ca25f3f1257005f0911e603f91440
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-httpstorageobject"></a>SQL Server, HTTP_STORAGE_OBJECT
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] O objeto de desempenho **SQLServer:HTTP_STORAGE_OBJECT** consiste nos contadores de desempenho que monitoram a conta de Armazenamento do Microsoft Azure. Com o recurso [Arquivos de dados do SQL Server no Microsoft Azure](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md) , você pode armazenar arquivos de banco de dados nos Blobs de Armazenamento do Microsoft Azure. Esse objeto de desempenho trata cada conta de Armazenamento do Windows Azure como uma unidade diferente.  
  
|Nome do contador|Description|  
|------------------|-----------------|  
|**Leitura de bytes/s**|Quantidade de dados que estão sendo transferidos do armazenamento HTTP por segundo durante operações de leitura.|  
|**Gravação de bytes/s**|Quantidade de dados que estão sendo transferidos do armazenamento HTTP por segundo durante operações de gravação.|  
|**Total de bytes/s**|Quantidade de dados que estão sendo transferidos do armazenamento HTTP por segundo durante operações de leitura ou gravação.|  
|**Leituras/s**|Número de leituras por segundo no armazenamento HTTP.|  
|**Gravações/s**|Número de gravações por segundo no armazenamento HTTP.|  
|**Transferências/s**|Número de operações de leitura e gravação por segundo no armazenamento HTTP.|  
|**Méd. de Bytes/leitura**|Número médio de bytes transferidos do armazenamento HTTP por leitura.|  
|**Méd. de Bytes/leitura BASE**|Somente para uso interno.|
|**Méd. de Bytes/transferência**|Número médio de bytes transferidos do armazenamento HTTP durante operações de leitura ou gravação.|  
|**Méd. de Bytes/transferência BASE**|Somente para uso interno.|
|**Méd. de Bytes/gravação**|Número médio de bytes transferidos do armazenamento HTTP por gravação.|  
|**Méd. de Bytes/gravação BASE**|Somente para uso interno.|
|**Média de microssegundos/leitura**|O número médio de microssegundos que leva para realizar cada leitura do armazenamento HTTP.|  
|**Média de microssegundos/leitura BASE**|Somente para uso interno.|
|**Média de microssegundos/leitura Comp**|O número médio de microssegundos que leva para que o HTTP conclua a leitura para armazenamento.| 
|**Média de microssegundos/leitura Comp BASE**|Somente para uso interno.|
|**Média de microssegundos/gravação**|O número médio de microssegundos que leva para realizar cada gravação no armazenamento HTTP.|  
|**Média de microssegundos/transferência**|O número médio de microssegundos que leva para realizar cada transferência para o armazenamento HTTP.|  
|**Média de microssegundos/transferência BASE**|Somente para uso interno.|
|**Média de microssegundos/gravação BASE**|Somente para uso interno.|
|**Média de microssegundos/gravação Comp**|O número médio de microssegundos que leva para o HTTP concluir a gravação no armazenamento.|  
|**Média de microssegundos/gravação Comp BASE**|Somente para uso interno.|
|**E/S de armazenamento HTTP pendente**|O número total de E/S pendente para um armazenamento HTTP.|  
|**Falha/s de E/S de Armazenamento HTTP**|Número de solicitações de gravação com falha enviadas ao armazenamento HTTP por segundo.| 
|**Tentativa/s de E/S de armazenamento HTTP**|Número de solicitações de tentativa enviadas para o armazenamento HTTP por segundo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
