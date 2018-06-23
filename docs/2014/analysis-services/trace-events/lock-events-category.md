---
title: Categoria de eventos de bloqueio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 06427f8e-89bb-4710-a0c1-dc5e42b7e95e
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 8e9bb88bb19f92ea383049ac62a500d1b0f5319f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121781"
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
  
 Para obter informações sobre as colunas associadas a cada classe de evento de bloqueio, consulte [Lock Events Data Columns](lock-events-data-columns.md).  
  
## <a name="see-also"></a>Consulte também  
 [Eventos de rastreamento do Analysis Services](analysis-services-trace-events.md)  
  
  