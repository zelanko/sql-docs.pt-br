---
title: "Distribuições de coluna (mineração de dados) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- normal distribution type [data mining]
- uniform distribution type [data mining]
- columns [data mining], distributions
- log normal distribution type [data mining]
- continuous columns
- distributions [data mining]
ms.assetid: 87e700de-32be-4bc8-b01d-ba4ee1ab48de
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 96b2502e351f371163d5b748b432d381d237a8a9
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="column-distributions-data-mining"></a>Distribuições de colunas (mineração de dados)
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], é possível definir as distribuições de colunas em uma estrutura de mineração para simular como os algoritmos processarão os dados na colunas quando você criar modelos de mineração. Com relação a certos algoritmos, é útil definir a distribuição de colunas contínuas antes de processar o modelo, principalmente quando se sabe que as colunas contêm distribuições comuns de valores. Se as distribuições não estiverem definidas, os modelos de mineração resultantes poderão produzir previsões menos precisas do que se as distribuições estiverem definidas, uma vez que os algoritmos terão menos informações com as quais interpretar dados.  
  
 Os algoritmos que estão disponíveis em [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornecem suporte aos seguintes tipos de distribuição:  
  
 **Normal**  
 Os valores para a coluna contínua formam um histograma com uma distribuição normal.  
  
 ![Histograma com distribuição normal](../../analysis-services/data-mining/media/normal-distribution.gif "histograma com distribuição normal")  
  
 **Log Normal**  
 Os valores para a coluna contínua formam um histograma, onde a curva é alongada na extremidade superior e é inclinada em direção à extremidade inferior.  
  
 ![Histograma com distribuição normal de log](../../analysis-services/data-mining/media/log-normal-distribution.gif "histograma com distribuição normal de log")  
  
 **Uniforme**  
 Os valores para a coluna contínua formam uma curva plana, na qual todos os valores são igualmente prováveis.  
  
 ![Histograma com distribuição uniforme](../../analysis-services/data-mining/media/uniform-distribution.gif "histograma com distribuição uniforme")  
  
 Para obter mais informações sobre os algoritmos fornecidos pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Algoritmos de Data Mining &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de conteúdo &#40;Data Mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md)   
 [Estruturas de Mineração &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Os métodos de diferenciação &#40; mineração de dados &#41;](../../analysis-services/data-mining/discretization-methods-data-mining.md)   
 [Distribuições &#40; DMX &#41;](../../dmx/distributions-dmx.md)   
 [Colunas da estrutura de mineração](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  

