---
title: Descobrir a categoria de evento de estado do servidor | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 953936b1f8054e6294788184750bb9e888b43f0f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="discover-server-state-event-category"></a>categoria de evento de identificação do estado do servidor
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  A categoria de evento de identificação do estado do servidor tem as classes de evento descritas na tabela a seguir.  
  
|Event Class|ID do evento|Description|  
|-----------------|--------------|-----------------|  
|Server State Discover Begin|33|Coleta todos os eventos de início de identificação XMLA do estado do servidor desde o início do rastreamento.|  
|Server State Discover Data|34|Coleta todos os eventos de dados de identificação XMLA do estado do servidor desde o início do rastreamento. Esses eventos captam o conteúdo da resposta para a solicitação de identificação.|  
|Server State Discover End|35|Coleta todos os eventos de término de identificação XMLA do estado do servidor desde o início do rastreamento.|  
  
 Para obter informações sobre as colunas associadas a cada classe Query Events, consulte [Descobrir colunas de dados de eventos de estado do servidor](../../analysis-services/trace-events/discover-server-state-events-data-columns.md).  
  
## <a name="see-also"></a>Consulte também  
 [Eventos de rastreamento do Analysis Services](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  
