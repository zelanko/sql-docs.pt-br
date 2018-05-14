---
title: Categoria de eventos de bloqueio | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 62804b077f43b5123b1992a6f52b29af288e2821
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="lock-events-category"></a>Categoria de eventos de bloqueio
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  A categoria de evento Eventos de Bloqueios tem as classes de evento descritas na tabela a seguir.  
  
|Event Class|ID do evento|Description|  
|-----------------|--------------|-----------------|  
|Deadlock|50|Coleta todos os eventos deadlock de bloqueios de metadados desde o início do rastreamento.|  
|Tempo limite de bloqueio|51|Coleta todos os eventos de tempo limite de bloqueio de metadados desde o início do rastreamento.|  
|Lock Acquired|52|Coleta informações sobre bloqueios adquiridos, desde que o rastreamento iniciou.|  
|Lock Released|53|Coleta informações sobre bloqueios liberados, desde que o rastreamento iniciou.|  
|Espera de bloqueio|54|Coleta informações sobre bloqueios no status aguardando, desde que o rastreamento iniciou.|  
  
 Para obter informações sobre as colunas associadas a cada classe de evento de bloqueio, consulte [Lock Events Data Columns](../../analysis-services/trace-events/lock-events-data-columns.md).  
  
## <a name="see-also"></a>Consulte também  
 [Eventos de rastreamento do Analysis Services](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  
