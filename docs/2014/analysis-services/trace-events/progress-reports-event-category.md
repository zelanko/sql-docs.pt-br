---
title: Categoria de evento de relatórios de andamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- progress events [Analysis Services]
- Progress Reports event category
- event classes [Analysis Services], progress reports
ms.assetid: c130f160-28ef-49bc-9ee6-da47dc9aab2a
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 8bcfa530f87d7a8caaee6814c2e2e2282e2783ed
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006437"
---
# <a name="progress-reports-event-category"></a>categoria de evento de relatórios de andamento
  A categoria de evento de relatórios de andamento tem as classes de evento descritas na tabela a seguir.  
  
|Event Class|ID do evento|Description|  
|-----------------|--------------|-----------------|  
|Progress Report Begin|5|Coleta todos os eventos de início de relatório de andamento desde o começo do rastreamento.|  
|Progress Report End|6|Coleta todos os eventos de término de relatório de andamento desde o começo do rastreamento.|  
|Progress Report Current|7|Coleta todos os eventos atuais de relatório de andamento desde o começo do rastreamento. Por exemplo, durante o processamento, os relatórios atuais incluem informações de processamento sobre os objetos que estão processados (dimensões, partições, cubo, etc.).|  
|Progress Report Error|8|Coleta todos os eventos de erro de relatório de andamento desde o começo do rastreamento.|  
  
 Cada evento Progress Report Begin começa com um fluxo de eventos de andamento e termina com um evento Progress Report End. O fluxo pode conter qualquer número de eventos Progress Report Current e Progress Report Error.  
  
 Para obter informações sobre as colunas associadas a cada classe Progress Report, consulte [Progress Reports Data Columns](progress-reports-data-columns.md).  
  
## <a name="see-also"></a>Consulte também  
 [Eventos de rastreamento do Analysis Services](analysis-services-trace-events.md)  
  
  