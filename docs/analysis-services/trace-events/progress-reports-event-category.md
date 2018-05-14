---
title: Categoria de evento de relatórios de andamento | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f3e48e34e5b85093793b0ea70786b106d72235a7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="progress-reports-event-category"></a>categoria de evento de relatórios de andamento
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  A categoria de evento de relatórios de andamento tem as classes de evento descritas na tabela a seguir.  
  
|Event Class|ID do evento|Description|  
|-----------------|--------------|-----------------|  
|Progress Report Begin|5|Coleta todos os eventos de início de relatório de andamento desde o começo do rastreamento.|  
|Progress Report End|6|Coleta todos os eventos de término de relatório de andamento desde o começo do rastreamento.|  
|Progress Report Current|7|Coleta todos os eventos atuais de relatório de andamento desde o começo do rastreamento. Por exemplo, durante o processamento, os relatórios atuais incluem informações de processamento sobre os objetos que estão processados (dimensões, partições, cubo, etc.).|  
|Progress Report Error|8|Coleta todos os eventos de erro de relatório de andamento desde o começo do rastreamento.|  
  
 Cada evento Progress Report Begin começa com um fluxo de eventos de andamento e termina com um evento Progress Report End. O fluxo pode conter qualquer número de eventos Progress Report Current e Progress Report Error.  
  
 Para obter informações sobre as colunas associadas a cada classe Progress Report, consulte [Progress Reports Data Columns](../../analysis-services/trace-events/progress-reports-data-columns.md).  
  
## <a name="see-also"></a>Consulte também  
 [Eventos de rastreamento do Analysis Services](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  
