---
title: Descobrir a categoria de evento de estado do servidor | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- Discover Server State event category
- server state events [Analysis Services]
- discover server state events
- event classes [Analysis Services], discover server state
ms.assetid: b62ebf66-d090-4f74-8c83-11ed518b2018
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bc94790d8903fa644bd79fa9328c60a781b62d4b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="discover-server-state-event-category"></a>categoria de evento de identificação do estado do servidor
  A categoria de evento de identificação do estado do servidor tem as classes de evento descritas na tabela a seguir.  
  
|Event Class|ID do evento|Description|  
|-----------------|--------------|-----------------|  
|Server State Discover Begin|33|Coleta todos os eventos de início de identificação XMLA do estado do servidor desde o início do rastreamento.|  
|Server State Discover Data|34|Coleta todos os eventos de dados de identificação XMLA do estado do servidor desde o início do rastreamento. Esses eventos captam o conteúdo da resposta para a solicitação de identificação.|  
|Server State Discover End|35|Coleta todos os eventos de término de identificação XMLA do estado do servidor desde o início do rastreamento.|  
  
 Para obter informações sobre as colunas associadas a cada classe Query Events, consulte [Descobrir colunas de dados de eventos de estado do servidor](../../analysis-services/trace-events/discover-server-state-events-data-columns.md).  
  
## <a name="see-also"></a>Consulte também  
 [Eventos de rastreamento do Analysis Services](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  

