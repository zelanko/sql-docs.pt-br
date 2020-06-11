---
title: Algoritmo Bayes do Microsoft Naive | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Bayesian classifiers
- algorithms [data mining]
- predictive modeling [Analysis Services]
- classification algorithms [Analysis Services]
- naive bayes algorithms [Analysis Services]
ms.assetid: 3b53e011-3b1a-4cd1-bdc2-456768ba31b5
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0c0fc3ae439f3502458e71fca1700302d745788a
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84521772"
---
# <a name="microsoft-naive-bayes-algorithm"></a>Algoritmo Naïve Bayes da Microsoft
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] algoritmo Naive Bayes é um algoritmo de classificação baseado em Bayes ' theorems e fornecido pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para uso na modelagem preditiva. O nome naïve no nome Naïve Bayes foi atribuído pelo fato de o algoritmo usar técnicas Bayesianas, mas não considerar dependências que possam existir. Portanto, suas suposições são consideradas ingênuas.

 Esse algoritmo é computacionalmente menos intenso de que outros algoritmos da [!INCLUDE[msCoName](../../includes/msconame-md.md)] e, portanto, é útil para gerar modelos de mineração rapidamente para descobrir as relações entre as colunas de entrada e as colunas previsíveis. Você pode usar esse algoritmo para realizar exploração de dados iniciais, e em seguida, aplicar os resultados para criar modelos de mineração adicionais com outros algoritmos que são computacionalmente mais intensos e mais precisos.

## <a name="example"></a>Exemplo
 Como estratégia promocional contínua, o departamento de marketing da empresa Adventure Works Cycle decidiu atingir clientes em potencial, enviando folhetos pelo correio. Para reduzir despesas, eles querem enviar folhetos apenas aos clientes que provavelmente irão responder. A empresa armazena as informações sobre dados demográficos e resposta a uma correspondência anterior em um banco de dados. Eles querem usar esses dados para ver como os dados demográficos, tais como idade e local, podem ajudar a prever a resposta a uma promoção, comparando clientes em potencial com clientes que têm características similares e que já compraram da empresa no passado. Especificamente, eles querem ver a diferença entre os clientes que compraram uma bicicleta e aqueles que não compraram.

 Usando o algoritmo Naive Bayes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] , o departamento de marketing pode prever rapidamente o resultado do perfil de um cliente específico e, portanto, determinar os clientes que mais provavelmente irão responder aos folhetos. Usando o Visualizador do Naive Bayes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], eles podem especificamente investigar visualmente as colunas de entrada que contribuem para respostas positivas aos folhetos.

## <a name="how-the-algorithm-works"></a>Como o algoritmo funciona
 O algoritmo Naive Bayes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] calcula a probabilidade do estado de cada coluna de entrada, uma vez proporcionado cada possível estado da coluna previsível.

 Para entender como isso funciona, use o Visualizador do Naive Bayes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] (conforme mostrado no gráfico a seguir) para explorar visualmente como o algoritmo distribui estados.

 ![Distribuição de naive bayes de estados](../media/naive-bayes.gif "Distribuição de naive bayes de estados")

 Aqui, o Visualizador Naive Bayes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] lista cada coluna de entrada no conjunto de dados e mostra como os estados de cada coluna são distribuídos, uma vez proporcionado cada estado da coluna previsível.

 Você poderia usar essa exibição do modelo para identificar as colunas de entrada que são importantes para diferenciar estados da coluna previsível.

 Por exemplo, na linha para Distância do Trabalho mostrada aqui, a distribuição de valores de entrada é visivelmente diferente para compradores versus não compradores. O que isso diz é que a entrada, Distância do Trabalho = 0-1 milhas, é um indicador potencial.

 O visualizador também fornece valores para as distribuições, para que você possa ver isso para os clientes que se deslocam até duas milhas para trabalhar, a probabilidade de ele comprar uma bicicleta é 0,387 e a de ele não comprar é 0,287. Nesse exemplo, o algoritmo usa as informações numéricas, derivadas das características do cliente (tais como a distância do trabalho), para prever se o cliente comprará a bicicleta.

 Para obter mais informações sobre como usar o Visualizador Naïve Bayes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] , consulte [Procurar um modelo usando o Visualizador Naïve Bayes da Microsoft](browse-a-model-using-the-microsoft-naive-bayes-viewer.md).

