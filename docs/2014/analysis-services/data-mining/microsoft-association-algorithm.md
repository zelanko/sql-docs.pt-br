---
title: Algoritmo de associação da Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MinimumProbability property
- itemsets [Analysis Services]
- MaximumItemsetCount property
- MinimumSupport property
- OPTIMIZED_PREDICTION_COUNT
- OptimizedPredictionCount property
- MaximumSupport property
- MINIMUM_PROBABILITY
- algorithms [data mining]
- association algorithms [Analysis Services]
- rules [Data Mining]
- association rules
- MinimumItemsetSize property
- market basket analysis [Analysis Services]
- associations [Analysis Services]
- MINIMUM_SUPPORT
- MAXIMUM_SUPPORT
- MINIMUM_ITEMSET_SIZE
- MaximumItemsetSize property
ms.assetid: 8b6b8247-62f9-4f6f-b1af-d01dab290e4c
caps.latest.revision: 53
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4dfed3abb4cff8826c42770996a2ea78ab4b324a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013229"
---
# <a name="microsoft-association-algorithm"></a>Algoritmo Associação da Microsoft
  O algoritmo Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] é um algoritmo de associação fornecido pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que é útil para mecanismos de recomendação. Um mecanismo de recomendação recomenda produtos aos clientes com base nos itens que eles já compraram ou pelos quais mostraram interesse. O algoritmo Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] também é útil para análise da cesta básica. Para obter um exemplo de uma análise da cesta de compras, consulte [lição 3: Criando um cenário de cesta de compras &#40;Tutorial de mineração de dados intermediário&#41; ](../../tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md) no Tutorial de mineração de dados.  
  
 Modelos de associação são criados a partir de conjuntos de dados que contêm identificadores de casos individuais e de itens contidos em casos. Um grupo de itens em um caso é chamado de *conjunto de itens*. Um modelo de associação é formado por uma série de conjuntos de itens e regras que descrevem como esses itens são agrupados nos casos. As regras que o algoritmo identificar podem ser usadas para prever as prováveis compras futuras do cliente com base nos itens já existentes em seu carrinho de compras. O diagrama a seguir mostra uma série de regras em um conjunto de itens.  
  
 ![Um conjunto de regras para um modelo de associação](../media/association.gif "um conjunto de regras para um modelo de associação")  
  
 Como ilustra o diagrama, o algoritmo Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] pode potencialmente localizar muitas regras em um conjunto de dados. O algoritmo usa dois parâmetros, suporte e probabilidade, para descrever os conjuntos de itens e as regras que gera. Por exemplo, se X e Y representassem dois itens que poderiam estar em um carrinho de compras, o parâmetro de suporte seria o número de casos no conjunto de dados que contém a combinação dos itens X e Y. Ao usar o parâmetro de suporte em combinação com os parâmetros definidos pelo usuário, *MINIMUM_SUPPORT* e *MAXIMUM_SUPPORT* , o algoritmo controla o número de conjuntos de itens gerados. O parâmetro de probabilidade, também chamado de *confiança*, representa a fração de casos no conjunto de dados que contém X e que também contém Y. Ao usar o parâmetro de probabilidade combinado com o parâmetro *MINIMUM_PROBABILITY* , o algoritmo controla o número de regras geradas.  
  
## <a name="example"></a>Exemplo  
 A empresa [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] Cycle está redesenhando a funcionalidade de seu site. A meta do redesenho é aumentar a venda direta de produtos. Como a empresa registra cada venda em um banco de dados transacional, pode usar o algoritmo Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] para identificar conjuntos de produtos que tendem a ser comprados juntos. Ela pode então prever outros itens pelos o quais o cliente poderia interessar-se com base nos itens que já estão no carrinho de compras.  
  
## <a name="how-the-algorithm-works"></a>Como o algoritmo funciona  
 O algoritmo Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] atravessa um conjunto de dados para localizar itens que aparecem juntos em um caso. Em seguida, ele agrupa em conjuntos de itens todos os itens associados que aparecem, no mínimo, em diversos casos que são especificados pelo parâmetro *MINIMUM_SUPPORT* . Por exemplo, um conjunto de itens poderia ser "Mountain 200=Existing, Sport 100=Existing" e poderia ter um suporte de 710. Depois, o algoritmo gera as regras a partir dos conjuntos de itens. Essas regras são usadas para prever a presença de um item no banco de dados, de acordo com a presença de outros itens especificados que o algoritmo identifica como importante. Por exemplo, uma regra poderia ser "if Touring 1000=existing and Road bottle cage=existing, then Water bottle=existing" e ter a probabilidade de 0,812. Nesse exemplo, o algoritmo identifica que a presença no carrinho de compras do pneu Touring 1000 e do suporte para garrafa prevê que a garrafa de água também poderia estar no carrinho.  
  
 Para obter uma explicação mais detalhada do algoritmo e uma lista de parâmetros para personalizar seu comportamento e controlar os resultados no modelo de mineração, consulte [Referência técnica do algoritmo de associação da Microsoft](microsoft-association-algorithm-technical-reference.md).  
  
