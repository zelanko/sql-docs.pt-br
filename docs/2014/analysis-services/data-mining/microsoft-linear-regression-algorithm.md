---
title: Algoritmo de regressão linear da Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- algorithms [data mining]
- linear regression algorithms [Analysis Services]
- linear regression [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 50a4abb8-c0b0-4380-ba5e-c49b305b9d22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a855df4440f2c023380a97aa37e35047db27ebb9
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78174415"
---
# <a name="microsoft-linear-regression-algorithm"></a>Algoritmo Regressão Linear da Microsoft
  O algoritmo Regressão Linear da [!INCLUDE[msCoName](../../includes/msconame-md.md)] é uma variação do algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] que o ajuda a calcular uma relação linear entre uma variável dependente e uma independente e, depois, a usar aquela relação para previsão.

 A relação assume a forma de uma equação para uma linha que melhor represente uma série de dados. Por exemplo, a linha no diagrama a seguir é a melhor representação linear possível dos dados.

 ![Uma linha que modela um conjunto de dados](../media/linear-regression.gif "Uma linha que modela um conjunto de dados")

 Cada ponto de dados no diagrama tem um erro associado à sua distância da linha de regressão. Os coeficientes a e b na equação de regressão ajustam o ângulo e o local da linha de regressão. É possível obter a equação de regressão ajustando a e b até que a soma dos erros associados a todos os pontos atinja o menor número.

 Há outros tipos de regressão que usam diversas variáveis e também métodos não lineares de regressão. Porém, uma regressão linear é um método útil e conhecido para modelar uma resposta a uma alteração em alguns fatores subjacentes.

## <a name="example"></a>Exemplo
 É possível usar a regressão linear para determinar uma relação entre duas colunas contínuas. Por exemplo, você pode usar a regressão linear para computar uma linha de tendência de dados de fabricação ou de vendas. É possível também usar a regressão linear como um precursor para o desenvolvimento de modelos de mineração de dados mais complexos para avaliar relações entre colunas de dados.

 Apesar de haver muitas maneiras para se computar regressão linear sem a necessidade de ferramentas de mineração de dados, a vantagem de usar o algoritmo Regressão Linear da [!INCLUDE[msCoName](../../includes/msconame-md.md)] para esta tarefa é que todas as relações possíveis entre as variáveis são automaticamente computadas e testadas. Não é necessário selecionar um método de computação, como resolver para mínimos quadrados. Porém, a regressão linear pode simplificar muito as relações em cenários onde diversos fatores afetam o resultado.

## <a name="how-the-algorithm-works"></a>Como o algoritmo funciona
 O algoritmo Regressão Linear da [!INCLUDE[msCoName](../../includes/msconame-md.md)] é uma variação do algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Ao selecionar o algoritmo Regressão Linear da [!INCLUDE[msCoName](../../includes/msconame-md.md)] , é chamado um tipo especial de algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] , com parâmetros que restringem o comportamento do algoritmo e requerem determinados tipos de dados de entrada. Além disso, em um modelo de regressão linear, todo o conjunto de dados é usado para computar relações na passagem inicial, enquanto que um modelo de árvores de decisão divide os dados repetidamente em subconjuntos ou árvores menores.

## <a name="data-required-for-linear-regression-models"></a>Dados requeridos para modelos de regressão linear
 Ao preparar dados para usar em um modelo de regressão linear, você deve entender os requisitos para o algoritmo específico. Isso inclui a quantidade de dados necessária e a forma como os dados são usados. Os requisitos para este tipo de modelos são os seguintes:

-   **Uma única coluna de chave** Cada modelo deve conter uma coluna numérica ou de texto que identifique exclusivamente cada registro. Não são permitidas chaves compostas.

-   **Uma coluna previsível** Requer pelo menos uma coluna previsível. Você pode incluir diversos atributos previsíveis em um modelo, mas eles devem ser tipos de dados numéricos contínuos. Não é possível usar um tipo de dados datetime como um atributo previsível, mesmo que o armazenamento nativo dos dados seja numérico.

-   **Colunas de entrada** As colunas de entrada devem conter dados numéricos contínuos e receber o tipo de dados apropriado.

 Para obter mais informações sobre esse algoritmo, consulte [Referência técnica do algoritmo Regressão Linear da Microsoft](microsoft-linear-regression-algorithm-technical-reference.md).

## <a name="viewing-a-linear-regression-model"></a>Exibindo um modelo de regressão linear
 Para explorar o modelo, use o **Visualizador de Árvores da Microsoft**. A estrutura da árvore para um modelo de regressão linear é muito simples, com todas as informações sobre a equação de regressão contidas em um único nó. Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Árvores da Microsoft](browse-a-model-using-the-microsoft-tree-viewer.md).

 Se quiser obter mais detalhes sobre a equação, você também poderá exibir os coeficientes e outros detalhes usando o [Visualizador de Árvore de Conteúdo Genérica da Microsoft](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md).

 No caso de um modelo de regressão linear, o conteúdo do modelo inclui metadados, a fórmula de regressão e as estatísticas sobre a distribuição de valores de entrada. Para obter mais informações, consulte [Conteúdo do modelo de mineração para modelos de regressão linear &#40;Analysis Services – Data Mining&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md).

## <a name="creating-predictions"></a>Criando previsões
 Depois que o modelo foi processado, os resultados são armazenados como um conjunto de estatísticas, juntamente com a fórmula de regressão linear que pode ser usada para computar tendências futuras. Para obter exemplos de consultas a serem usadas com um modelo de regressão linear, consulte [Exemplos de consulta de modelo de regressão linear](linear-regression-model-query-examples.md).

 Para obter informações gerais sobre como criar consultas com base em modelos de mineração, consulte [Consultas de mineração de dados](data-mining-queries.md).

 Além de criar um modelo de regressão linear selecionando o algoritmo Regressão Linear da [!INCLUDE[msCoName](../../includes/msconame-md.md)] , se o atributo previsível for um tipo de dados numérico contínuo, você poderá criar um modelo de árvore de decisão que contenha regressões. Neste caso, o algoritmo irá dividir quando encontrar os pontos de separação apropriados, mas criará uma fórmula de regressão para algumas regiões de dados. Para obter mais informações sobre árvores de regressão em um modelo de árvores de decisão, consulte [Conteúdo do modelo de mineração para modelos da árvore de decisão &#40;Analysis Services – Mineração de dados&#41;](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md).

## <a name="remarks"></a>Comentários

-   Não dá suporte ao uso de PMML para criar modelos de mineração.

-   Não suporta a criação de dimensões de mineração de dados.

-   Dá suporte ao detalhamento.

-   Suporta o uso de modelos de mineração OLAP.

## <a name="see-also"></a>Consulte Também
 [Algoritmos de mineração de dados &#40;mineração de dados Analysis Services&#41;](data-mining-algorithms-analysis-services-data-mining.md) [do algoritmo regressão linear da Microsoft](microsoft-linear-regression-algorithm-technical-reference.md) [exemplos de consulta de modelo](linear-regression-model-query-examples.md) de regressão linear exemplo [de consultas de modelo de mineração de conteúdo para modelos de regressão linear &#40;Analysis Services-Data Mining&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)


