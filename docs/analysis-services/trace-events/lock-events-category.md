---
title: Categoria de eventos de bloqueio | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: trace-events
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 06427f8e-89bb-4710-a0c1-dc5e42b7e95e
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8b2e6ba2dc66621bd74026f8aceb8c35eed4f0b1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="lock-events-category"></a>Categoria de eventos de bloqueio
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
  
  
