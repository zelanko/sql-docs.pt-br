---
title: Categoria de eventos de processamento de consulta | Microsoft Docs
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
ms.assetid: a94b3198-be85-4935-845d-1cd4e121fc94
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 462d9a67cf2a56aaf46fb4106ec786c1d003d8a6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="query-processing-events-category"></a>Categoria de eventos de processamento de consultas
  A categoria de evento Processamento de Consulta tem as classes de evento descritas na tabela a seguir.  
  
|**Event Class**|**ID do evento**|**Description**|  
|---------------------|------------------|---------------------|  
|Subcubo de consulta|11|Subcubo de consulta, a Otimização Baseada em Uso.|  
|Subcubo de consulta detalhado|12|Subcubo de consulta com informações detalhadas. Este evento pode ter um impacto negativo no desempenho quando ativado.|  
|Obter Dados de Agregação|60|Responder a consulta obtendo dados de agregação. Este evento pode ter um impacto negativo no desempenho quando ativado.|  
|Obter Dados de Cache|61|Responder a consulta obtendo dados de um dos caches. Este evento pode ter um impacto negativo no desempenho quando ativado.|  
|Início do Cubo de Consulta|70|Coleta todos os eventos Início do Cubo de Consulta desde o começo do rastreamento.|  
|Final do Cubo de Consulta|71|Coleta todos os eventos Final do Cubo de Consulta desde o começo do rastreamento.|  
|Calculate Non Empty Begin|72|Início de cálculo de não vazio.|  
|Calculate Non Empty Current|73|Calcular não vazio atual.|  
|Calculate Non Empty End|74|Término de cálculo de não vazio.|  
|Serialize Results Begin|75|Início da serialização de resultados.|  
|Serializar Resultados Atuais|76|Serializar resultados atuais.|  
|Serializar Final de Resultados|77|Serializar final de resultados.|  
|Executar Início do Script do MDX|78|Executar início do script do MDX.|  
|Executar Script do MDX Atual|79|Executar script do MDX atual.|  
|Execute Final do Script do MDX|80|Executar final do script do MDX.|  
|Dimensão da consulta|81|Dimensão da consulta.|  
|Início da Consulta VertiPaq SE|82|Consulta VertiPaq SE|  
|Final da Consulta VertiPaq SE|83|Consulta VertiPaq SE|  
  
 Para obter informações sobre as colunas associadas a cada classe de evento de Processamento de Consulta, veja [Colunas de dados de Eventos de Consultas](../../analysis-services/trace-events/query-processing-events-data-columns.md).  
  
## <a name="see-also"></a>Consulte também  
 [Eventos de rastreamento do Analysis Services](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  
