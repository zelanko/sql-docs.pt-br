---
title: SQL Server Agent, objeto Trabalhos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLAgent:Jobs
- Jobs object
ms.assetid: 225b5e2d-4a78-4178-b2b6-b419df83c4aa
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5bd37ab434dbefbb01862f1004ca62e673df0453
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63251026"
---
# <a name="sql-server-agent-jobs-object"></a>SQL Server Agent, objeto Jobs
  O objeto de desempenho **Jobs** do SQL Server Agent contém contadores de desempenho que relatam informações sobre trabalhos do SQL Server Agent. A tabela a seguir lista os contadores contidos nesse objeto.  
  
 A tabela abaixo contém os contadores **SQLAgent:Jobs** .  
  
|Nome|Descrição|  
|----------|-----------------|  
|**Trabalhos Ativos**|Este contador informa o número de trabalhos atualmente em execução.|  
|**Trabalhos com falha**|Este contador informa o número de trabalhos que falharam.|  
|**Taxa de êxito de trabalhos**|Este contador informa a porcentagem de trabalhos executados que foram concluídos com êxito.|  
|**Trabalhos ativados/minuto**|Este contador informa o número de trabalhos iniciados no último minuto.|  
|**Trabalhos em fila**|Este contador informa o número de trabalhos prontos para execução pelo SQL Server Agent, mas que ainda não foram iniciados.|  
|**Trabalhos bem-sucedidos**|Este contador informa o número de trabalhos que obtiveram êxito.|  
  
 Cada contador no objeto contém as seguintes instâncias:  
  
|Instância|Descrição|  
|--------------|-----------------|  
|**_Total**|Informações referentes a todos os trabalhos.|  
|**Alertas**|Informações sobre trabalhos iniciados por alertas.|  
|**Others**|Informações sobre trabalhos que não foram iniciados nem por alertas, nem por agendas. Normalmente, trata-se de trabalhos iniciados manualmente usando **sp_start_job**.|  
|**Agendas**|Informações sobre trabalhos iniciados por agendas.|  
  
## <a name="see-also"></a>Consulte também  
 [Implementar trabalhos](../../ssms/agent/implement-jobs.md)   
 [Usar objetos de desempenho](../../ssms/agent/use-performance-objects.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
