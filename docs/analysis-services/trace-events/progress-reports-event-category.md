---
title: "Categoria de evento de relatórios de andamento | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- progress events [Analysis Services]
- Progress Reports event category
- event classes [Analysis Services], progress reports
ms.assetid: c130f160-28ef-49bc-9ee6-da47dc9aab2a
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c90cfbe7e30d0678d13a329737c21f7d45575e22
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
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
  
  
