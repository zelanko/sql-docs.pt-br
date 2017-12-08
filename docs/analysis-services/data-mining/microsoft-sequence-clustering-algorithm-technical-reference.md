---
title: "Referência técnica do algoritmo msc | Microsoft Docs"
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
- MAXIMUM_SEQUENCE_STATES parameter
- MINIMUM_SUPPORT parameter
- MAXIMUM_STATES parameter
- sequence clustering algorithms [Analysis Services]
- CLUSTER_COUNT parameter
ms.assetid: 251c369d-6b02-4687-964e-39bf55c9b009
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9c624a1c14614d62c200e1f3afdfe5623a318853
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="microsoft-sequence-clustering-algorithm-technical-reference"></a>Referência técnica do algoritmo MSC
  O algoritmo MSC é um híbrido que usa a análise de cadeia Markov para identificar sequências ordenadas e combina os resultados dessa análise com técnicas de clustering para gerar clusters com base nas sequências e outros atributos no modelo. Este tópico descreve a implementação do algoritmo, como personalizá-lo e os requisitos especiais para modelos de clusterização de sequências.  
  
 Para obter mais informações gerais sobre o algoritmo, inclusive como navegar e consultar modelos de clusterização de sequência, consulte [Microsoft Sequence Clustering Algorithm](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md).  
  
## <a name="implementation-of-the-microsoft-sequence-clustering-algorithm"></a>Implementação do algoritmo do MSC  
 O modelo MSC usa modelos Markov para identificar sequências e determinar a probabilidade das sequências. Um modelo Markov é um gráfico direcionado que armazena as transições entre estados diferentes. O algoritmo MSC usa cadeias Markov de n-ordem, não um modelo Markov Oculto.  
  
 O número de ordens em uma cadeia Markov informa quantos estados são usados para determinar a probabilidade dos estados atuais. Em um modelo Markov de primeira ordem, a probabilidade do estado atual depende apenas do estado anterior. Em uma cadeia Markov de segunda ordem, a probabilidade de um estado depende dos dois estados anteriores e assim por diante. Para cada cadeia Markov,uma matriz de transição armazena as transições de cada combinação de estados. À medida que o comprimento da cadeia Markov aumenta, o tamanho da matriz também aumenta exponencialmente e ela se torna extremamente esparsa. O tempo de processamento também aumenta proporcionalmente.  
  
 Talvez seja útil visualizar a cadeia usando o exemplo da análise da sequência de cliques, que analisa as visitas às páginas da Web em um site. Cada usuário cria uma sequência longa de cliques para cada sessão. Quando você cria um modelo para analisar o comportamento do usuário em um site, o conjunto de dados usado para treinamento é uma sequência de URLs, convertida em um gráfico que inclui a contagem de todas as instâncias do mesmo caminho de cliques. Por exemplo, o gráfico contém a probabilidade de o usuário passar da página 1 para a página 2 (10%), a probabilidade de o usuário passar da página 1 para a página 3 (20%) etc. Quando você junta todos os caminhos e partes de caminhos possíveis, obtém um gráfico que pode ser muito maior e mais complexo do que qualquer caminho observado único.  
  
 Por padrão, o algoritmo MSC usa o método Maximização da Expectativa (ME) de clusterização. Para obter mais informações, consulte [Referência técnica do algoritmo Microsoft Clustering](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md).  
  
 Os destinos de clusterização são os atributos sequenciais e não sequenciais. Cada cluster é selecionado aleatoriamente com o uso de uma distribuição de probabilidade. Cada cluster tem uma cadeia Markov que representa o conjunto completo de caminhos e uma matriz que contém as transições de estado de sequência e as probabilidades. Com base na distribuição inicial, a regra de Bayes é usada para calcular a probabilidade de qualquer atributo, inclusive uma sequência, em um cluster específico.  
  
 O algoritmo MSC dá suporte à adição de atributos não sequenciais ao modelo. Isso significa que esses atributos adicionais são combinados aos atributos de sequência para criar clusters de casos com atributos similares, assim como ocorre em um modelo de clusterização típico.  
  
 Um modelo de clusterização de sequência tende a criar muito mais clusters do que um modelo de clusterização típico. Assim, o algoritmo MSC executa a *decomposição de cluster*para separar clusters com base nas sequências e em outros atributos.  
  
