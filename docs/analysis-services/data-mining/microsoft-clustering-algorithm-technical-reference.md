---
title: "Referência técnica do algoritmo de cluster da Microsoft | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- clustering [Data Mining]
- MAXIMUM_INPUT_ATTRIBUTES parameter
- CLUSTER_SEED parameter
- MODELLING_CARDINALITY parameter
- MINIMUM_SUPPORT parameter
- STOPPING_TOLERANCE parameter
- MAXIMUM_STATES parameter
- SAMPLE_SIZE parameter
- CLUSTERING_METHOD parameter
- soft clustering [Data Mining]
- clustering algorithms [Analysis Services]
- CLUSTER_COUNT parameter
ms.assetid: ec40868a-6dc7-4dfa-aadc-dedf69e555eb
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c0c63e2966073fc045401febb16b1a350e94552c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="microsoft-clustering-algorithm-technical-reference"></a>Referência técnica do algoritmo Microsoft Clustering
  Esta seção explica a implementação do algoritmo de clustering [!INCLUDE[msCoName](../../includes/msconame-md.md)] , inclusive os parâmetros que podem ser usados para controlar o comportamento de modelos de clustering. Ela também fornece orientação sobre como melhorar o desempenho ao criar e processar modelos de clustering.  
  
 Para obter informações adicionais sobre como usar modelos de clustering, consulte os seguintes tópicos:  
  
-   [Conteúdo do modelo de mineração para modelos de clustering &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md)  
  
-   [Exemplos de consulta de modelo de clustering](../../analysis-services/data-mining/clustering-model-query-examples.md)  
  
## <a name="implementation-of-the-microsoft-clustering-algorithm"></a>Implementação do algoritmo do Microsoft Clustering  
 O algoritmo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering fornece dois métodos para criar clusters e atribuir pontos de dados aos clusters. O primeiro, o algoritmo *K-means* , é um método de cluster rígido. Isso significa que um ponto de dados pode pertencer somente a um cluster e que uma única probabilidade é calculada para a associação de cada ponto de dados nesse cluster. O segundo método, de *Maximização de Expectativa* (EM), é um método *de cluster flexível* . Isso significa que um ponto de dados sempre pertence a vários clusters e que uma probabilidade é calculada para cada combinação de ponto de dados e cluster.  
  
 Você pode escolher o algoritmo que será usado definindo o parâmetro *CLUSTERING_METHOD* . O método padrão de cluster é o EM evolutivo.  
  
### <a name="em-clustering"></a>Cluster EM  
 No cluster EM, o algoritmo refina de modo iterativo um modelo de clustering inicial para ajustar os dados e determina a probabilidade de um ponto de dados existir no cluster. O algoritmo termina o processo quando o modelo de probabilidade ajusta os dados. A função usada para determinar o ajuste é a probabilidade de log dos dados de acordo com o modelo.  
  
 Se clusters vazios forem gerados durante o processo ou se a associação de um ou mais clusters estiver abaixo de um determinado limite, os clusters com baixas populações serão propagados novamente em novos pontos e o algoritmo EM será executado mais uma vez.  
  
 Os resultados do método de cluster EM são probabilidades. Isso significa que cada ponto de dados pertence a todos os clusters, mas cada atribuição de um ponto de dados a um cluster tem uma probabilidade diferente. Como o método permite a sobreposição dos clusters, a soma dos itens de todos os clusters pode ultrapassar o total de itens do conjunto de treinamento. Nos resultados de modelo de mineração, as pontuações que indicam suporte são ajustadas para cumprir esse requisito.  
  
 O algoritmo EM é o algoritmo padrão usado nos modelos de clustering da Microsoft. Esse algoritmo é usado como o padrão porque oferece inúmeras vantagens em comparação ao cluster K-means:  
  
-   Requer no máximo uma verificação de banco de dados.  
  
-   Funciona apesar da memória limitada (RAM).  
  
-   Pode usar um cursor de somente avanço.  
  
