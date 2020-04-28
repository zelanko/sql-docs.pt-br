---
title: SQL Server, HTTP_STORAGE_OBJECT | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: ae849f79-c581-42a5-a5cc-0a9ebea171b9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f104f7a6395442484be15f1e72c849edbf11e74f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "70152684"
---
# <a name="sql-server-http_storage_object"></a>SQL Server, HTTP_STORAGE_OBJECT
  O objeto de desempenho **SqlServer: HTTP_STORAGE_OBJECT** consiste em contadores de desempenho que monitoram a conta de armazenamento do Azure. Usando [SQL Server arquivos de dados no recurso do Azure](../databases/sql-server-data-files-in-microsoft-azure.md) , você pode armazenar arquivos de banco de dado em blobs de armazenamento do Azure. Esse objeto de desempenho trata cada conta de Armazenamento do Microsoft Azure como uma unidade diferente.  
  
|Nome do contador|Descrição|  
|------------------|-----------------|  
|**Leitura de bytes/s**|Quantidade de dados que estão sendo transferidos do armazenamento HTTP por segundo durante operações de leitura.|  
|**Gravação de bytes/s**|Quantidade de dados que estão sendo transferidos do armazenamento HTTP por segundo durante operações de gravação.|  
|**Total de bytes/s**|Quantidade de dados que estão sendo transferidos do armazenamento HTTP por segundo durante operações de leitura ou gravação.|  
|**Leituras/s**|Número de leituras por segundo no armazenamento HTTP.|  
|**Gravações/s**|Número de gravações por segundo no armazenamento HTTP.|  
|**Transferências/s**|Número de operações de leitura e gravação por segundo no armazenamento HTTP.|  
|**Média de bytes/leitura**|Número médio de bytes transferidos do armazenamento HTTP por leitura.|  
|**Média de bytes/gravação**|Número médio de bytes transferidos do armazenamento HTTP por gravação.|  
|**Média de bytes/transferência**|Número médio de bytes transferidos do armazenamento HTTP durante operações de leitura ou gravação.|  
|**Média de microssegundos/leitura**|O número médio de microssegundos que leva para realizar cada leitura do armazenamento HTTP.|  
|**Média de microssegundos/gravação**|O número médio de microssegundos que leva para realizar cada gravação no armazenamento HTTP.|  
|**Média de microssegundos/transferência**|O número médio de microssegundos que leva para realizar cada transferência para o armazenamento HTTP.|  
|**E/S de armazenamento HTTP pendente**|O número total de E/S pendente para um armazenamento HTTP.|  
|**Tentativa/s de E/S de armazenamento HTTP**|Número de solicitações de tentativa enviadas para o armazenamento HTTP por segundo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
