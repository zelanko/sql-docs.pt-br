---
title: "Algoritmo de regressão logística da Microsoft | Microsoft Docs"
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
- logical regression algorithms [Analysis Services]
- algorithms [data mining]
- neural network algorithms [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 3dd54d07-1c3b-4b87-b7f0-b962ed8cf844
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0a62e3bad1e9bfcae6c929061000ebcc8d3b7af7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="microsoft-logistic-regression-algorithm"></a>Algoritmo Regressão Logística da Microsoft
  A regressão logística é uma técnica estatística conhecida, usada para modelar resultados binários.  
  
 Há várias implementações de regressão logística em pesquisa de estatísticas, usando técnicas de aprendizagem diferentes. O algoritmo Regressão Logística da [!INCLUDE[msCoName](../../includes/msconame-md.md)] foi implementado usando uma variação do algoritmo Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Este algoritmo compartilha muitas das qualidades de redes neurais mas é mais fácil treinar.  
  
 Uma vantagem da regressão logística é que o algoritmo é altamente flexível, aceitando qualquer tipo de entrada, e suporta diferentes tarefas analíticas:  
  
-   Use dados demográficos para fazer previsões sobre resultados, como risco de certa doença.  
  
-   Explore e pondere os fatores que contribuem com um resultado. Por exemplo, identifique os fatores que influenciam clientes a voltarem a uma loja.  
  
-   Classifique documentos, emails ou outros objetos que contêm muitos atributos.  
  
## <a name="example"></a>Exemplo  
 Considere um grupo de pessoas que tem informações demográficas parecidas e que compra produtos da empresa Adventure Works. Ao modelar os dados para relacioná-los a um resultado específico, como a compra de determinado produto, você poderá ver como informações demográficas contribuem para a probabilidade de alguém comprar o determinado produto.  
  
## <a name="how-the-algorithm-works"></a>Como o algoritmo funciona  
 A regressão logística é um método estatístico conhecido para determinar a contribuição de vários fatores para um par de resultados. A implementação da Microsoft usa uma rede neural modificada para modelar as relações entre entradas e resultados. O efeito de cada entrada no resultado é medido e as várias entradas são ponderadas no modelo finalizado. O nome regressão logística foi atribuído pelo fato de a curva de dados ser compactada usando uma transformação logística para minimizar o efeito de valores extremos. Para obter mais informações sobre a implementação e como personalizar o algoritmo, consulte [Referência técnica do algoritmo Regressão Logística da Microsoft](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md).  
  
## <a name="data-required-for-logistic-regression-models"></a>Dados necessários para modelos de regressão logística  
 Quando você prepara dados para serem usados no treinamento de um modelo de regressão logística, é preciso conhecer os requisitos de um determinado algoritmo, inclusive a quantidade de dados necessária e como os dados serão usados.  
  
 Os requisitos de um modelo de regressão logística são os seguintes:  
  
 **Uma única coluna de chave** Cada modelo deve conter uma coluna de texto ou numérica que identifique unicamente cada registro. Chaves compostas não são permitidas.  
  
 **Colunas de entrada** Cada modelo deve conter pelo menos uma coluna de entrada que tenha os valores que serão usados como fatores na análise. Você pode ter quantas colunas de entrada desejar, mas, dependendo do número de valores em cada coluna, a inclusão de colunas extras pode aumentar o tempo que leva para treinar o modelo.  
  
 **Pelo menos uma coluna previsível** O modelo deve conter pelo menos uma coluna previsível de qualquer tipo, incluindo dados numéricos contínuos. Os valores da coluna previsível também podem ser tratados como entradas no modelo ou você pode especificar que eles devem ser usados apenas para previsão. Não são permitidas tabelas aninhadas em colunas previsíveis, mas elas podem ser usadas como entradas.  
  
 Para obter informações mais detalhadas sobre os tipos de conteúdo e de dados aceitos por modelos de regressão logística, consulte a seção Requisitos de [Referência técnica do algoritmo Regressão Logística da Microsoft](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md).  
  
## <a name="viewing-a-logistic-regression-model"></a>Exibindo um modelo de regressão logística  
 Para explorar o modelo, você pode usar o Visualizador de Rede Neural da Microsoft ou o Visualizador de Árvore de Conteúdo Genérica da Microsoft.  
  
 Ao exibir o modelo usando o Visualizador de Rede Neural da Microsoft, o Analysis Services mostra os fatores que contribuem com um determinado resultado, classificados por importância. Você pode escolher um atributo e valores para comparar. Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Rede Neural da Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md).  
  
 Para obter mais informações, você pode navegar pelos detalhes do modelo usando o Visualizador de Árvore de Conteúdo Genérica da Microsoft. O conteúdo do modelo em um modelo de regressão logística inclui um nó marginal que mostra todas as entradas usadas para o modelo e as sub-redes dos atributos previsíveis. Para obter mais informações, consulte [Conteúdo do modelo de mineração para modelos de regressão logística &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md).  
  
## <a name="creating-predictions"></a>Criando previsões  
 Depois que o modelo foi treinado, você pode criar consultas para o conteúdo do modelo a fim de obter os coeficientes de regressão e outros detalhes ou pode usar o modelo para fazer previsões.  
  
-   Para obter informações gerais sobre como criar consultas com base em um modelo de mineração de dados, consulte [Consultas de mineração de dados](../../analysis-services/data-mining/data-mining-queries.md).  
  
-   Para obter exemplos de consultas em um modelo de regressão logística, consulte [Exemplos de consulta de modelo de clustering](../../analysis-services/data-mining/clustering-model-query-examples.md).  
  
## <a name="remarks"></a>Comentários  
  
-   Não suporta detalhamento. Isso acontece porque a estrutura dos nós do modelo de mineração não corresponde diretamente aos dados subjacentes.  
  
-   Não suporta a criação de dimensões de mineração de dados.  
  
-   Suporta o uso de modelos de mineração OLAP.  
  
-   Não dá suporte ao uso de PMML para criar modelos de mineração.  
  
## <a name="see-also"></a>Consulte também  
 [Conteúdo do modelo de mineração para modelos de regressão logística &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)   
 [Referência técnica do algoritmo de regressão logística de Microsoft](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)   
 [Exemplos de consulta de modelo de regressão logística](../../analysis-services/data-mining/logistic-regression-model-query-examples.md)  
  
  