-   Supera as abordagens de amostragem.  
  
 A implementação da Microsoft fornece duas opções: EM evolutivo e não evolutivo. Por padrão, no EM evolutivo, os primeiros 50.000 registros são usados para propagar a verificação inicial. Se esse processo for bem-sucedido, o modelo só usará esses dados. Se não for possível ajustar o modelo com 50.000 registros, serão lidos mais 50.000. No EM não evolutivo, o conjunto de dados inteiro é lido independentemente do tamanho. Esse método pode criar clusters mais precisos, mas os requisitos de memória podem ser significativos. Como o EM evolutivo atua em um buffer local, a iteração através dos dados é muito mais rápida e o algoritmo usa muito melhor o cache de memória da CPU do que o EM não evolutivo. Além disso, o EM evolutivo é três vezes mais rápido do que o EM não evolutivo, mesmo que seja possível ajustar os dados na memória principal. Na maioria dos casos, a melhoria do desempenho não diminui a qualidade do modelo completo.  
  
 Para obter um relatório técnico que descreve a implementação do EM no algoritmo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering, consulte [Scaling EM (Expectation Maximization) Clustering to Large Databases](http://go.microsoft.com/fwlink/?LinkId=45964)(Dimensionando clustering EM [Maximização de Expectativa] para bancos de dados grandes).  
  
### <a name="k-means-clustering"></a>Cluster K-Means  
 O cluster K-means é um método conhecido de atribuir a associação de clusters minimizando as diferenças entre os itens de um cluster e maximizando a distância entre os clusters. Em K-means, a palavra “means” (médio) refere-se ao *centroide* do cluster, que é um ponto de dados escolhido arbitrariamente e refinado de modo iterativo até representar a média real de todos os pontos de dados do cluster. O “K” refere-se a um número arbitrário de pontos que são usados para propagar o processo de cluster. O algoritmo K-means calcula as distâncias euclidianas quadradas entre os registros de dados de um cluster e o vetor que representa a média do cluster e é convertido em um conjunto final de K clusters quando essa soma atinge um valor mínimo.  
  
 O algoritmo K-means atribui cada ponto de dados exatamente a um cluster e não permite incertezas na associação. A associação em um cluster é expressa como uma distância do centroide.  
  
 Normalmente, o algoritmo K-means é usado para criar clusters de atributos contínuos, onde calcular a distância até o centro é simples. No entanto, a implementação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] adapta o método K-means para atributos de distinção de cluster usando probabilidades.  Para os atributos de distinção, a distância de um ponto de dados a partir de um cluster específico é calculada da seguinte maneira:  
  
 1 - P (ponto de dados, cluster)  
  
