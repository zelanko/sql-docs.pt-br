---
title: "Distribui&#231;&#245;es de colunas (minera&#231;&#227;o de dados) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "tipo de distribuição normal [mineração de dados]"
  - "tipo de distribuição uniforme [mineração de dados]"
  - "colunas [mineração de dados], distribuições"
  - "tipo de distribuição normal de log [mineração de dados]"
  - "colunas contínuas"
  - "distribuições [mineração de dados]"
ms.assetid: 87e700de-32be-4bc8-b01d-ba4ee1ab48de
caps.latest.revision: 32
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 32
---
# Distribui&#231;&#245;es de colunas (minera&#231;&#227;o de dados)
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], é possível definir as distribuições de colunas em uma estrutura de mineração para simular como os algoritmos processarão os dados na colunas quando você criar modelos de mineração. Com relação a certos algoritmos, é útil definir a distribuição de colunas contínuas antes de processar o modelo, principalmente quando se sabe que as colunas contêm distribuições comuns de valores. Se as distribuições não estiverem definidas, os modelos de mineração resultantes poderão produzir previsões menos precisas do que se as distribuições estiverem definidas, uma vez que os algoritmos terão menos informações com as quais interpretar dados.  
  
 Os algoritmos que estão disponíveis em [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornecem suporte aos seguintes tipos de distribuição:  
  
 **Normal**  
 Os valores para a coluna contínua formam um histograma com uma distribuição normal.  
  
 ![Histograma com distribuição normal](../../analysis-services/data-mining/media/normal-distribution.png "Histograma com distribuição normal")  
  
 **Log Normal**  
 Os valores para a coluna contínua formam um histograma, onde a curva é alongada na extremidade superior e é inclinada em direção à extremidade inferior.  
  
 ![Histograma com distribuição normal de log](../../analysis-services/data-mining/media/log-normal-distribution.png "Histograma com distribuição normal de log")  
  
 **Uniforme**  
 Os valores para a coluna contínua formam uma curva plana, na qual todos os valores são igualmente prováveis.  
  
 ![Histograma com distribuição uniforme](../../analysis-services/data-mining/media/uniform-distribution.png "Histograma com distribuição uniforme")  
  
 Para obter mais informações sobre os algoritmos fornecidos pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Algoritmos de Data Mining &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
## Consulte também  
 [Tipos de conteúdo &#40;Data Mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md)   
 [Estruturas de Mineração &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Métodos de discretização &#40;Mineração de dados&#41;](../../analysis-services/data-mining/discretization-methods-data-mining.md)   
 [Distribuições &#40;DMX&#41;](../../dmx/distributions-dmx.md)   
 [Colunas da estrutura de mineração](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  