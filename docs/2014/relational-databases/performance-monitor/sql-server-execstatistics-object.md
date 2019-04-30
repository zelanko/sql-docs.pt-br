---
title: SQL Server, objeto ExecStatistics | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:ExecStatistics
- ExecStatistics object
ms.assetid: 4f8557a8-345f-4622-a8a5-763a0388ad94
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a09c2a57b76974758626a1847d5f0df3f8b7f55c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63250597"
---
# <a name="sql-server-execstatistics-object"></a>SQL Server, objeto ExecStatistics
  O objeto **SQLServer:ExecStatistics** do Microsoft SQL Server oferece contadores para o monitoramento de diversas execuções.  
  
 Esta tabela descreve os contadores **Exec Statistics** do SQL Server.  
  
|Contadores Exec Statistics do SQL Server|Descrição|  
|-----------------------------------------|-----------------|  
|**Consulta Distribuída**|Estatísticas referentes à execução de consultas distribuídas.|  
|**Chamadas DTC**|Estatísticas referentes à execução de chamadas DTC.|  
|**Procedimentos Estendidos**|Estatísticas referentes à execução de procedimentos estendidos.|  
|**Chamadas OLEDB**|Estatísticas referentes à execução de chamadas OLEDB.|  
  
 Cada contador no objeto contém as seguintes instâncias:  
  
|Item|Descrição|  
|----------|-----------------|  
|**Tempo médio de execução (ms)**|Tempo médio de execução do tipo de execução selecionado.|  
|**Tempo de execução cumulativo (ms) por segundo**|Tempo de execução agregado, por segundo, do tipo de execução selecionado.|  
|**Execuções em andamento**|Número de execuções em andamento do tipo de execução selecionado.|  
|**Execuções iniciadas por segundo**|Número de execuções iniciadas por segundo, do tipo de execução selecionado.|  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
