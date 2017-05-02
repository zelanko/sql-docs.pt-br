---
title: SQL Server Agent, objeto Trabalhos | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLAgent:Jobs
- Jobs object
ms.assetid: 225b5e2d-4a78-4178-b2b6-b419df83c4aa
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a8f2931c070c0ed3816fb348b4ca41f3705b19a0
ms.lasthandoff: 04/11/2017

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
 [Implementar trabalhos](http://msdn.microsoft.com/library/69e06724-25c7-4fb3-8a5b-3d4596f21756)   
 [Usar objetos de desempenho](http://msdn.microsoft.com/library/830b843a-6b2a-4620-a51b-98358e9fc54b)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
