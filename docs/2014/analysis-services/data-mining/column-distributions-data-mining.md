---
title: Distribuições de colunas (mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- normal distribution type [data mining]
- uniform distribution type [data mining]
- columns [data mining], distributions
- log normal distribution type [data mining]
- continuous columns
- distributions [data mining]
ms.assetid: 87e700de-32be-4bc8-b01d-ba4ee1ab48de
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5db71b5a94285f8ae63afeb65bec3f9807f8da27
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085713"
---
# <a name="column-distributions-data-mining"></a>Distribuições de colunas (mineração de dados)
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], é possível definir as distribuições de colunas em uma estrutura de mineração para simular como os algoritmos processarão os dados na colunas quando você criar modelos de mineração. Com relação a certos algoritmos, é útil definir a distribuição de colunas contínuas antes de processar o modelo, principalmente quando se sabe que as colunas contêm distribuições comuns de valores. Se as distribuições não estiverem definidas, os modelos de mineração resultantes poderão produzir previsões menos precisas do que se as distribuições estiverem definidas, uma vez que os algoritmos terão menos informações com as quais interpretar dados.  
  
 Os algoritmos que estão disponíveis em [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornecem suporte aos seguintes tipos de distribuição:  
  
 `Normal`  
 Os valores para a coluna contínua formam um histograma com uma distribuição normal.  
  
 ![Histograma com distribuição normal](../media/normal-distribution.gif "histograma com distribuição normal")  
  
 `Log Normal`  
 Os valores para a coluna contínua formam um histograma, onde a curva é alongada na extremidade superior e é inclinada em direção à extremidade inferior.  
  
 ![Histograma com distribuição normal de log](../media/log-normal-distribution.gif "histograma com distribuição normal de log")  
  
 `Uniform`  
 Os valores para a coluna contínua formam uma curva plana, na qual todos os valores são igualmente prováveis.  
  
 ![Histograma com distribuição uniforme](../media/uniform-distribution.gif "histograma com distribuição uniforme")  
  
 Para obter mais informações sobre os algoritmos fornecidos pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Algoritmos de Data Mining &#40;Analysis Services – Data Mining&#41;](data-mining-algorithms-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de conteúdo &#40;Data Mining&#41;](content-types-data-mining.md)   
 [Estruturas de Mineração &#40;Analysis Services – Data Mining&#41;](mining-structures-analysis-services-data-mining.md)   
 [Métodos de discretização &#40;Mineração de dados&#41;](discretization-methods-data-mining.md)   
 [Distribuições &#40;DMX&#41;](/sql/dmx/distributions-dmx)   
 [Colunas da estrutura de mineração](mining-structure-columns.md)  
  
  
