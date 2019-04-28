---
title: Colunas do modelo de mineração | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- columns [data mining], mining model columns
- columns [data mining]
- REGRESSOR column
- columns [data mining], modeling flags
- modeling flags [data mining]
- MODEL_EXISTENCE_ONLY column
- usage property [data mining]
ms.assetid: fab47643-5bfd-424e-a0f7-69e665db6bab
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 92cee93affaedab7c36517c730e09914ba842041
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62733618"
---
# <a name="mining-model-columns"></a>Colunas do modelo de mineração
  Um modelo de mineração de dados aplica um algoritmo de modelo de mineração aos dados que são representados por uma estrutura de mineração. Como a estrutura de mineração, o modelo de mineração contém colunas. Um modelo de mineração reside na estrutura de mineração e herda todos os valores das propriedades que são definidos pela estrutura de mineração. O modelo pode usar todas as colunas contidas na estrutura de mineração ou um subconjunto das colunas.  
  
 Você pode definir duas informações adicionais em uma coluna de modelo de mineração: uso e sinalizadores de modelagem.  
  
-   **Uso** é uma propriedade que define como o modelo usa a coluna. As colunas podem ser usadas como colunas de entrada, colunas de chave ou colunas previsíveis.  
  
-   Os**sinalizadores de modelagem** fornecem o algoritmo com informações adicionais sobre os dados definidos na tabela de casos, de forma que o algoritmo possa criar um modelo mais preciso. Você pode definir sinalizadores de modelagem programaticamente usando a linguagem DMX (Data Mining Extensions) ou no **Designer de Mineração de Dados** em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 A lista a seguir descreve os sinalizadores de modelagem que você pode definir em uma coluna de modelo de mineração.  
  
 `MODEL_EXISTENCE_ONLY`  
 Indica que a presença do atributo é mais importante que os valores da coluna de atributo. Por exemplo, considere a tabela de casos que contém uma lista de itens do pedido que são associados a um cliente específico. Os dados da tabela incluem o tipo de produto, ID e custo de cada item. Para fins de modelagem, o fato que o cliente comprou um item do pedido em particular pode ser mais importante que o custo em si do item do pedido. Neste caso, a coluna de custo deveria ser marcada como `MODEL_EXISTENCE_ONLY`.  
  
 `REGRESSOR`  
 Indica que o algoritmo pode usar a coluna especificada na fórmula de regressão de algoritmos de regressão. Há suporte para esse sinalizador nos algoritmos das Árvores de Decisão do [!INCLUDE[msCoName](../../includes/msconame-md.md)] e Série Temporal do [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
 Para obter mais informações sobre a configuração da propriedade de uso e definição dos sinalizadores de modelagem programaticamente com DMX, consulte [CRIAR UM MODELO DE MINERAÇÃO &#40;DMX&#41;](/sql/dmx/create-mining-model-dmx). Para obter mais informações sobre a configuração da propriedade de uso e definição dos sinalizadores de modelagem no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], consulte [Movendo objetos de mineração de dados](moving-data-mining-objects.md).  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados &#40;Analysis Services – Data Mining&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [Estruturas de Mineração &#40;Analysis Services – Data Mining&#41;](mining-structures-analysis-services-data-mining.md)   
 [Alterar as propriedades de um modelo de mineração](change-the-properties-of-a-mining-model.md)   
 [Excluir uma coluna de um modelo de mineração](exclude-a-column-from-a-mining-model.md)   
 [Colunas da estrutura de mineração](mining-structure-columns.md)  
  
  
