---
title: "Colunas do modelo de minera&#231;&#227;o | Microsoft Docs"
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
  - "colunas [mineração de dados], colunas do modelo de mineração"
  - "colunas [mineração de dados]"
  - "Coluna REGRESSOR"
  - "colunas [mineração de dados], sinalizadores de modelagem"
  - "sinalizadores de modelagem [mineração de dados]"
  - "Coluna MODEL_EXISTENCE_ONLY"
  - "propriedade de uso [mineração de dados]"
ms.assetid: fab47643-5bfd-424e-a0f7-69e665db6bab
caps.latest.revision: 38
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 38
---
# Colunas do modelo de minera&#231;&#227;o
  Um modelo de mineração de dados aplica um algoritmo de modelo de mineração aos dados que são representados por uma estrutura de mineração. Como a estrutura de mineração, o modelo de mineração contém colunas. Um modelo de mineração reside na estrutura de mineração e herda todos os valores das propriedades que são definidos pela estrutura de mineração. O modelo pode usar todas as colunas contidas na estrutura de mineração ou um subconjunto das colunas.  
  
 Você pode definir duas informações adicionais em uma coluna de modelo de mineração: uso e sinalizadores de modelagem.  
  
-   **Uso** é uma propriedade que define como o modelo usa a coluna. As colunas podem ser usadas como colunas de entrada, colunas de chave ou colunas previsíveis.  
  
-   Os **sinalizadores de modelagem** fornecem o algoritmo com informações adicionais sobre os dados definidos na tabela de casos, de forma que o algoritmo possa criar um modelo mais preciso. Você pode definir sinalizadores de modelagem programaticamente usando a linguagem DMX (Data Mining Extensions) ou no **Designer de Mineração de Dados** em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 A lista a seguir descreve os sinalizadores de modelagem que você pode definir em uma coluna de modelo de mineração.  
  
 **MODEL_EXISTENCE_ONLY**  
 Indica que a presença do atributo é mais importante que os valores da coluna de atributo. Por exemplo, considere a tabela de casos que contém uma lista de itens do pedido que são associados a um cliente específico. Os dados da tabela incluem o tipo de produto, ID e custo de cada item. Para fins de modelagem, o fato que o cliente comprou um item do pedido em particular pode ser mais importante que o custo em si do item do pedido. Neste caso, a coluna de custo deveria ser marcada como **MODEL_EXISTENCE_ONLY**.  
  
 **REGRESSOR**  
 Indica que o algoritmo pode usar a coluna especificada na fórmula de regressão de algoritmos de regressão. Há suporte para esse sinalizador nos algoritmos das Árvores de Decisão do [!INCLUDE[msCoName](../../includes/msconame-md.md)] e Série Temporal do [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
 Para obter mais informações sobre a configuração da propriedade de uso e definição dos sinalizadores de modelagem programaticamente com DMX, consulte [CRIAR UM MODELO DE MINERAÇÃO &#40;DMX&#41;](../../dmx/create-mining-model-dmx.md). Para obter mais informações sobre a configuração da propriedade de uso e definição dos sinalizadores de modelagem no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], consulte [Movendo objetos de mineração de dados](../../analysis-services/data-mining/moving-data-mining-objects.md).  
  
## Consulte também  
 [Algoritmos de mineração de dados &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Estruturas de Mineração &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Alterar as propriedades de um modelo de mineração](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md)   
 [Excluir uma coluna de um modelo de mineração](../../analysis-services/data-mining/exclude-a-column-from-a-mining-model.md)   
 [Colunas da estrutura de mineração](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  