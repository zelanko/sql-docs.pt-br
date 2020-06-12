---
title: Exemplos de consulta de modelo de clustering | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- clustering [Data Mining]
- content queries [DMX]
- clustering algorithms [Analysis Services]
ms.assetid: bf2ba332-9bc6-411a-a3af-b919c52432c8
author: minewiskan
ms.author: owend
ms.openlocfilehash: fe12b82ce2d237acd060b1e387e7a6dfbf958851
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84524152"
---
# <a name="clustering-model-query-examples"></a>Exemplos de consulta de modelo de clustering
  Ao criar uma consulta em um modelo de mineração de dados, é possível recuperar metadados sobre o modelo ou criar uma consulta de conteúdo que forneça detalhes sobre os padrões descobertos na análise. Se preferir, crie uma consulta de previsão, que usa os padrões do modelo para fazer previsões para os novos dados. Cada tipo de consulta fornece informações diferentes. Por exemplo, uma consulta de conteúdo pode fornecer detalhes adicionais sobre os clusters encontrados, enquanto uma consulta de previsão pode informar a qual cluster um novo ponto de dados provavelmente pertence.  
  
 Esta seção explica como criar consultas para modelos baseados no algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering.  
  
 **Consultas de conteúdo**  
  
 [Obtendo metadados do modelo usando DMX](#bkmk_Query1)  
  
 [Recuperando metadados do modelo do conjunto de linhas de esquema](#bkmk_Query2)  
  
 [Retornando um cluster ou uma lista de clusters](#bkmk_Query3)  
  
 [Retornando atributos para um cluster](#bkmk_Query4)  
  
 [Retornando um perfil de cluster por meio de procedimentos armazenados do sistema](#bkmk_Query5)  
  
 [Localizando fatores de distinção para um cluster](#bkmk_Query6)  
  
 [Retornando casos que pertencem a um cluster](#bkmk_Query7)  
  
 **Consultas de previsão**  
  
 [Prevendo resultados de um modelo de clustering](#bkmk_Query8)  
  
 [Determinando a associação do cluster](#bkmk_Query9)  
  
 [Retornando todos os possíveis clusters com probabilidade e distância](#bkmk_Query10)  
  
##  <a name="finding-information-about-the-model"></a><a name="bkmk_top2"></a> Localizando informações sobre o modelo  
 Todos os modelos de mineração expõem o conteúdo captado pelo algoritmo de acordo com um esquema padronizado, o conjunto de linhas do esquema do modelo de mineração. Você pode criar consultas para o conjunto de linhas de esquema de modelo de mineração usando instruções DMX. No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], você também pode consultar os conjuntos de linhas de esquema diretamente como tabelas do sistema.  
  
 [Retornar ao início](#bkmk_top2)  
  
###  <a name="sample-query-1-getting-model-metadata-by-using-dmx"></a><a name="bkmk_Query1"></a>Exemplo de consulta 1: obtendo metadados de modelo usando DMX  
 A consulta a seguir retorna os metadados básicos do modelo de clustering, `TM_Clustering`, que você criou no Tutorial de mineração de dados básico. Os metadados disponíveis no nó pai de um modelo de clustering incluem o nome do modelo, o banco de dados onde o modelo é armazenado e o número de nós filho do modelo. Esta consulta usa uma consulta de conteúdo DMX para recuperar os metadados do nó pai do modelo:  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY], NODE_DESCRIPTION  
FROM TM_Clustering.CONTENT  
WHERE NODE_TYPE = 1  
```  
  
> [!NOTE]  
>  É necessário colocar o nome na coluna, CHILDREN_CARDINALITY, entre colchetes para diferenciá-lo da palavra-chave reservada MDX do mesmo nome.  
  
 Resultados do exemplo:  
  
|||  
|-|-|  
|MODEL_CATALOG|TM_Clustering|  
|MODEL_NAME|Adventure Works DW|  
|NODE_CAPTION|Cluster Model|  
|NODE_SUPPORT|12939|  
|CHILDREN_CARDINALITY|10|  
|NODE_DESCRIPTION|Tudo|  
  
 Para obter uma definição do que essas colunas significam em um modelo de clustering, consulte [Conteúdo do modelo de mineração para modelos de clustering &#40;Analysis Services – Data Mining&#41;](mining-model-content-for-clustering-models-analysis-services-data-mining.md).  
  
 [Retornar ao início](#bkmk_top2)  
  
###  <a name="sample-query-2-retrieving-model-metadata-from-the-schema-rowset"></a><a name="bkmk_Query2"></a>Exemplo de consulta 2: Recuperando metadados de modelo do conjunto de linhas de esquema  
 É possível consultar o conjunto de linhas de esquema de mineração de dados para encontrar as mesmas informações retornadas em uma consulta de conteúdo DMX. No entanto, o conjunto de linhas de esquema fornece algumas colunas adicionais. Essas colunas incluem os parâmetros usados quando o modelo foi criado, a data e a hora em que o modelo foi processado pela última vez e o proprietário do modelo.  
  
 O exemplo a seguir retorna a data em que o modelo foi criado, modificado e processado pela última vez, além dos parâmetros de cluster usados para criar o modelo e o tamanho do conjunto de treinamento. Essas informações podem ser úteis para documentar o modelo ou para determinar quais opções de clustering foram usadas para criar um modelo existente.  
  
```  
SELECT MODEL_NAME, DATE_CREATED, LAST_PROCESSED, PREDICTION_ENTITY, MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_Clustering'  
```  
  
 Resultados do exemplo:  
  
|||  
|-|-|  
|MODEL_NAME|TM_Clustering|  
|DATE_CREATED|10/12/2007 7:42:51 PM|  
|LAST_PROCESSED|10/12/2007 8:09:54 PM|  
|PREDICTION_ENTITY|Bike Buyer|  
|MINING_PARAMETERS|CLUSTER_COUNT = 10<br /><br /> CLUSTER_SEED = 0<br /><br /> CLUSTERING_METHOD = 1<br /><br /> MAXIMUM_INPUT_ATTRIBUTES = 255<br /><br /> MAXIMUM_STATES = 100<br /><br /> MINIMUM_SUPPORT = 1<br /><br /> MODELLING_CARDINALITY = 10,<br /><br /> SAMPLE_SIZE = 50000,<br /><br /> STOPPING_TOLERANCE = 10|  
  
 [Retornar ao início](#bkmk_top2)  
  
## <a name="finding-information-about-clusters"></a>Localizando informações sobre clusters  
 As consultas de conteúdo mais úteis sobre modelos de clustering geralmente retornam o mesmo tipo de informação que você pode procurar por meio do **Visualizador de Cluster**. Isto inclui perfis de cluster, características de cluster e distinção de cluster. Esta seção fornece exemplos de consultas que recuperam essas informações.  
  
###  <a name="sample-query-3-returning-a-cluster-or-list-of-clusters"></a><a name="bkmk_Query3"></a> Exemplo de consulta 3: Retornando um cluster ou lista de clusters  
 Como todos os clusters têm um tipo de nó 5, é possível recuperar facilmente uma lista de clusters consultando o conteúdo do modelo apenas para os nós desse tipo. Você também pode filtrar os nós que são retornados pela probabilidade ou pelo suporte, como mostra este exemplo.  
  
```  
SELECT NODE_NAME, NODE_CAPTION ,NODE_SUPPORT, NODE_DESCRIPTION  
FROM TM_Clustering.CONTENT  
WHERE NODE_TYPE = 5 AND NODE_SUPPORT > 1000  
```  
  
 Resultados do exemplo:  
  
|||  
|-|-|  
|NODE_NAME|002|  
|NODE_CAPTION|Cluster 2|  
|NODE_SUPPORT|1649|  
|NODE_DESCRIPTION|English Education=Graduate Degree , 32 <=Age <=48 , Number Cars Owned=0 , 35964.0771121808 <=Yearly Income <=97407.7163393957 , English Occupation=Professional , Commute Distance=2-5 Miles , Region=North America , Bike Buyer=1 , Number Children At Home=0 , Number Cars Owned=1 , Commute Distance=0-1 Miles , English Education=Bachelors , Total Children=1 , Number Children At Home=2 , English Occupation=Skilled Manual , Marital Status=S , Total Children=0 , House Owner Flag=0 , Gender=F , Total Children=2 , Region=Pacific|  
  
 Os atributos que definem o cluster podem ser encontrados em duas colunas no conjunto de linhas de esquema de mineração de dados.  
  
-   A coluna NODE_DESCRIPTION contém uma lista de atributos separados por vírgula. Observe que a lista de atributos pode ser abreviada para fins de exibição.  
  
-   A tabela aninhada na coluna NODE_DISTRIBUTION contém a lista completa de atributos do cluster. Se o cliente não suportar conjuntos de linhas hierárquicos, é possível retornar a tabela aninhada adicionando a palavra-chave FLATTENED antes da lista da coluna SELECT. Para obter mais informações sobre o uso da palavra-chave FLATTENED, consulte [SELECT FROM &#60;modelo&#62; CONTENT &#40;DMX&#41;](/sql/dmx/select-from-model-dimension-content-dmx).  
  
 [Retornar ao início](#bkmk_top2)  
  
###  <a name="sample-query-4-returning-attributes-for-a-cluster"></a><a name="bkmk_Query4"></a> Exemplo de consulta 4: Retornando atributos para um cluster  
 Para cada cluster, o **Visualizador de Cluster** exibe um perfil que lista os atributos e seus valores. O visualizador também exibe um histograma que mostra a distribuição de valores para toda a população de casos do modelo. Se estiver procurando o modelo no visualizador, copie o histograma da Legenda de Mineração e cole-o no Excel ou em um documento do Word. Você também pode usar o painel Características do Cluster do visualizador para comparar graficamente os atributos de clusters diferentes.  
  
 No entanto, se for necessário obter valores para mais de um cluster de uma vez, é mais fácil consultar o modelo. Por exemplo, ao consultar o modelo, você pode perceber que os dois primeiros clusters diferem em um atributo, `Number Cars Owned`. Desse modo, você deve extrair os valores de cada cluster.  
  
```  
SELECT TOP 2 NODE_NAME,   
(SELECT ATTRIBUTE_VALUE, [PROBABILITY] FROM NODE_DISTRIBUTION WHERE ATTRIBUTE_NAME = 'Number Cars Owned')  
AS t  
FROM [TM_Clustering].CONTENT  
WHERE NODE_TYPE = 5  
```  
  
 A primeira linha do código especifica que você quer somente dois primeiros clusters.  
  
> [!NOTE]  
>  Por padrão, os clusters são ordenados por suporte. Desse modo, a coluna NODE_SUPPORT pode ser omitida.  
  
 A segunda linha do código adiciona uma instrução de subseleção que retorna somente algumas colunas da coluna da tabela aninhada. Além disso, ela restringe as linhas da tabela aninhada às linhas relacionadas ao atributo de destino, `Number Cars Owned`. Para simplificar a exibição, a tabela aninhada possui alias.  
  
> [!NOTE]  
>  A coluna da tabela aninhada, `PROBABILITY`, deve ficar entre colchetes porque ela também é o nome de uma palavra-chave MDX reservada.  
>   
>  Resultados do exemplo:  
  
|NODE_NAME|T.ATTRIBUTE_VALUE|T.PROBABILITY|  
|----------------|------------------------|-------------------|  
|001|2|0.829207754|  
|001|1|0.109354156|  
|001|3|0.034481552|  
|001|4|0.013503302|  
|001|0|0.013453236|  
|001|Ausente|0|  
|002|0|0.576980023|  
|002|1|0.406623939|  
|002|2|0.016380082|  
|002|3|1,60E-05|  
|002|4|0|  
|002|Ausente|0|  
  
 [Retornar ao início](#bkmk_top2)  
  
###  <a name="sample-query-5-return-a-cluster-profile-using-system-stored-procedures"></a><a name="bkmk_Query5"></a> Exemplo de consulta 5: Retornar um perfil de cluster usando procedimentos armazenados do sistema  
 Para simplificar, em vez de gravar suas próprias consultas usando DMX, você também pode chamar os procedimentos armazenados de sistema que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa para trabalhar com clusters. O exemplo a seguir ilustra como é possível usar os procedimentos armazenados internos para retornar o perfil de um cluster com ID 002.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterProfiles('TM_Clustering", '002',0.0005  
```  
  
 Similarmente, é possível usar um procedimento armazenado de sistema para retornar as características de um cluster específico, como mostra o exemplo a seguir:  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('TM_Clustering", '009',0.0005  
```  
  
 Resultados do exemplo:  
  
|Atributos|Valores|Frequência|Suporte|  
|----------------|------------|---------------|-------------|  
|Number Children at Home|0|0.999999829076798|899|  
|Região|América do Norte|0.999852875241508|899|  
|Total de Filhos|0|0.993860958572323|893|  
  
> [!NOTE]  
>  Os procedimentos armazenados do sistema de mineração de dados são para uso interno e a [!INCLUDE[msCoName](../../includes/msconame-md.md)] reserva-se o direito de alterá-los conforme necessário. Para uso em produção, é recomendável criar consultas por meio de DMX, AMO ou XMLA.  
  
 [Retornar ao início](#bkmk_top2)  
  
###  <a name="sample-query-6-find-discriminating-factors-for-a-cluster"></a><a name="bkmk_Query6"></a> Exemplo de consulta 6: Localizar fatores de distinção para um cluster  
 A guia **Distinção de Cluster** do **Visualizador de Cluster** permite que você compare com facilidade um cluster com outro ou um cluster com todos os casos restantes (o complemento do cluster).  
  
 No entanto, criar consultas para retornar essas informações pode ser complexo e talvez seja necessário algum processamento adicional no cliente para armazenar os resultados temporários e comparar os resultados de duas ou mais consultas. Para simplificar, você pode usar os procedimentos armazenados de sistema.  
  
 A consulta a seguir retorna uma única tabela que indica os principais fatores de distinção entre os dois clusters que têm IDs de nó 009 e 007. Os atributos com valores positivos favorecem o cluster 009, enquanto os atributos com valores negativos favorecem o cluster 007.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('TM_Clustering','009','007',0.0005,true)  
```  
  
 Resultados do exemplo:  
  
|Atributos|Valores|Pontuação|  
|----------------|------------|-----------|  
|Região|América do Norte|100|  
|Ocupação em Inglês|Skilled Manual|94.9003803898654|  
|Região|Europa|-72.5041051379789|  
|Ocupação em Inglês|Manual|-69.6503163202722|  
  
 Estas são as mesmas informações apresentadas no gráfico do visualizador de **Distinção de Cluster** se você selecionar Cluster 9 na primeira lista suspensa e Cluster 7 na segunda lista suspensa. Para comparar o cluster 9 com seu complemento, use a cadeia de caracteres vazia no segundo parâmetro, como mostra o exemplo a seguir:  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('TM_Clustering','009','',0.0005,true)  
```  
  
> [!NOTE]  
>  Os procedimentos armazenados do sistema de mineração de dados são para uso interno e a [!INCLUDE[msCoName](../../includes/msconame-md.md)] reserva-se o direito de alterá-los conforme necessário. Para uso em produção, é recomendável criar consultas por meio de DMX, AMO ou XMLA.  
  
 [Retornar ao início](#bkmk_top2)  
  
###  <a name="sample-query-7-returning-cases-that-belong-to-a-cluster"></a><a name="bkmk_Query7"></a> Exemplo de consulta 7: Retornando casos que pertencem a um cluster  
 Se o detalhamento estiver habilitado no modelo de mineração, você pode criar consultas que retornam informações detalhadas sobre os casos usados no modelo. Além disso, se o drillthrough tiver sido habilitado na estrutura de mineração, será possível incluir colunas da estrutura subjacente usando a função [StructureColumn &#40;DMX&#41;](/sql/dmx/structurecolumn-dmx).  
  
 O exemplo a seguir retorna duas colunas que foram usadas no modelo (Idade e Região) e mais uma coluna (Nome) que não foi usada no modelo. A consulta só retorna casos que foram classificados no Cluster 1.  
  
```  
SELECT [Age], [Region], StructureColumn('First Name')  
FROM [TM_Clustering].CASES  
WHERE IsInNode('001')  
```  
  
 Para retornar os casos que pertencem a um cluster, é necessário conhecer a ID do cluster. Você pode obter a ID do cluster navegando no modelo em um dos visualizadores. Se preferir, renomeie um cluster para facilitar a referência e, em seguida, use o nome em vez de um número de ID. No entanto, lembre-se de que os nomes atribuídos a um cluster serão perdidos se o modelo for reprocessado.  
  
 [Retornar ao início](#bkmk_top2)  
  
## <a name="making-predictions-using-the-model"></a>Fazendo predições com o modelo  
 Embora o clustering normalmente seja usado para descrever e entender dados, a implementação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] também permite que você faça previsões sobre associação do cluster e retorne probabilidades associadas à previsão. Esta seção fornece exemplos de como criar consultas de previsão em modelos de clustering. Você pode fazer previsões para vários casos, especificando uma fonte de dados tabular, ou fornecer novos valores de uma vez criando uma consulta singleton. Para deixar claros os exemplos, todas as consultas desta seção são singleton.  
  
 Para obter mais informações sobre como criar consultas de previsão usando DMX, consulte [interfaces de consulta de mineração de dados](data-mining-query-tools.md).  
  
 [Retornar ao início](#bkmk_top2)  
  
###  <a name="sample-query-8-predicting-outcomes-from-a-clustering-model"></a><a name="bkmk_Query8"></a> Exemplo de consulta 8: Prevendo resultados de um modelo de clustering  
 Se o modelo de clustering criado tiver um atributo previsível, use-o para fazer previsões sobre os resultados. No entanto, o modelo manipula o atributo previsível de modo diferente, dependendo da definição da coluna previsível com `Predict` ou `PredictOnly`. Se você definir o uso da coluna como `Predict`, os valores desse atributo serão adicionados ao modelo de clustering e aparecerão como atributos no modelo acabado. Porém, se você definir o uso da coluna como `PredictOnly`, os valores não serão usados para criar clusters. Em vez disso, quando o modo for concluído, o algoritmo de cluster criará novos valores para o atributo `PredictOnly` com base nos clusters aos quais cada caso pertence.  
  
 A consulta a seguir fornece um único caso novo para o modelo, onde as únicas informações sobre o caso são a idade e o sexo. A instrução SELECT especifica o par atributo/valor previsível de seu interesse e a função [PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx) informa a probabilidade de um caso com esses atributos ter o resultado planejado.  
  
```  
SELECT  
  [TM_Clustering].[Bike Buyer], PredictProbability([Bike Buyer],1)  
FROM  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender]) AS t  
```  
  
 Exemplo dos resultados quando o uso é definido como `Predict`:  
  
|Bike Buyer|Expression|  
|----------------|----------------|  
|1|0.592924735740338|  
  
 Exemplo dos resultados quando o uso é definido como `PredictOnly` e o modelo é reprocessado:  
  
|Bike Buyer|Expression|  
|----------------|----------------|  
|1|0.55843544003102|  
  
 Neste exemplo, a diferença no modelo não é significante. No entanto, às vezes pode ser importante detectar diferenças a distribuição real dos valores e o que é previsto pelo modelo. A guia [PredictCaseLikelihood &#40;DMX&#41;](/sql/dmx/predictcaselikelihood-dmx) é útil neste cenário porque informa a probabilidade de um caso no modelo em questão.  
  
 O número que é retornado pela função PredictCaseLikelihood é uma probabilidade e, portanto, sempre está entre 0 e 1, com o valor 0,5 representando um resultado aleatório. Desse modo, uma pontuação inferior a 0,5 indica que o caso previsto é improvável para o modelo e uma pontuação superior a 0,5 indica que o caso previsto é mais provável para se ajustar ao modelo.  
  
 Por exemplo, a consulta a seguir retorna dois valores que caracterizam a probabilidade de um novo caso de exemplo. O valor não normalizado representa a probabilidade para o modelo atual. Quando a palavra-chave NORMALIZED é usada, a pontuação de probabilidade retornada pela função é ajustada dividindo-se a “probabilidade com o modelo” pela “probabilidade sem o modelo”.  
  
```  
SELECT  
PredictCaseLikelihood(NORMALIZED) AS [NormalizedValue], PredictCaseLikelihood(NONNORMALIZED) AS [NonNormalizedValue]  
FROM  
  [TM_Clustering_PredictOnly]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender]) AS t  
```  
  
 Resultados do exemplo:  
  
|NormalizedValue|NonNormalizedValue|  
|---------------------|------------------------|  
|5,56438372679893E-11|8,65459953145182E-68|  
  
 Observe que os números nesses resultados são expressos em notação científica.  
  
 [Retornar ao início](#bkmk_top2)  
  
###  <a name="sample-query-9-determining-cluster-membership"></a><a name="bkmk_Query9"></a> Exemplo de consulta 9: Determinando a associação do cluster  
 Este exemplo usa a função [Cluster &#40;DMX&#41;](/sql/dmx/cluster-dmx) para retornar o cluster ao qual o novo caso provavelmente pertence e usa a função [ClusterProbability &#40;DMX&#41;](/sql/dmx/clusterprobability-dmx) para retornar a probabilidade de associação nesse cluster.  
  
```  
SELECT Cluster(), ClusterProbability()  
FROM  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender],  
  'S' AS [Marital Status]) AS t  
```  
  
 Resultados do exemplo:  
  
|$CLUSTER|Expression|  
|--------------|----------------|  
|Cluster 2|0.397918596951617|  
  
 **Observação** Por padrão, a `ClusterProbability` função retorna a probabilidade do cluster mais provável. No entanto, é possível especificar um cluster diferente usando a sintaxe `ClusterProbability('cluster name')`. Se você fizer isto, saiba que os resultados de cada função de previsão são independentes dos outros resultados. Portanto, a pontuação de probabilidade da segunda coluna pode fazer referência a um cluster diferente do nomeado na primeira coluna.  
  
 [Retornar ao início](#bkmk_top2)  
  
###  <a name="sample-query-10-returning-all-possible-clusters-with-probability-and-distance"></a><a name="bkmk_Query10"></a> Exemplo de consulta 10: Retornando todos os possíveis clusters com probabilidade e distância  
 No exemplo anterior, a pontuação de probabilidade não foi muito alta. Para determinar se existe um cluster melhor, use a função [PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx) junto com a função [Cluster &#40;DMX&#41;](/sql/dmx/cluster-dmx) para retornar uma tabela aninhada que inclui todos os clusters possíveis, junto à probabilidade de o novo caso pertencer a cada cluster. A palavra-chave FLATTENED é usada para alterar o conjunto de linhas hierárquico em uma tabela simples para facilitar a visualização.  
  
```  
SELECT FLATTENED PredictHistogram(Cluster())  
From  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender],  
  'S' AS [Marital Status])  
```  
  
|Expression.$CLUSTER|Expression.$DISTANCE|Expression.$PROBABILITY|  
|-------------------------|--------------------------|-----------------------------|  
|Cluster 2|0.602081403048383|0.397918596951617|  
|Cluster 10|0.719691686785675|0.280308313214325|  
|Cluster 4|0.867772590378791|0.132227409621209|  
|Cluster 5|0.931039872200985|0.0689601277990149|  
|Cluster 3|0.942359230072167|0.0576407699278328|  
|Cluster 6|0.958973668972756|0.0410263310272437|  
|Cluster 7|0.979081275926724|0.0209187240732763|  
|Cluster 1|0.999169044818624|0.000830955181376364|  
|Cluster 9|0.999831227795894|0.000168772204105754|  
|Cluster 8|1|0|  
  
 Por padrão, os resultados são classificados por probabilidade. Os resultados informam que, apesar da probabilidade ser baixa, o Cluster 2 ainda é o melhor para o novo ponto de dados.  
  
 **Observação** A coluna adicional, `$DISTANCE`, representa a distância do ponto de dados ao cluster. Por padrão, o algoritmo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering usa o cluster EM evolutivo, que atribui vários clusters a cada ponto de dados e classifica os possíveis clusters.  No entanto, se você criar o modelo de clustering usando o algoritmo K-means, somente um cluster poderá ser atribuído a cada ponto de dados e esta consulta retornará somente uma linha. É necessário entender essas diferenças para interpretar os resultados da função [PredictCaseLikelihood &#40;DMX&#41;](/sql/dmx/predictcaselikelihood-dmx) . Para obter mais informações sobre as diferenças entre clustering EM e K-means, consulte [Referência técnica do algoritmo Microsoft Clustering](microsoft-clustering-algorithm-technical-reference.md).  
  
 [Retornar ao início](#bkmk_top2)  
  
## <a name="function-list"></a>Lista de funções  
 Todos os algoritmos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] dão suporte a um conjunto comum de funções. No entanto, os modelos criados com o algoritmo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering dão suporte para as funções adicionais listadas na tabela a seguir.  
  
|||  
|-|-|  
|Função de previsão|Uso|  
|[Cluster &#40;DMX&#41;](/sql/dmx/cluster-dmx)|Retorna o cluster com maior probabilidade de conter o caso de entrada.|  
|[ClusterDistance &#40;DMX&#41;](/sql/dmx/clusterdistance-dmx)|Retorna a distância do caso de entrada do cluster especificado ou, caso nenhum cluster tenha sido especificado, a distância do caso de entrada do cluster mais provável.<br /><br /> Retorna a probabilidade de que o caso de entrada pertença ao cluster especificado.|  
|[ClusterProbability &#40;DMX&#41;](/sql/dmx/clusterprobability-dmx)|Retorna a probabilidade de que o caso de entrada pertença ao cluster especificado.|  
|[IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx)|Determina se um nó é um filho de outro nó no modelo.|  
|[IsInNode &#40;DMX&#41;](/sql/dmx/isinnode-dmx)|Indica se o nó especificado contém o caso atual.|  
|[PredictAdjustedProbability &#40;DMX&#41;](/sql/dmx/predictadjustedprobability-dmx)|Retorna a probabilidade ponderada.|  
|[PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx)|Prevê associação de membro em um conjunto de dados associativo.|  
|[PredictCaseLikelihood &#40;DMX&#41;](/sql/dmx/predictcaselikelihood-dmx)|Retorna a probabilidade de que um caso de entrada se ajuste ao modelo existente.|  
|[PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)|Retorna uma tabela de valores relacionados ao valor previsto atual.|  
|[PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)|Retorna Node_ID para cada caso.|  
|[PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx)|Retorna a probabilidade para o valor previsto.|  
|[PredictStdev &#40;DMX&#41;](/sql/dmx/predictstdev-dmx)|Retorna o desvio padrão previsto para a coluna especificada.|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|Retorna o valor de suporte para um estado especificado.|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|Retorna a variação de uma coluna especificada.|  
  
 Para obter a sintaxe de funções específicas, consulte [Referência de função de DMX &#40;extensões DMX&#41;](/sql/dmx/data-mining-extensions-dmx-function-reference).  
  
## <a name="see-also"></a>Consulte Também  
 [Consultas de mineração de dados](data-mining-queries.md)   
 [Referência técnica do algoritmo Microsoft Clustering](microsoft-clustering-algorithm-technical-reference.md)   
 [Algoritmo Microsoft Clustering](microsoft-clustering-algorithm.md)  
  
  
