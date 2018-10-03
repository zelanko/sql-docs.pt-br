---
title: Algoritmo Microsoft Clustering | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- segmentation algorithms [Analysis Services]
- nearest neighbor [Data Mining]
- clustering [Data Mining]
- clusters [Analysis Services]
- relationships [Analysis Services], clusters
- algorithms [data mining]
- classification algorithms [Analysis Services]
- datasets [Analysis Services]
- clustering algorithms [Analysis Services]
ms.assetid: 92a1e67e-f46e-4960-99b2-4d20f6192fbd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b3b9d48c6bcdfd07599ded1b4a92955cc45abfec
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48195096"
---
# <a name="microsoft-clustering-algorithm"></a>Algoritmo Microsoft Clustering
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering é um algoritmo de segmentação fornecido pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. O algoritmo usa técnicas iterativas para agrupar casos em um conjunto de dados em clusters que contenham características semelhantes. Esses agrupamentos são úteis para explorar dados, identificando anomalias nos dados e criar previsões.  
  
 Modelos de clustering identificam as relações em um conjunto de dados que não podem ser derivados de forma lógica através de observação casual. Por exemplo, você pode discernir logicamente que pessoas que se vão para o trabalho de bicicleta normalmente não moram longe do local onde trabalham. Porém, o algoritmo pode encontrar outras características dos usuários de bicicleta que não são tão óbvias. No diagrama a seguir, o cluster A representa dados sobre pessoas que pretendem ir de carro para o trabalho, enquanto o cluster B representa dados sobre pessoas que pretendem ir de bicicleta para o trabalho.  
  
 ![Padrão de cluster tendências de comutador](../media/clustering-example.gif "padrão de tendências de comutador de Cluster")  
  
 O algoritmo de clustering difere dos demais algoritmos de mineração de dados, como o algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] , porque você não precisa designar uma coluna previsível para poder criar um modelo de clustering. O algoritmo de clustering treina o modelo estritamente a partir das relações existentes nos dados e a partir dos clusters que o algoritmo identifica.  
  
## <a name="example"></a>Exemplo  
 Considere um grupo de pessoas que compartilha informações demográficas similares e que compram produtos semelhantes da empresa [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] . Esse grupo de pessoas representa um cluster de dados. Podem existir vários desses clusters em um banco de dados. Observando as colunas que formam um cluster, é possível observar claramente como os registros em um conjunto de dados são relacionados entre si.  
  
## <a name="how-the-algorithm-works"></a>Como o algoritmo funciona  
 O algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering primeiro identifica as relações em um conjunto de dados e gera uma série de clusters com base nelas. Uma dispersão é uma maneira útil para representar visualmente como o algoritmo agrupa os dados, conforme mostrado no diagrama a seguir. A dispersão representa todos os caso no conjunto de dados, e cada caso é um ponto no gráfico. Os clusters agrupam pontos no gráfico e ilustram as relações que o algoritmo identifica.  
  
 ![Dispersão de casos em um conjunto de dados](../media/clustering-plot.gif "gráfico de dispersão de casos em um conjunto de dados")  
  
 Após definir primeiro os clusters, o algoritmo calcula como os mesmos representam satisfatoriamente agrupamentos dos pontos, e em seguida, tenta redefinir os agrupamentos para criar os clusters que melhor representem os dados. O algoritmo itera através desse processo até não poder mais melhorar os resultados pela redefinição dos clusters.  
  
 Você pode personalizar o modo como o algoritmo funciona ao selecionar uma técnica de clustering específica, limitando o número máximo de clusters ou alterando o valor de suporte necessário para criar um cluster. Para obter mais informações, consulte [Referência técnica do algoritmo Microsoft Clustering](microsoft-clustering-algorithm-technical-reference.md).  
  
## <a name="data-required-for-clustering-models"></a>Dados requeridos por agrupar modelos  
 Ao preparar dados para usar no treinamento de um modelo de clustering, é preciso entender os requisitos de um determinado algoritmo, incluindo a quantidade de dados necessária e como eles são usados.  
  
 Os requisitos de um modelo de clustering são os seguintes:  
  