> [!NOTE]  
>  O algoritmo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering não expõe a função de distância usada no cálculo de K-means e as medidas de distância não estão disponíveis no modelo concluído. No entanto, é possível usar uma função de previsão para retornar um valor que corresponde à distância, onde a distância é calculada como a probabilidade de um ponto de dados pertencer ao cluster. Para obter mais informações, consulte [ClusterProbability &#40;DMX&#41;](../../dmx/clusterprobability-dmx.md).  
  
 O algoritmo K-means fornece dois métodos de amostragem do conjunto de dados: K-means não evolutivo, que carrega o conjunto de dados inteiro e faz uma passagem de cluster, ou K-means evolutivo, em que o algoritmo usa os primeiros 50.000 casos e lê mais casos somente se precisar de mais dados para atingir um bom ajuste do modelo aos dados.  
  
### <a name="updates-to-the-microsoft-clustering-algorithm-in-sql-server-2008"></a>Atualizações para o algoritmo Microsoft Clustering no SQL Server 2008  
 No SQL Server 2008, a configuração padrão do algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering foi alterada para usar o parâmetro interno, NORMALIZATION = 1. A normalização é executada usando-se estatísticas de pontuação z e pressupõe uma distribuição normal. A intenção dessa alteração feita no comportamento padrão é minimizar o efeito de atributos que podem ter grandes magnitudes e muitas exceções. No entanto, a normalização da pontuação z pode alterar os resultados do clustering em distribuições que não sejam normais (como distribuições uniformes). Para impedir a normalização e obter o mesmo comportamento do algoritmo de clustering K-means no SQL Server 2005, é possível usar a caixa de diálogo **Configurações de Parâmetro** para adicionar o parâmetro personalizado, NORMALIZATION, e definir o valor como 0.  
  
> [!NOTE]  
>  O parâmetro NORMALIZATION é uma propriedade interna do algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering, e não há suporte para ele. Em geral, o uso da normalização é recomendável em modelos de clustering para melhorar os resultados do modelo.  
  
## <a name="customizing-the-microsoft-clustering-algorithm"></a>Personalizando o algoritmo Microsoft Clustering  
 O algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering dá suporte a vários parâmetros que afetam o comportamento, o desempenho e a exatidão do modelo de mineração resultante.  
  
### <a name="setting-algorithm-parameters"></a>Definindo parâmetros de algoritmo  
 A tabela a seguir descreve os parâmetros que podem ser usados com o algoritmo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering. Esses parâmetros afetam o desempenho e a exatidão do modelo de mineração resultante.  
  
 CLUSTERING_METHOD  
 Especifica o método de clustering para o algoritmo a ser usado. Os métodos de cluster a seguir estão disponíveis:  
  
|ID|Método|  
|--------|------------|  
|1|EM evolutivo|  
|2|EM não evolutivo|  
|3|K-Means evolutivo|  
|4|K-means não escalonável.|  
  
 O padrão é 1 (EM evolutivo).  
  
 CLUSTER_COUNT  
 Especifica o número aproximado de clusters a serem criados pelo algoritmo. Se o número aproximado de clusters não pode ser criado a partir dos dados, o algoritmo cria o máximo de clusters possível. Quando CLUSTER_COUNT é definido como 0, o algoritmo usa heurísticos para determinar melhor o número de clusters a serem criados.  
  
 O padrão é 10.  
  
 CLUSTER_SEED  
 Especifica o número de propagação usado apenas para gerar clusters aleatoriamente para o estágio inicial de criação de modelo.  
  
 Ao alterar esse número, você pode alterar o modo de criação dos clusters iniciais e, em seguida, comparar os modelos criados com propagações diferentes. Se a propagação for alterada, mas os clusters encontrados não mudarem muito, o modelo pode ser considerado relativamente estável.  
  
 O padrão é 0.  
  
 MINIMUM_SUPPORT  
 Especifica o número mínimo de casos necessários para criar um cluster. Se o número de casos do cluster for menor que esse número, o cluster será tratado como vazio e descartado.  
  
 Se você definir este número muito alto, poderá perder clusters válidos.  
  
> [!NOTE]  
>  Se o EM for usado, que é o método de cluster padrão, alguns clusters poderão ter um valor de suporte inferior ao valor especificado. Isso acontece porque a associação de cada caso é avaliada em todos os clusters possíveis e, em alguns clusters, talvez exista apenas um suporte mínimo.  
  
 O padrão é 1.  
  
 MODELLING_CARDINALITY  
 Especifica o número de modelos de exemplo construídos durante o processo de clustering.  
  
 Reduzir o número de modelos candidatos pode melhorar o desempenho, mas pode acarretar a perda de alguns bons modelos candidatos.  
  
 O padrão é 10.  
  
 STOPPING_TOLERANCE  
 Especifica o valor usado para determinar quando a convergência é alcançada e o algoritmo terminou de criar o modelo. A convergência é alcançada quando a alteração geral nas probabilidades do cluster é menor do que a taxa do parâmetro STOPPING_TOLERANCE dividida pelo tamanho do modelo.  
  
 O padrão é 10.  
  
 SAMPLE_SIZE  
 Especifica o número de casos que o algoritmo usará em cada passagem se o parâmetro CLUSTERING_METHOD for definido como um dos métodos de cluster evolutivo. A definição do parâmetro SAMPLE_SIZE como 0 fará com que todo o conjunto de dados seja clusterizado em uma única passagem. Carregar o conjunto de dados inteiro em uma única passagem pode causar problemas de memória e de desempenho.  
  
 O padrão é 50000.  
  
 MAXIMUM_INPUT_ATTRIBUTES  
 Especifica o número máximo de atributos de entrada que o algoritmo pode manipular antes de invocar a seleção de recurso. A definição deste valor como 0 especifica que não há um número máximo de atributos.  
  
 O aumento do número de atributos pode afetar o desempenho significativamente.  
  
 O padrão é 255.  
  
 MAXIMUM_STATES  
 Especifica o número máximo de estados de atributo para os quais o algoritmo dá suporte. Se um atributo tiver mais estados que o valor máximo, o algoritmo usará os estados mais populares e ignorará os demais estados.  
  
 O aumento do número de estados pode afetar o desempenho significativamente.  
  
 O padrão é 100.  
  
### <a name="modeling-flags"></a>Sinalizadores de modelagem  
 O algoritmo dá suporte aos seguintes sinalizadores de modelagem. Você define sinalizadores de modelagem ao criar a estrutura de mineração ou o modelo de mineração. Os sinalizadores de modelagem especificam como os valores de cada coluna são controlados durante a análise.  
  
|Sinalizador de modelagem|Description|  
|-------------------|-----------------|  
|MODEL_EXISTENCE_ONLY|A coluna será tratada como tendo dois estados possíveis: Ausente e Existente. Nulo é um valor ausente.<br /><br /> Aplica-se à coluna de modelo de mineração.|  
|NOT NULL|A coluna não pode conter um valor nulo. Um erro ocorrerá se o Analysis Services encontrar um valor nulo durante o treinamento do modelo.<br /><br /> Aplica-se à coluna de estrutura de mineração.|  
  
## <a name="requirements"></a>Requisitos  
 Um modelo de clustering deve conter uma coluna de chave e colunas de entrada. Você também pode definir colunas de entrada como sendo previsíveis. As colunas definidas como **Somente Previsão** não são usadas para criar clusters. A distribuição desses valores nos clusters é calculada após a criação dos clusters.  
  
### <a name="input-and-predictable-columns"></a>Colunas de entrada e colunas previsíveis  
 O algoritmo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering dá suporte a colunas de entrada e colunas previsíveis específicas que são listadas na tabela a seguir. Para obter mais informações sobre o significado dos tipos de conteúdo quando usados em um modelo de mineração, consulte [Tipos de conteúdo &#40;Mineração de dados&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
|Coluna|Tipos de conteúdo|  
|------------|-------------------|  
|Atributo de entrada|Contínuo, cíclico, discreto, diferenciado, chave, tabela, ordenado|  
|Atributo previsível|Contínuo, cíclico, discreto, diferenciado, tabela, ordenado|  
  
> [!NOTE]  
>  Os tipos de conteúdo Cíclico e Ordenado têm suporte, mas o algoritmo os trata como valores discretos e não executa processamento especial.  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmo Microsoft Clustering](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)   
 [Exemplos de consulta de modelo de clustering](../../analysis-services/data-mining/clustering-model-query-examples.md)   
 [Conteúdo do modelo de mineração para modelos de clustering &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md)  
  
  