## <a name="data-required-for-association-models"></a>Dados requeridos para os modelos de associação  
 Ao preparar dados para usar em um modelo de regras de associação, é preciso entender os requisitos de um determinado algoritmo, incluindo a quantidade de dados necessária e como eles são usados.  
  
 Os requisitos de um modelo de regras de associação são:  
  
-   **Uma única coluna de chave** Cada modelo deve conter uma coluna de texto ou numérica que identifique unicamente cada registro. Não são permitidas chaves compostas.  
  
-   **Uma única coluna previsível** Um modelo de associação pode ter apenas uma coluna previsível. Geralmente, é a coluna de chave da tabela aninhada, como aquela arquivada, que lista os produtos que foram comprados. Os valores devem ser discretos ou diferenciados.  
  
-   **Colunas de entrada** . As colunas de entrada devem ser discretas. Normalmente, os dados de entrada do modelo de associação são mantidos em duas tabelas. Por exemplo, uma tabela poderia conter informações sobre o cliente enquanto outra tabela contém as compras feitas pelo cliente. Você pode inserir esses dados no modelo usando uma tabela aninhada. Para obter mais informações sobre tabelas aninhadas, consulte [Tabelas aninhadas &#40;Analysis Services – Mineração de Dados&#41;](nested-tables-analysis-services-data-mining.md).  
  
 Para obter informações mais detalhadas sobre os tipos de conteúdo e de dados com suporte pelos modelos de associação, consulte a seção Requisitos de [Referência técnica do algoritmo de associação da Microsoft](microsoft-association-algorithm-technical-reference.md).  
  
## <a name="viewing-an-association-model"></a>Exibindo um modelo de associação  
 Para explorar o modelo, você pode usar o **Visualizador de Associação da Microsoft**. Quando você exibir um modelo de associação, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] apresentará as correlações de ângulos diferentes para que você possa entender melhor as relações e as regras encontradas nos dados. O painel **Conjunto de Itens** do visualizador fornece uma análise detalhada das combinações, ou conjuntos de itens, mais comuns. O painel **Regras** apresenta uma lista de regras que foram generalizadas por meio dos dados, adiciona cálculos de probabilidade e classifica as regras por importância relativa. Com o Visualizador de Rede de Dependências, você pode explorar como se conectam itens diferentes. Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Cluster da Microsoft](browse-a-model-using-the-microsoft-cluster-viewer.md).  
  
 Para obter mais detalhes sobre qualquer dos conjuntos de itens ou das regras, você pode navegar pelo modelo no [Visualizador de Árvore de Conteúdo Genérica da Microsoft](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md). O conteúdo armazenado para o modelo inclui o suporte para cada conjunto de itens, uma pontuação para cada regra e outras estatísticas. Para obter mais informações, consulte [Mining Model Content for Association Models &#40;Analysis Services - Data Mining&#41;](mining-model-content-for-association-models-analysis-services-data-mining.md).  
  
## <a name="creating-predictions"></a>Criando previsões  
 Depois de processado o modelo, você pode usar as regras e os conjuntos de itens para fazer previsões. Em um modelo de associação, uma previsão indica qual item deveria aparecer mediante a presença do item especificado, além de poder incluir informações como probabilidade, suporte ou importância. Para obter exemplos de como criar consultas em um modelo de associação, consulte [Exemplos de consulta de um modelo associação](association-model-query-examples.md).  
  
 Para obter informações gerais sobre como criar uma consulta com base em um modelo de mineração de dados, consulte [Consultas de mineração de dados](data-mining-queries.md).  
  
## <a name="performance"></a>Desempenho  
 O processo de criação de conjuntos de itens e de contagem de correlações pode ser demorado. Embora o [!INCLUDE[msCoName](../../includes/msconame-md.md)] algoritmo regras de associação usa técnicas de otimização para economizar espaço e acelerar o processamento, você deve saber que os problemas de desempenho podem ocorrer sob as seguintes condições:  
  
-   O conjunto de dados é grande, com muitos itens individuais.  
  
-   O tamanho mínimo do conjunto de itens também é muito pequeno.  
  
 Para reduzir o tempo de processamento e a complexidade dos conjuntos de itens, convém tentar agrupar itens relacionados por categorias antes de analisar os dados.  
  
## <a name="remarks"></a>Remarks  
  
-   Não dá suporte ao uso de PMML para criar modelos de mineração.  
  
-   Dá suporte ao detalhamento.  
  
-   Suporta o uso de modelos de mineração OLAP.  
  
-   Suporta a criação de dimensões de mineração de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados &#40;Analysis Services – mineração de dados&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [Procurar um modelo usando o Visualizador de regras de associação da Microsoft](browse-a-model-using-the-microsoft-association-rules-viewer.md)   
 [Conteúdo do modelo de mineração para modelos de associação &#40; Analysis Services – mineração de dados &#41;](mining-model-content-for-association-models-analysis-services-data-mining.md)   
 [Referência técnica do algoritmo de associação da Microsoft](microsoft-association-algorithm-technical-reference.md)   
 [Exemplos de consulta de um modelo de associação](association-model-query-examples.md)  
  
  