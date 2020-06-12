---
title: Distribuições (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 535d1caff3729b552ef0982b056eb516b8f23048
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669768"
---
# <a name="distributions-dmx"></a>Distribuições (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  No [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , você pode definir o conteúdo das colunas em uma estrutura de mineração para afetar como os algoritmos processam os dados nessas colunas quando você cria modelos de mineração. Com relação a certos algoritmos, é útil definir a distribuição de colunas contínuas antes de processar o modelo, principalmente quando se sabe que as colunas contêm distribuições comuns de valores. Se as distribuições não estiverem definidas, os modelos de mineração resultantes poderão produzir previsões menos precisas do que se as distribuições estiverem definidas, uma vez que os algoritmos terão menos informações com as quais interpretar dados.  
  
 Os algoritmos de mineração de dados do [!INCLUDE[msCoName](../includes/msconame-md.md)] oferecem suporte aos seguintes tipos de distribuição:  
  
 **NORMAL**  
 Os valores para a coluna contínua formam um histograma com uma distribuição Gaussiana normal.  
  
 **Log Normal**  
 Os valores da coluna contínua formam um histograma, onde o logaritmo dos valores é normalmente distribuído.  
  
 **UNIVERSAL**  
 Os valores para a coluna contínua formam uma curva plana, na qual todos os valores são igualmente prováveis.  
  
 Para obter mais informações sobre [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmos de data mining, consulte [algoritmos de mineração de dados &#40;Analysis Services-&#41;de mineração de dados ](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining). Provedores de algoritmo de terceiros podem oferecer suporte a tipos de distribuição adicionais. Para determinar a quais tipos de distribuição um algoritmo dá suporte, use o conjunto de linhas de esquema **SUPPORTED_DISTRIBUTION_FLAGS** .  
  
 Para obter mais informações sobre tipos de distribuição, consulte [distribuições de coluna &#40;mineração de dados&#41;](https://docs.microsoft.com/analysis-services/data-mining/column-distributions-data-mining).  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de conteúdo &#40;mineração de dados&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining)   
 [Referência de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-reference.md)   
 [As extensões de mineração de dados &#40;elementos de sintaxe DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referência de operador de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referência de instrução&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)   
 [&#40;as convenções de sintaxe de&#41; DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funções de previsão gerais &#40;&#41;DMX](../dmx/general-prediction-functions-dmx.md)   
 [Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