### <a name="feature-selection-in-a-sequence-clustering-model"></a>Seleção de recursos em um modelo de clusterização de sequência  
 A seleção de recursos não é invocada durante a criação de sequências; no entanto, ela se aplica no estágio de clusterização.  
  
|Tipo de modelo|Método de seleção de recursos|Comentários|  
|----------------|------------------------------|--------------|  
|Agrupamento de Sequência|Não usado|A seleção de recursos não é chamada; no entanto, você pode controlar o comportamento do algoritmo definindo o valor dos parâmetros MINIMUM_SUPPORT e MINIMUM_PROBABILIITY.|  
|Clustering|Pontuação de interesse|Embora o algoritmo de clusterização possa usar algoritmos discretos ou diferenciados, a pontuação de cada atributo é calculada como uma distância e é contínua; por isso, é usada a pontuação de interesse.|  
  
 Para obter mais informações, consulte [Feature Selection](http://msdn.microsoft.com/library/73182088-153b-4634-a060-d14d1fd23b70).  
  
### <a name="optimizing-performance"></a>Aperfeiçoando o desempenho  
 O algoritmo MSC dá suporte a várias maneiras de otimizar o processamento:  
  
-   Controlar o número de clusters gerado, definindo um valor para o parâmetro CLUSTER_COUNT.  
  
-   Reduzir o número de sequências incluídas como atributos, aumentando o valor do parâmetro MINIMUM_SUPPORT. Assim, as sequências raras são eliminadas.  
  
-   Reduzir a complexidade antes de processar o modelo, agrupando os atributos relacionados.  
  
 Em geral, é possível otimizar o desempenho de um modo de cadeia Markov de n- ordem de várias maneiras:  
  
-   Controlando o comprimento das sequências possíveis.  
  
-   Reduzindo o valor de n de forma programática.  
  
-   Armazenando apenas probabilidades que excedem um limite especificado.  
  
 Uma análise completa desses métodos está além do escopo deste tópico.  
  
## <a name="customizing-the-sequence-clustering-algorithm"></a>Personalizando o algoritmo MSC  
 O algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering dá suporte a parâmetros que afetam o comportamento, o desempenho e a precisão do modelo de mineração resultante. Também é possível modificar o comportamento do modelo completo definindo sinalizadores de modelagem que controlam a maneira como o algoritmo processa dados de treinamento.  
  
### <a name="setting-algorithm-parameters"></a>Definindo parâmetros de algoritmo  
 A tabela a seguir descreve os parâmetros que podem ser usados com o algoritmo MSC.  
  
 CLUSTER_COUNT  
 Especifica o número aproximado de clusters a serem criados pelo algoritmo. Se o número aproximado de clusters não pode ser criado a partir dos dados, o algoritmo cria o máximo de clusters possível. A definição do parâmetro CLUSTER_COUNT como 0 faz com que o algoritmo use heurística para determinar melhor o número de clusters a serem criados.  
  
 O padrão é 10.  
  
> [!NOTE]  
>  A especificação de um número diferente de zero atua como uma dica para o algoritmo, que prossegue com a meta de encontrar o número especificado, mas pode acabar encontrando mais ou menos.  
  
 MINIMUM_SUPPORT  
 Especifica o número mínimo de casos necessários para dar suporte à criação de um cluster por um atributo.  
  
 O padrão é 10.  
  
 MAXIMUM_SEQUENCE_STATES  
 Especifica o número de máximo de estados que uma sequência pode ter.  
  
 A definição desse valor com um número maior que 100 pode fazer com que o algoritmo crie um modelo que não fornece informações significativas.  
  
 O padrão é 64.  
  
 MAXIMUM_STATES  
 Especifica o número máximo de estados de um atributo não sequencial para os quais o algoritmo oferece suporte. Se o número de estados de um atributo não sequencial for maior que o número máximo de estados, o algoritmo usará os estados mais populares do atributo e tratará os estados restantes como **Ausentes**.  
  
 O padrão é 100.  
  
### <a name="modeling-flags"></a>Sinalizadores de modelagem  
 Os sinalizadores de modelagem a seguir são suportados para uso com o algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering.  
  
 NOT NULL  
 Indica que a coluna não pode conter um nulo. Um erro ocorrerá se o Analysis Services encontrar um valor nulo durante o treinamento do modelo.  
  
 Aplica-se à coluna da estrutura de mineração.  
  
 MODEL_EXISTENCE_ONLY  
 Significa que a coluna será tratada como se tivesse dois estados possíveis: **Missing** e **Existing**. Um valor nulo é tratado como **Missing** .  
  
 Aplica-se à coluna do modelo de mineração.  
  
 Para obter mais informações sobre o uso de valores Ausentes em modelos de mineração e como os valores ausentes afetam as pontuações de probabilidade, consulte [Valores ausentes &#40;Analysis Services – Mineração de dados&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md).  
  
## <a name="requirements"></a>Requisitos  
 A tabela de casos deve ter uma coluna de ID de caso. Opcionalmente, a tabela de casos pode conter outras colunas que armazenam atributos sobre o caso.  
  
 O algoritmo MSC exige informações de sequência, armazenadas como uma tabela aninhada. A tabela aninhada deve ter uma única coluna Key Sequence. Uma coluna **Key Sequence** pode conter qualquer tipo de dados que possa ser armazenado, inclusive tipos de dados de cadeia de caracteres, mas a coluna deve conter valores exclusivos para cada caso. Além disso, antes de processar o modelo, você deve assegurar que a tabela de casos e a tabela aninhada sejam classificadas em ordem crescente na chave que relaciona as tabelas.  
  
> [!NOTE]  
>  Se você criar um modelo que use o algoritmo MSC, mas não use uma coluna de sequência, o modelo resultante não conterá nenhuma sequência, mas simplesmente clusterizará casos com base em outros atributos incluídos no modelo.  
  
### <a name="input-and-predictable-columns"></a>Colunas de entrada e colunas previsíveis  
 O algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering dá suporte a colunas de entrada e colunas previsíveis específicas que são listadas na tabela a seguir. Para obter mais informações sobre o significado dos tipos de conteúdo quando usados em um modelo de mineração, consulte [Tipos de conteúdo &#40;Mineração de dados&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
|Coluna|Tipos de conteúdo|  
|------------|-------------------|  
|Atributo de entrada|Contínuo, cíclico, discreto, diferenciado, chave, Key Sequence, tabela e ordenado|  
|Atributo previsível|Contínuo, cíclico, discreto, diferenciado, tabela e ordenado|  
  
## <a name="remarks"></a>Comentários  
  
-   Use a função [PredictSequence &#40;DMX&#41;](../../dmx/predictsequence-dmx.md) para a Previsão de Sequências. Para obter mais informações sobre as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que dão suporte à Previsão de Sequência, consulte [Recursos com suporte nas edições do SQL Server 2012](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473).  
  
-   O algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] MSC não dá suporte ao uso de PMML para criar modelos de mineração.  
  
-   O algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering dá suporte ao detalhamento, ao uso de modelos de mineração OLAP e ao uso de dimensões de mineração de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Microsoft Sequence Clustering Algorithm](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)   
 [Exemplos de consulta de modelo de Clustering de sequência](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)   
 [Conteúdo do modelo de mineração para modelos de clustering de sequência &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)  
  
  