## <a name="data-required-for-naive-bayes-models"></a>Dados necessários para modelos Naive Bayes
 Ao preparar dados para usar no treinamento de um modelo Naive Bayes, você deve compreender os requisitos do algoritmo, incluindo a quantidade de dados necessária, e a forma que os dados são usados.

 Os requisitos para um modelo Naive Bayes são os seguintes:

-   **Uma única coluna de chave** Cada modelo deve conter uma coluna de texto ou numérica que identifique unicamente cada registro. Chaves compostas não são permitidas.

-   **Colunas de entrada** Em um modelo Naive Bayes, todas as colunas devem ser de colunas discretas ou discretizado. Para obter informações sobre colunas discretização, consulte [métodos de discretização &#40;mineração de dados&#41;](discretization-methods-data-mining.md).

     Além disso, também é importante assegurar que os atributos de entrada sejam independentes uns dos outros. Isto é particularmente importante quando você usa o modelo para previsão.

     A razão é que, se você usar duas colunas de dados que já estão intimamente relacionadas, o efeito seria multiplicar a influência dessas colunas, que podem obscurecer outros fatores que influenciam o resultado.

     De maneira recíproca, a capacidade de o algoritmo identificar correlações entre variáveis é útil quando você está explorando um modelo ou conjunto de dados, para identificar relações entre entradas.

-   **Pelo menos uma coluna previsível** O atributo previsível deve conter valores discretos ou diferenciados.

     Os valores da coluna previsível podem ser tratados como entradas. Esta prática pode ser útil quando você está explorando um novo conjunto de dados, para localizar relações entre as colunas.

## <a name="viewing-the-model"></a>Exibindo o modelo
 Para explorar o modelo, você pode usar o **Visualizador Naive Bayes da Microsoft**. O visualizador mostra a você como os atributos de entrada se relacionam com o atributo previsível. Ele também fornece um perfil detalhado para cada clusters, uma lista dos atributos que distinguem cada um dos clusters e as características de todo o conjunto de dados de treinamento. Para obter mais informações, consulte [Procurar um modelo usando o Visualizador Naïve Bayes da Microsoft](browse-a-model-using-the-microsoft-naive-bayes-viewer.md).

 Para obter mais detalhes, você pode navegar pelo modelo no [Visualizador de Árvore de Conteúdo Genérica da Microsoft &#40;Mineração de dados&#41;](../microsoft-generic-content-tree-viewer-data-mining.md). Para obter mais informações sobre o tipo de informação armazenada no modelo, consulte [Conteúdo do modelo de mineração para modelos Naive Bayes &#40;Analysis Services – Data Mining&#41;](mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md).

## <a name="making-predictions"></a>Fazendo previsões
 Depois que o modelo tiver sido treinado, os resultados serão armazenados como um conjunto de padrões, que você poderá explorar ou usar para realizar previsões.

 Você pode criar consultas para retornar previsões sobre como novos dados se relacionam com o atributo previsível ou pode recuperar estatísticas que descrevem as correlações encontradas pelo modelo.

 Para obter informações sobre como criar consultas com base em um modelo de mineração de dados, consulte [Consultas de mineração de dados](data-mining-queries.md). Para obter exemplos de como usar consultas com um modelo Naive Bayes, consulte [Exemplos de consulta de modelo Naïve Bayes](naive-bayes-model-query-examples.md).

## <a name="remarks"></a>Comentários

-   Suporta o uso de PMML (Predictive Model Markup Language) para criar modelos de mineração.

-   Dá suporte ao detalhamento.

-   Não suporta a criação de dimensões de mineração de dados.

-   Suporta o uso de modelos de mineração OLAP.

## <a name="see-also"></a>Consulte Também
 [Algoritmos de mineração de dados &#40;Analysis Services-Mineração de dados&#41;](data-mining-algorithms-analysis-services-data-mining.md) [seleção de recursos &#40;mineração de dados&#41;](feature-selection-data-mining.md) [exemplos de consulta de modelo de Naive Bayes](naive-bayes-model-query-examples.md) [mineração de conteúdo para modelos Naive Bayes &#40;Analysis Services-Mineração de dados&#41;](mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md) [referência técnica do algoritmo Microsoft Naive Bayes](microsoft-naive-bayes-algorithm-technical-reference.md)


