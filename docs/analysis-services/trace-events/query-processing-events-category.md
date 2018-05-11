---
title: Categoria de eventos de processamento de consulta | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 576a07ac29c598691ccdbf00cd3ca165edf99c0d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="query-processing-events-category"></a>Categoria de eventos de processamento de consultas
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
  
  
