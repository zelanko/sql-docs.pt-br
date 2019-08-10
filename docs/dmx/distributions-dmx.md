---
title: Distribuições (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fda2eb169985eb670614f611764fbf149c71a42d
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892790"
---
# <a name="distributions-dmx"></a>Distribuições (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  No [!INCLUDE[msCoName](../includes/msconame-md.md)] ,vocêpode[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]definir o conteúdo das colunas em uma estrutura de mineração para afetar como os algoritmos processam os dados nessas colunas quando você cria modelos de mineração. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Com relação a certos algoritmos, é útil definir a distribuição de colunas contínuas antes de processar o modelo, principalmente quando se sabe que as colunas contêm distribuições comuns de valores. Se as distribuições não estiverem definidas, os modelos de mineração resultantes poderão produzir previsões menos precisas do que se as distribuições estiverem definidas, uma vez que os algoritmos terão menos informações com as quais interpretar dados.  
  
 Os algoritmos de mineração de dados do [!INCLUDE[msCoName](../includes/msconame-md.md)] oferecem suporte aos seguintes tipos de distribuição:  
  
 **NORMAL**  
 Os valores para a coluna contínua formam um histograma com uma distribuição Gaussiana normal.  
  
 **Log Normal**  
 Os valores da coluna contínua formam um histograma, onde o logaritmo dos valores é normalmente distribuído.  
  
 **UNIVERSAL**  
 Os valores para a coluna contínua formam uma curva plana, na qual todos os valores são igualmente prováveis.  
  
 Para obter mais informações [!INCLUDE[msCoName](../includes/msconame-md.md)] sobre algoritmos de data mining, consulte [algoritmos &#40;de mineração&#41;de dados Analysis Services-Mineração de dados](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining). Provedores de algoritmo de terceiros podem oferecer suporte a tipos de distribuição adicionais. Para determinar a quais tipos de distribuição um algoritmo dá suporte, use o conjunto de linhas de esquema **SUPPORTED_DISTRIBUTION_FLAGS** .  
  
 Para obter mais informações sobre [ &#40;os&#41;](https://docs.microsoft.com/analysis-services/data-mining/column-distributions-data-mining)tipos de distribuição, consulte mineração de dados de distribuições de coluna.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de conteúdo &#40;Data Mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining)   
 [Referência de DMX &#40;extensões DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Elementos de sintaxe &#40;DMX&#41; de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Referência da função &#40;DMX&#41; das extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referência de operador &#40;DMX&#41; de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referência de instrução &#40;DMX&#41; de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)   
 [Convenções de sintaxe &#40;DMX&#41; de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funções &#40;de previsão gerais DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
