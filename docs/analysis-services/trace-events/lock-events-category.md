---
title: Categoria de eventos de bloqueio | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 06427f8e-89bb-4710-a0c1-dc5e42b7e95e
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 7e1b7a18c7ed5f763674ade69647a26f775cfb98
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
  
  
