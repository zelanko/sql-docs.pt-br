---
title: "Categoria de evento de identifica&#231;&#227;o do estado do servidor | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "categoria de evento de identificação do estado do servidor"
  - "eventos de estado do servidor [Analysis Services]"
  - "eventos de identificação do estado do servidor"
  - "classes de evento [Analysis Services], descobrir o estado do servidor"
ms.assetid: b62ebf66-d090-4f74-8c83-11ed518b2018
caps.latest.revision: 25
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 25
---
# Categoria de evento de identifica&#231;&#227;o do estado do servidor
  A categoria de evento de identificação do estado do servidor tem as classes de evento descritas na tabela a seguir.  
  
|Event Class|ID do evento|Description|  
|-----------------|--------------|-----------------|  
|Server State Discover Begin|33|Coleta todos os eventos de início de identificação XMLA do estado do servidor desde o início do rastreamento.|  
|Server State Discover Data|34|Coleta todos os eventos de dados de identificação XMLA do estado do servidor desde o início do rastreamento. Esses eventos captam o conteúdo da resposta para a solicitação de identificação.|  
|Server State Discover End|35|Coleta todos os eventos de término de identificação XMLA do estado do servidor desde o início do rastreamento.|  
  
 Para obter informações sobre as colunas associadas a cada classe Query Events, consulte [Descobrir colunas de dados de eventos de estado do servidor](../../analysis-services/trace-events/discover-server-state-events-data-columns.md).  
  
## Consulte também  
 [Eventos de rastreamento do Analysis Services](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  