-   **Uma única coluna de chave** Cada modelo deve conter uma coluna de texto ou numérica que identifique unicamente cada registro. Chaves compostas não são permitidas.  
  
-   **Colunas de entrada** Cada modelo deve conter pelo menos uma coluna de entrada contendo os valores que serão usados para criar os clusters. Você pode ter quantas colunas de entrada desejar, mas, dependendo do número de valores em cada coluna, a inclusão de colunas extras pode aumentar o tempo que leva para treinar o modelo.  
  
-   **Coluna previsível opcional** O algoritmo não precisa de uma coluna previsível para criar o modelo, mas você pode adicionar uma coluna previsível de praticamente qualquer tipo de dados. Os valores da coluna previsível podem ser tratados como entrada para o modelo de clustering ou você pode especificar que ela deve ser usada somente para previsão. Por exemplo, se você deseja prever a renda do cliente pelo clustering de dados demográficos, como região ou idade, você poderia especificar a receita como `PredictOnly` e adicionar todas as outras colunas, como região ou idade, como entradas.  
  
 Para obter informações mais detalhadas sobre os tipos de conteúdo e de dados com suporte pelos modelos de clustering, consulte a seção Requisitos de [Referência técnica do algoritmo Microsoft Clustering](microsoft-clustering-algorithm-technical-reference.md).  
  
## <a name="viewing-a-clustering-model"></a>Exibindo um modelo de clustering  
 Para explorar o modelo, você pode usar o **Visualizador de Cluster da Microsoft**. Quando você exibir um modelo de clustering, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mostrará os clusters em um diagrama que descreve as relações entre eles, além de fornecer um perfil detalhado de cada cluster, uma lista dos atributos que distinguem cada um deles e as características de todo o conjunto de dados de treinamento. Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Cluster da Microsoft](browse-a-model-using-the-microsoft-cluster-viewer.md).  
  
 Para obter mais detalhes, você pode navegar pelo modelo no [Visualizador de Árvore de Conteúdo Genérica da Microsoft](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md). O conteúdo armazenado para o modelo inclui a distribuição de todos os valores em cada nó, a probabilidade de cada cluster e outras informações. Para obter mais informações, consulte [Mining Model Content for Clustering Models &#40;Analysis Services - Data Mining&#41;](mining-model-content-for-clustering-models-analysis-services-data-mining.md).  
  
## <a name="creating-predictions"></a>Criando previsões  
 Depois que o modelo tiver sido treinado, os resultados serão armazenados como um conjunto de padrões, que você poderá explorar ou usar para realizar previsões.  
  
 Você pode criar consultas para retornar previsões sobre a adequação dos novos dados aos clusters que foram detectados ou para obter estatísticas descritivas sobre os clusters.  
  
 Para obter informações sobre como criar consultas com base em um modelo de mineração de dados, consulte [Consultas de mineração de dados](data-mining-queries.md). Para obter exemplos de como usar consultas com um modelo de clustering, consulte [Exemplos de consulta de modelo de clustering](clustering-model-query-examples.md).  
  
## <a name="remarks"></a>Comentários  
  
-   Suporta o uso de PMML (Predictive Model Markup Language) para criar modelos de mineração.  
  
-   Dá suporte ao detalhamento.  
  
-   Dá suporte ao uso de modelos de mineração OLAP e à criação de dimensões de mineração de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados &#40;Analysis Services - mineração de dados&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [Microsoft Clustering Algorithm Technical Reference](microsoft-clustering-algorithm-technical-reference.md)   
 [Conteúdo do modelo de mineração para modelos de Clustering &#40;Analysis Services - mineração de dados&#41;](mining-model-content-for-clustering-models-analysis-services-data-mining.md)   
 [Exemplos de consulta de modelo de clustering](clustering-model-query-examples.md)  
  
  
