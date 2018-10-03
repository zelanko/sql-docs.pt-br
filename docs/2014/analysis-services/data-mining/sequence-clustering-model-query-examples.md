---
title: Exemplos de consulta de modelo de Clustering de sequência | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- sequence clustering algorithms [Analysis Services]
- content queries [DMX]
- sequence [Analysis Services]
ms.assetid: 64bebcdc-70ab-43fb-8d40-57672a126602
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8f5776d2a7523f4d56bb48926a8f0bf0929e87f1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48118116"
---
# <a name="sequence-clustering-model-query-examples"></a>Sequence Clustering Model Query Examples
  Quando você cria uma consulta referente a um modelo de mineração de dados, pode criar uma consulta de conteúdo, que fornece detalhes sobre as informações armazenadas no modelo ou pode criar uma consulta de previsão, que usa os padrões no modelo para fazer previsões com base nos novos dados fornecidos. Para um modelo de clusterização de sequência, as consultas de conteúdo geralmente fornecem mais detalhes sobre os clusters encontrados ou as transições dentro desses clusters. Você também pode recuperar metadados sobre o modelo usando uma consulta.  
  
 As consultas de previsão em um modelo de clusterização de sequência geralmente fazem recomendações com base nas sequências e transições, em atributos não sequenciais incluídos no modelo ou em uma combinação de atributos sequenciais e não sequenciais.  
  
 Esta seção explica como criar consultas para modelos baseados no algoritmo MSC. Para obter informações gerais sobre como criar consultas, consulte [Consultas de mineração de dados](data-mining-queries.md).  
  
 **Consultas de conteúdo**  
  
 [Usando o conjunto de linhas do esquema de mineração de dados para retornar parâmetros do modelo](#bkmk_Query1)  
  
 [Obtendo uma lista de sequências para um estado](#bkmk_Query2)  
  
 [Usando procedimentos armazenados do sistema](#bkmk_Query3)  
  
 **Consultas de previsão**  
  
 [Prever o(s) próximo(s) estado(s)](#bkmk_Query4)  
  
##  <a name="bkmk_ContentQueries"></a> Localizando informações sobre o Modelo de Clustering de Sequências  
 Para criar consultas significativas sobre o conteúdo de um modelo de mineração, você deve entender a estrutura do conteúdo do modelo e quais tipos de nós armazenam quais tipos de informações. Para obter mais informações, consulte [Conteúdo do modelo de mineração para modelos de clustering de sequência &#40;Analysis Services – Data Mining&#41;](mining-model-content-for-sequence-clustering-models.md).  
  
###  <a name="bkmk_Query1"></a> Exemplo de consulta 1: Usando o conjunto de linhas do esquema de mineração de dados para retornar parâmetros do modelo  
 Ao consultar o conjunto de linhas do esquema de mineração de dados, você pode encontrar vários tipos de informações sobre o modelo, inclusive metadados básicos, a data e a hora de criação e do último processamento do modelo, o nome da estrutura de mineração na qual o modelo se baseia e a coluna usada como o atributo previsível.  
  
 A consulta a seguir retorna os parâmetros que foram usados para criar e treinar o modelo, `[Sequence Clustering]`. Você pode criar este modelo na Lição 5 do [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md).  
  
```  
SELECT MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Sequence Clustering'  
```  
  
 Resultados do exemplo:  
  
|MINING_PARAMETERS|  
|------------------------|  
|CLUSTER_COUNT=15,MINIMUM_SUPPORT=10,MAXIMUM_STATES=100,MAXIMUM_SEQUENCE_STATES=64|  
  
 Observe que este modelo foi criado usando-se o valor padrão de 10 para CLUSTER_COUNT. Quando você especifica um número de clusters diferente de zero para CLUSTER_COUNT, o algoritmo trata esse número como uma dica para o número aproximado de clusters a serem encontrados. No entanto, no processo de análise, o algoritmo pode encontrar mais ou menos clusters. Nesse caso, o algoritmo descobriu que 15 clusters se ajustam melhor aos dados de treinamento. Assim, a lista de valores de parâmetro do modelo completo reporta a contagem de clusters conforme determinado pelo algoritmo, não o valor passado durante a criação do modelo.  
  
 Como esse comportamento difere de deixar o algoritmo determinar o melhor número de clusters? Como uma experiência, você pode criar outro modelo de clusterização que usa os mesmos dados, mas definir CLUSTER_COUNT como 0. Quando você fizer isso, o algoritmo detectará 32 clusters. Portanto, usando o valor padrão de 10 para CLUSTER_COUNT, você restringe o número de resultados.  
  
 O valor de 10 é usado por padrão porque reduzir o número de clusters torna mais fácil para a maioria das pessoas procurar e entender os agrupamentos nos dados. Entretanto, cada modelo e conjunto de dados é diferente. Talvez você queira fazer experiências com números de clusters diferentes para verificar qual valor de parâmetro gera o modelo mais preciso.  
  
###  <a name="bkmk_Query2"></a> Exemplo de consulta 2: Obtendo uma lista de sequências para um estado  
 O conteúdo do modelo de mineração armazena as sequências encontradas nos dados de treinamento como um primeiro estado associado a uma lista de todos os segundos estados relacionados. O primeiro estado é usado como o rótulo da sequência e os segundos estados relacionados são denominados transições.  
  
 Por exemplo, a consulta a seguir retorna a lista completa de primeiros estados no modelo, antes do agrupamento de sequências em clusters.  Você pode obter essa lista retornando a lista de sequências (NODE_TYPE = 13) que têm o nó raiz do modelo como pai (PARENT_UNIQUE_NAME = 0). A palavra-chave FLATTENED torna os resultados mais fáceis de ler.  
  
> [!NOTE]  
>  O nome das colunas, PARENT_UNIQUE_NAME, Suporte e Probabilidade deve ser colocado entre colchetes para distingui-los das palavras-chave reservadas de mesmo nome.  
  
```  
SELECT FLATTENED NODE_UNIQUE_NAME,  
(SELECT ATTRIBUTE_VALUE AS [Product 1],  
[Support] AS [Sequence Support],   
[Probability] AS [Sequence Probability]  
FROM NODE_DISTRIBUTION) AS t  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_TYPE = 13  
AND [PARENT_UNIQUE_NAME] = 0  
```  
  
 Resultados parciais:  
  
|NODE_UNIQUE_NAME|Produto 1|Suporte de sequência|Probabilidade de sequência|  
|------------------------|---------------|----------------------|--------------------------|  
|1081327|Ausente|0|#######|  
|1081327|Suporte de bicicleta multifuncional|17|0.00111|  
|1081327|Lavagem de bicicleta|64|0.00418|  
|1081327|(linhas 4 a 36 omitidas)|||  
|1081327|Women's Mountain Shorts|506|0.03307|  
  
 A lista de sequências no modelo sempre é classificada alfabeticamente em ordem crescente. A ordem das sequências é importante porque você pode encontrar as transições relacionadas examinando o número de ordem de sequência. O `Missing` valor sempre é a transição 0.  
  
 Por exemplo, nos resultados anteriores, o produto "Women Mountain Shorts" é a sequência número 37 no modelo. Você pode usar essa informação para exibir todos os produtos que já foram comprados depois de "Women Mountain Shorts".  
  
 Para fazer isso, primeiro referencie o valor retornado para NODE_UNIQUE_NAME na consulta anterior, para obter a ID do nó que contém todas as sequências do modelo. Passe esse valor à consulta como a ID do nó pai, para obter apenas as transições incluídas no nó, o que ocorre para conter uma lista de todas as sequências do modelo. No entanto, se queria visualizar a lista de transições de um determinado cluster, você poderia passar a ID do nó do cluster e visualizar apenas as sequências associadas a esse cluster.  
  
```  
SELECT NODE_UNIQUE_NAME  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_DESCRIPTION = 'Transition row for sequence state 37'  
AND [PARENT_UNIQUE_NAME] = '1081327'  
```  
  
 Resultados do exemplo:  
  
|NODE_UNIQUE_NAME|  
|------------------------|  
|1081365|  
  
 O nó representado por esta ID contém uma lista das sequências após o produto "Women's Mountain Shorts", junto com os valores de suporte e probabilidade.  
  
```  
SELECT FLATTENED  
(SELECT ATTRIBUTE_VALUE AS Product2,  
[Support] AS [P2 Support],  
[Probability] AS [P2 Probability]  
FROM NODE_DISTRIBUTION) AS t  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_UNIQUE_NAME = '1081365'  
```  
  
 Resultados do exemplo:  
  
|t.Product2|Suporte de t.P2|Probabilidade de t.P2|  
|----------------|------------------|----------------------|  
|Ausente|230.7419|0.456012|  
|Colete clássico|8.16129|0.016129|  
|Capacete para Ciclismo|60.83871|0.120235|  
|Luvas de meio dedo|30.41935|0.060117|  
|Jersey Logo de manga longa|86.80645|0.171554|  
|Meias para corrida|28.93548|0.057185|  
|Camisa esportiva clássica de manga curta|60.09677|0.118768|  
  
 Observe que o suporte para as várias sequências relacionadas a Women's Mountain Shorts é 506 no modelo. Os valores de suporte para as transições também somam 506. No entanto, os números não são inteiros, o que parecerá um pouco estranho se você esperar que o suporte represente simplesmente uma contagem de casos que contêm cada transição. No entanto, como o método para criar clusters calcula a associação parcial, a probabilidade de qualquer transição em um cluster deve ser avaliada por sua probabilidade de pertencer a esse cluster em particular.  
  
 Por exemplo, se houver quatro clusters, uma determinada sequência pode ter uma possibilidade de 40% de pertencer ao cluster 1, 30% de pertencer ao cluster 2, 20% de pertencer ao cluster 3 e 10% de pertencer ao cluster 4. Depois que o algoritmo determinar a qual cluster a transição tem maior probabilidade de pertencer, ele avaliará as probabilidades dentro do cluster pela probabilidade de precedência de cluster.  
  
###  <a name="bkmk_Query3"></a> Exemplo de consulta 3: Usando procedimentos armazenados de sistema  
 Com esses exemplos de consulta, você pode observar que as informações armazenadas no modelo são complexas e que talvez seja preciso criar várias consultas para obter os dados necessários. No entanto, o visualizador MSC fornece um conjunto avançado de ferramentas para navegação gráfica pelas informações contidas em um modelo de clusterização de sequência e você ainda pode usar esse visualizador para consultar e detalhar o modelo.  
  
 Na maioria dos casos, as informações apresentadas no visualizador MSC são criadas com o uso de procedimentos armazenados de sistema do Analysis Services para consultar o modelo. Você pode escrever consultas DMX referentes ao conteúdo do modelo para recuperar as mesmas informações, mas os procedimentos armazenados de sistema do Analysis Services fornecem um atalho prático para explorar ou testar modelos.  
  
> [!NOTE]  
>  Os procedimentos armazenados de sistema são usados para processamento interno pelo servidor e pelos clientes que a Microsoft fornece para interação com o servidor Analysis Services. Assim, a Microsoft se reserva o direito de alterá-los a qualquer momento. Embora eles sejam descritos aqui para sua conveniência, não há suporte para seu uso em um ambiente de produção. Para assegurar a estabilidade e a compatibilidade em um ambiente de produção, você sempre deve escrever suas próprias consultas usando DMX.  
  
 Esta seção fornece alguns exemplos de como usar os procedimentos armazenados de sistema para criar consultas referentes a um modelo de clusterização de sequência:  
  
#### <a name="cluster-profiles-and-sample-cases"></a>Perfis de cluster e casos de exemplo  
 A guia Perfis de cluster mostra uma lista de clusters no modelo, o tamanho de cada cluster e um histograma que indica os estados inclusos no cluster. Há dois procedimentos armazenados de sistema que você pode usar em consultas para recuperar informações semelhantes:  
  
-   `GetClusterProfile` retorna as características do cluster, com todas as informações encontradas na tabela NODE_DISTRIBUTION do cluster.  
  
-   `GetNodeGraph` retorna os nós e as margens que podem ser usadas para construir uma representação matemática gráfica dos clusters, correspondente ao que você visualiza na primeira guia de Clusterização de Sequência. Os nós são clusters e as margens representam pesos ou força.  
  
 O exemplo a seguir demonstra como usar o procedimento armazenado de sistema, `GetClusterProfiles`, para retornar todos os clusters no modelo, com os respectivos perfis. Este procedimento armazenado executa uma série de instruções DMX que retornam o conjunto completo de perfis no modelo. Entretanto, para usar esse procedimento armazenado, você deve saber o endereço do modelo.  
  
 `CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterProfiles('Sequence Clustering', 2147483647, 0)`  
  
 O exemplo a seguir demonstra como recuperar o perfil de um determinado cluster, Cluster 12, usando o procedimento armazenado de sistema `GetNodeGraph`e especificando a ID do cluster, que geralmente é igual ao número no nome do cluster.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetNodeGraph('Sequence Clustering','12',0)  
```  
  
 Se você omitir a ID do cluster, conforme mostrado na consulta a seguir, `GetNodeGraph` retornará uma lista simples ordenada de todos os perfis de cluster:  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetNodeGraph('Sequence Clustering','',0)  
```  
  
 A guia **Perfil de Cluster** também exibe um histograma de casos de exemplo do modelo. Esses casos de exemplo representam os casos idealizados do modelo. Esses casos não são armazenados no modelo da mesma forma que os dados de treinamento; você deve usar uma sintaxe especial para recuperar os casos de exemplo do modelo.  
  
```  
SELECT * FROM [Sequence Clustering].SAMPLE_CASES WHERE IsInNode('12')  
```  
  
 Para obter mais informações, consulte [SELECT FROM &#60;model&#62;.SAMPLE CASES &#40;DMX&#41;](/sql/dmx/select-from-model-dmx).  
  
#### <a name="cluster-characteristics-and-cluster-discrimination"></a>Características e discriminação do cluster  
 A guia **Características do Cluster** resume os atributos principais de cada cluster, classificados por probabilidade. Você pode descobrir quantos casos pertencem a um cluster e como é a distribuição de casos no cluster: cada característica tem um certo suporte. Para visualizar as características de um cluster específico, você deve saber a ID do cluster.  
  
 Os exemplos a seguir usam o procedimento armazenado de sistema `GetClusterCharacteristics`para retornar todas as características de Cluster 12 que têm uma pontuação de probabilidade acima do limite especificado de 0,0005.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('Sequence Clustering','12',0.0005)  
```  
  
 Para retornar as características de todos os clusters, deixe a ID de cluster vazia.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('Sequence Clustering','',0.0005)  
```  
  
 O exemplo a seguir chama o procedimento armazenado de sistema `GetClusterDiscrimination` para comparar as características de Cluster 1 e Cluster 12.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('Sequence Clustering','1','12',0.0005,true)  
```  
  
 Se você quiser escrever sua própria consulta em DMX para comparar dois clusters ou comparar um cluster com seu complemento, primeiro será necessário recuperar um conjunto de características e depois recuperar as características do cluster específico no qual há interesse e comparar os dois conjuntos. Este cenário é mais complicado e normalmente requer algum processamento de cliente.  
  
#### <a name="states-and-transitions"></a>Estados e transições  
 A guia **Transições de Estado** de MSC executa consultas complicadas no back-end para recuperar e comparar as estatísticas para clusters diferentes. Reproduzir esses resultados requer uma consulta mais complexa e algum processamento de cliente.  
  
 No entanto, você pode usar as consultas DMX descritas no Exemplo 2 da seção [Consultas de conteúdo](#bkmk_ContentQueries)para recuperar probabilidades e estados para sequências ou para transições individuais.  
  
## <a name="using-the-model-to-make-predictions"></a>Usando o modelo para fazer previsões  
 As consultas de previsão em um modelo de clusterização de sequência podem usar muitas das funções de previsão utilizadas com outros modelos de clusterização. Além disso, é possível usar a função de previsão especial, [PredictSequence &#40;DMX&#41;](/sql/dmx/predictsequence-dmx), para fazer recomendações ou para prever os próximos estados.  
  
###  <a name="bkmk_Query4"></a> Exemplo de consulta 4: Prever o próximo estado ou estados  
 Você pode usar a função [PredictSequence &#40;DMX&#41;](/sql/dmx/predictsequence-dmx) para prever o próximo estado mais provável, dado um valor. Também é possível prever vários estados seguintes: por exemplo, você pode retornar uma lista dos três principais produtos que um cliente provavelmente compra, para apresentar uma lista de recomendações.  
  
 O exemplo de consulta a seguir é uma consulta de previsão singleton que retorna as cinco previsões principais, junto com sua probabilidade. Como o modelo inclui uma tabela aninhada, você deve usar a tabela aninhada `[v Assoc Seq Line Items]`como a referência de coluna ao fazer previsões. Além disso, quando você fornece valores como entrada, é necessário juntar as colunas da tabela de caixa e da tabela aninhada, conforme mostrado pelas instruções SELECT aninhadas.  
  
```  
SELECT FLATTENED PredictSequence([v Assoc Seq Line Items], 7)  
FROM [Sequence Clustering]  
NATURAL PREDICTION JOIN  
(SELECT  (SELECT 1 as [Line Number],  
   'All-Purpose Bike Stand' as [Model]) AS [v Assoc Seq Line Items])   
AS t  
```  
  
 Resultados do exemplo:  
  
|Expression.$Sequence|Expression.Line Number|Expression.Model|  
|--------------------------|----------------------------|----------------------|  
|1||Capacete para Ciclismo|  
|2||Capacete para Ciclismo|  
|3||Sport-100|  
|4||Jersey Logo de manga longa|  
|5||Luvas de meio dedo|  
|6||Suporte de bicicleta multifuncional|  
|7||Suporte de bicicleta multifuncional|  
  
 Há três colunas nos resultados, mesmo que você talvez esteja esperando apenas uma coluna, porque consulta sempre retorna uma coluna para a tabela de caixa. Aqui os resultados são simples; caso contrário, a consulta retornaria uma única coluna que contém duas colunas de tabela aninhada.  
  
 A coluna $sequence é retornada por padrão pela função `PredictSequence` para ordenar os resultados da previsão. A coluna `[Line Number]`é necessária para corresponder às chaves de sequência no modelo, mas as chaves não são geradas.  
  
 De forma interessante, as principais sequências previstas depois de Suporte de bicicleta multifuncional são Capacete para ciclismo e Capacete para ciclismo. Isso não é um erro. Dependendo do modo como os dados são apresentados ao cliente e como são agrupados durante o treinamento do modelo, é bem possível ter sequências desse tipo. Por exemplo, um cliente pode adquirir um capacete para ciclismo (vermelho) e depois outro capacete para ciclismo (azul), ou comprar dois seguidos se não havia nenhum modo de especificar a quantidade.  
  
 Os valores nas linhas 6 e 7 são espaços reservados. Quando você chega ao fim da cadeia de transições possíveis, em vez de encerrar os resultados da previsão, o valor que foi passado como entrada é adicionado aos resultados. Por exemplo, se você aumentou o número de previsões para 20, os valores das linhas 6 a 20 serão iguais, Suporte de bicicleta multifuncional.  
  
## <a name="function-list"></a>Lista de funções  
 Todos os algoritmos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] dão suporte a um conjunto comum de funções. No entanto, o algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering dá suporte às funções adicionais relacionadas na tabela a seguir.  
  
|||  
|-|-|  
|Função de previsão|Uso|  
|[Cluster &#40;DMX&#41;](/sql/dmx/cluster-dmx)|Retorna o cluster com maior probabilidade de conter o caso de entrada|  
|[ClusterDistance &#40;DMX&#41;](/sql/dmx/clusterdistance-dmx)|Retorna a distância do caso de entrada do cluster especificado ou, caso nenhum cluster tenha sido especificado, a distância do caso de entrada do cluster mais provável.<br /><br /> Essa função pode ser usada com qualquer tipo de modelo de clustering (EM, K-Means etc.), mas o resultado será diferente de acordo com o algoritmo.|  
|[ClusterProbability &#40;DMX&#41;](/sql/dmx/clusterprobability-dmx)|Retorna a probabilidade de que o caso de entrada pertença ao cluster especificado.|  
|[IsInNode &#40;DMX&#41;](/sql/dmx/isinnode-dmx)|Indica se o nó especificado contém o caso atual.|  
|[PredictAdjustedProbability &#40;DMX&#41;](/sql/dmx/predictadjustedprobability-dmx)|Retorna a probabilidade ajustada de um estado especificado.|  
|[PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx)|Prevê associação de membro.|  
|[PredictCaseLikelihood &#40;DMX&#41;](/sql/dmx/predictcaselikelihood-dmx)|Retorna a probabilidade de que um caso de entrada se ajuste ao modelo existente.|  
|[PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)|Retorna uma tabela que representa um histograma para a previsão de uma determinada coluna.|  
|[PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)|Retorna o Node_ID do nó no qual o caso é classificado.|  
|[PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx)|Retorna a probabilidade para um estado especificado.|  
|[PredictSequence &#40;DMX&#41;](/sql/dmx/predictsequence-dmx)|Prediz valores de sequência futuros para um conjunto especificado de dados de sequência.|  
|[PredictStdev &#40;DMX&#41;](/sql/dmx/predictstdev-dmx)|Retorna o desvio padrão previsto para a coluna especificada.|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|Retorna o valor de suporte para um estado especificado.|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|Retorna a variação de uma coluna especificada.|  
  
 Para obter uma lista das funções comuns a todos os algoritmos [!INCLUDE[msCoName](../../includes/msconame-md.md)], consulte [Funções de previsão gerais &#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx). Para obter a sintaxe de funções específicas, consulte [Referência de função de DMX &#40;extensões DMX&#41;](/sql/dmx/data-mining-extensions-dmx-function-reference).  
  
## <a name="see-also"></a>Consulte também  
 [Consultas de mineração de dados](data-mining-queries.md)   
 [Referência técnica do algoritmo de Clustering de sequência da Microsoft](microsoft-sequence-clustering-algorithm-technical-reference.md)   
 [Algoritmo msc](microsoft-sequence-clustering-algorithm.md)   
 [Mining Model Content para modelos de Clustering de sequência &#40;Analysis Services - mineração de dados&#41;](mining-model-content-for-sequence-clustering-models.md)  
  
  
