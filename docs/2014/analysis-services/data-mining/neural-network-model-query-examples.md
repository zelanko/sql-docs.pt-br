---
title: Exemplos de consulta de modelo de rede neural | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- neural network algorithms [Analysis Services]
- content queries [DMX]
- neural network model [Analysis Services]
ms.assetid: 81b06183-620f-4e0c-bc10-532e6a1f0829
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3a249a83aba62c7881be024caa3931cb5ad07204
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66083290"
---
# <a name="neural-network-model-query-examples"></a>Neural Network Model Query Examples
  Ao criar uma consulta para um modelo de mineração de dados, você pode criar uma consulta de conteúdo que fornece detalhes de padrões encontrados em análises ou uma consulta de previsão que usa os padrões no modelo para fazer previsões para novos dados. Por exemplo, uma consulta de conteúdo para um modelo de rede neural pode recuperar metadados de modelo, como o número de camadas ocultas. Alternativamente, uma consulta de previsão pode sugerir classificações com base em uma entrada e opcionalmente fornecer as probabilidades de cada classificação.  
  
 Esta seção explica como criar consultas para modelos com base no algoritmo Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Consultas de conteúdo**  
  
 [Obtendo metadados do modelo usando DMX](#bkmk_Query1)  
  
 [Recuperando metadados do modelo do conjunto de linhas de esquema](#bkmk_Query2)  
  
 [Recuperando os atributos de entrada do modelo](#bkmk_Query3)  
  
 [Recuperando pesos da camada oculta](#bkmk_Query4)  
  
 **Consultas de previsão**  
  
 [Criando uma previsão singleton](#bkmk_Query5)  
  
## <a name="finding-information-about-a-neural-network-model"></a>Localizando informações sobre um modelo de rede neural  
 Todos os modelos de mineração expõem o conteúdo captado pelo algoritmo de acordo com um esquema padronizado, o conjunto de linhas do esquema do modelo de mineração. Essas informações fornecem detalhes sobre o modelo e incluem os metadados básicos, as estruturas descobertas na análise e os parâmetros usados durante o processamento. Você pode criar consultas no conteúdo do modelo de mineração usando instruções DMX.  
  
###  <a name="bkmk_Query1"></a> Consulta de exemplo 1: Obtendo metadados do modelo usando DMX  
 A consulta a seguir retorna alguns metadados básicos sobre um modelo criado com o uso do algoritmo Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Em um modelo de rede neural, o nó pai do modelo contém apenas o nome do modelo, o nome do banco de dados em que o modelo está armazenado e o número de nós filho. No entanto, o nó de estatísticas marginais (NODE_TYPE = 24) fornece esses metadados básicos e algumas estatísticas derivadas sobre as colunas de entrada usadas no modelo.  
  
 A consulta de exemplo a seguir se baseia no modelo de mineração criado no [Tutorial de mineração de dados intermediário](../../tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md), denominado `Call Center Default NN`. O modelo usa dados de um call center para explorar correlações possíveis entre o pessoal e o número de chamadas, pedidos e emissões. A instrução DMX recupera dados do nó de estatísticas marginais do modelo de rede neural. A consulta inclui a palavra-chave FLATTENED, porque as estatísticas de interesse do atributo de entrada são armazenadas em uma tabela aninhada, NODE_DISTRIBUTION. No entanto, se seu provedor de consulta der suporte a conjuntos de linhas hierárquicos, você não precisará usar a palavra-chave FLATTENED.  
  
```  
SELECT FLATTENED MODEL_CATALOG, MODEL_NAME,   
(    SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE,  
     [SUPPORT], [PROBABILITY], VALUETYPE   
     FROM NODE_DISTRIBUTION  
) AS t  
FROM [Call Center Default NN].CONTENT  
WHERE NODE_TYPE = 24  
```  
  
> [!NOTE]  
>  É necessário colocar o nome das colunas da tabela aninhada `[SUPPORT]` e `[PROBABILITY]` entre colchetes para distingui-las das palavras-chave reservadas de mesmo nome.  
  
 Resultados do exemplo:  
  
|MODEL_CATALOG|MODEL_NAME|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VALUETYPE|  
|--------------------|-----------------|-----------------------|------------------------|---------------|-------------------|-----------------|  
|Adventure Works DW Multidimensional 2012|Call Center NN|Tempo médio por emissão|Ausente|0|0|1|  
|Adventure Works DW Multidimensional 2012|Call Center NN|Tempo médio por emissão|< 64.7094100096|11|0.407407407|5|  
  
 Para obter uma definição do que significam as colunas no conjunto de linhas de esquema no contexto de um modelo de rede neural, consulte [Conteúdo do modelo de mineração para modelos de rede neural &#40;Analysis Services – Data Mining&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md).  
  
###  <a name="bkmk_Query2"></a> Consulta de exemplo 2: Recuperando metadados do modelo do conjunto de linhas de esquema  
 Você pode encontrar as mesmas informações retornadas em uma consulta de conteúdo DMX consultando o conjunto de linhas do esquema de mineração de dados. No entanto, o conjunto de linhas de esquema fornece algumas colunas adicionais. O exemplo de consulta a seguir retorna a data em que o modelo foi criado, modificado e processado pela última vez. A consulta também retorna as colunas previsíveis, que não estão facilmente disponíveis com base no conteúdo do modelo, e os parâmetros usados para criar o modelo. Essas informações podem ser úteis para documentar o modelo.  
  
```  
SELECT MODEL_NAME, DATE_CREATED, LAST_PROCESSED, PREDICTION_ENTITY, MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Call Center Default NN'  
```  
  
 Resultados do exemplo:  
  
|||  
|-|-|  
|MODEL_NAME|NM Padrão do Center|  
|DATE_CREATED|10/1/2008 5:07:38 PM|  
|LAST_PROCESSED|10/1/2008 5:24:02 PM|  
|PREDICTION_ENTITY|Tempo médio por emissão,<br /><br /> Grau de serviço,<br /><br /> Número de pedidos|  
|MINING_PARAMETERS|HOLDOUT_PERCENTAGE=30, HOLDOUT_SEED=0,<br /><br /> MAXIMUM_INPUT_ATTRIBUTES=255, MAXIMUM_OUTPUT_ATTRIBUTES=255,<br /><br /> MAXIMUM_STATES=100, SAMPLE_SIZE=10000, HIDDEN_NODE_RATIO=4|  
  
###  <a name="bkmk_Query3"></a> Consulta de exemplo 3: Recuperando os atributos de entrada do modelo  
 Você pode recuperar pares exatos de atributo-valor de entrada que foram usados para criar o modelo consultando os nós filho (NODE_TYPE = 20) da camada de entrada (NODE_TYPE = 18). A consulta a seguir retorna uma lista dos atributos de entrada, das descrições de nó.  
  
```  
SELECT NODE_DESCRIPTION  
FROM [Call Center Default NN].CONTENT  
WHERE NODE_TYPE = 2  
```  
  
 Resultados do exemplo:  
  
|NODE_DESCRIPTION|  
|-----------------------|  
|Tempo médio por emissão=64.7094100096 - 77.4002099712|  
|Dia da semana=Sex.|  
|Operadores de nível 1|  
  
 Somente algumas linhas representativas dos resultados são mostradas aqui. No entanto, você pode ver que NODE_DESCRIPTION fornece informações ligeiramente diferentes de acordo com o tipo de dados do atributo de entrada.  
  
-   Se o atributo for um valor discreto ou diferenciado, tanto o atributo quanto seu valor ou o intervalo diferenciado serão retornados.  
  
-   Se o atributo for um tipo de dados numérico contínuo, NODE_DESCRIPTION conterá só o nome de atributo. No entanto, você pode recuperar a tabela aninhada NODE_DISTRIBUTION para obter a média ou retornar NODE_RULE para obter os valores mínimo e máximo do intervalo numérico.  
  
 A consulta a seguir mostra como consultar a tabela aninhada NODE_DISTRIBUTION para retornar os atributos em uma coluna e seus valores em outra. Para atributos contínuos, o valor do atributo é representado pela sua média.  
  
```  
SELECT FLATTENED   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE  
FROM NODE_DISTRIBUTION) as t  
FROM [Call Center Default NN -- Predict Service and Orders].CONTENT  
WHERE NODE_TYPE = 21  
```  
  
 Resultados do exemplo:  
  
|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|  
|-----------------------|------------------------|  
|Tempo médio por emissão|64.7094100096 - 77.4002099712|  
|Day Of Week|Sex.|  
|Operadores de nível 1|3.2962962962963|  
  
 Os valores mínimo e máximo do intervalo são armazenados na coluna NODE_RULE e são representados como um fragmento XML, conforme mostrado no exemplo a seguir:  
  
```  
<NormContinuous field="Level 1 Operators">    
  <LinearNorm orig="2.83967303681711" norm="-1" />    
  <LinearNorm orig="3.75291955577548" norm="1" />    
</NormContinuous>    
```  
  
###  <a name="bkmk_Query4"></a> Consulta de exemplo 4: Recuperando pesos da camada oculta  
 O conteúdo de um modelo de rede neural é estruturado de modo a facilitar a recuperação de detalhes sobre qualquer nó na rede. Além disso, os números de ID dos nós fornecem informações que ajudam a identificar relações entre os tipos de nós.  
  
 A consulta a seguir demonstra como recuperar os coeficientes armazenados em um determinado nó da camada oculta. A camada oculta consiste em um nó do organizador (NODE_TYPE = 19), que contém apenas metadados e vários nós filho (NODE_TYPE = 22), que contêm os coeficientes das várias combinações dos atributos e dos valores. Esta consulta retorna apenas os nós de coeficiente.  
  
```  
SELECT FLATTENED TOP 1 NODE_UNIQUE_NAME,   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, VALUETYPE  
FROM NODE_DISTRIBUTION) as t  
FROM  [Call Center Default NN -- Predict Service and Orders].CONTENT  
WHERE NODE_TYPE = 22  
AND [PARENT_UNIQUE_NAME] = '40000000200000000' FROM [Call Center Default NN].CONTENT  
```  
  
 Resultados do exemplo:  
  
|NODE_UNIQUE_NAME|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.VALUETYPE|  
|------------------------|-----------------------|------------------------|-----------------|  
|70000000200000000|6000000000000000a|-0.178616518|7|  
|70000000200000000|6000000000000000b|-0.267561918|7|  
|70000000200000000|6000000000000000c|0.11069497|7|  
|70000000200000000|6000000000000000d|0.123757712|7|  
|70000000200000000|6000000000000000e|0.294565343|7|  
|70000000200000000|6000000000000000f|0.22245318|7|  
|70000000200000000||0.188805045|7|  
  
 Os resultados parciais mostrados aqui demonstram como o conteúdo do modelo de rede neural relaciona o nó oculto aos nós de entrada.  
  
-   Os nomes exclusivos de nós na camada oculta sempre começam com 70000000.  
  
-   Os nomes exclusivos de nós na camada de entrada sempre começam com 60000000.  
  
 Assim, esses resultados informam que o nó indicado pela ID 70000000200000000 tinha seis coeficientes diferentes (VALUETYPE = 7) passados a ele. Os valores dos coeficientes estão na coluna ATTRIBUTE_VALUE. Você pode determinar exatamente a qual atributo de entrada o coeficiente se destina usando a ID do nó na coluna ATTRIBUTE_NAME. Por exemplo, a ID do nó 6000000000000000a se refere a um atributo e valor de entrada, `Day of Week = 'Tue.'` Use a ID do nó para criar uma consulta ou procure o nó utilizando o [Visualizador de Árvore de Conteúdo Genérica da Microsoft](../microsoft-generic-content-tree-viewer-data-mining.md).  
  
 De modo semelhante, se você consultar a tabela NODE_DISTRIBUTION dos nós na camada de saída (NODE_TYPE = 23), poderá visualizar os coeficientes de cada valor de saída. No entanto, na camada de saída, os ponteiros se referem aos nós da camada oculta. Para obter mais informações, consulte [Mining Model Content for Neural Network Models &#40;Analysis Services - Data Mining&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md).  
  
## <a name="using-a-neural-network-model-to-make-predictions"></a>Usando um modelo de rede neural para fazer previsões  
 O algoritmo Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] dá suporte à classificação e regressão. Você pode usar funções de previsão com esses modelos para fornecer dados novos e criar previsões singleton ou em lotes.  
  
###  <a name="bkmk_Query5"></a> Consulta de exemplo 5: Criando uma previsão singleton  
 A maneira mais fácil de criar uma consulta de previsão em um modelo de rede neural é usar o Construtor de Consultas de Previsão, disponível na guia **Previsão de Mineração** do Designer de Mineração de Dados no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Procure o modelo no Visualizador de Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] para filtrar atributos de interesse e exibir novas tendências e, em seguida, alterne para a guia **Previsão de Mineração** para criar uma consulta e prever novos valores para essas tendências.  
  
 Por exemplo, você pode procurar o modelo de call center para exibir as correlações entre os volumes de pedidos e outros atributos. Para fazer isso, abra o modelo no visualizador e, para **entrada**, selecione  **\<todos os >**.  Em seguida, para **Saída**, selecione **Número de Pedidos**. Para **Valor 1**, selecione o intervalo que representa a maioria dos pedidos e, para **Valor 2**, selecione o intervalo que representa menos pedidos. Você poderá ver rapidamente todos os atributos que o modelo correlaciona com o volume de pedidos.  
  
 Ao procurar os resultados no visualizador, você descobre que certos dias da semana tem baixos volumes de pedidos e que um aumento no número de operadores parece estar correlacionado às vendas mais altas. Você poderia usar uma consulta de previsão no modelo para testar uma hipótese "e se" e perguntar se o aumento do número de operadores de nível 2 em um dia de baixo volume aumentaria os pedidos. Para fazer isso, crie uma consulta como a seguinte:  
  
```  
SELECT Predict([Call Center Default NN].[Number of Orders]) AS [Predicted Orders],  
PredictProbability([Call Center Default NN].[Number of Orders]) AS [Probability]  
FROM [Call Center Default NN]  
NATURAL PREDICTION JOIN   
(SELECT 'Tue.' AS [Day of Week],  
13 AS [Level 2 Operators]) AS t  
```  
  
 Resultados do exemplo:  
  
|Pedidos previstos|Probabilidade|  
|----------------------|-----------------|  
|364|0.9532...|  
  
 O volume de vendas previsto é maior do que o intervalo atual de vendas para terça-feira, e a probabilidade da previsão é muito alta. No entanto, talvez você queira criar várias previsões usando um processo em lotes para testar várias hipóteses no modelo.  
  
> [!NOTE]  
>  Os Suplementos de Mineração de Dados para Excel 2007 fornecem assistentes de regressão logística que facilitam responder perguntas complexas, como quantos Operadores de Nível Dois seriam necessários para melhorar a classificação do serviço visando um nível de destino para um turno específico. Os suplementos de mineração de dados são um download gratuito e incluem assistentes baseados nos algoritmos de rede neural e/ou regressão logística. Para obter mais informações, consulte o site [Suplementos de Data Mining para Office 2007](https://go.microsoft.com/fwlink/?LinkID=117790) .  
  
## <a name="list-of-prediction-functions"></a>Lista de funções de previsão  
 Todos os algoritmos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] dão suporte a um conjunto comum de funções. Não há nenhuma função de previsão específica para o algoritmo Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] ; entretanto, o algoritmo dá suporte às funções listadas na tabela a seguir.  
  
|||  
|-|-|  
|Função de previsão|Uso|  
|[IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx)|Determina se um nó é um filho de outro nó no gráfico de rede neural.|  
|[PredictAdjustedProbability &#40;DMX&#41;](/sql/dmx/predictadjustedprobability-dmx)|Retorna a probabilidade ponderada.|  
|[PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)|Retorna uma tabela de valores relacionados ao valor previsto atual.|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|Retorna a variância para o valor previsto.|  
|[PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx)|Retorna a probabilidade para o valor previsto.|  
|[PredictStdev &#40;DMX&#41;](/sql/dmx/predictstdev-dmx)|Retorna o desvio padrão para o valor previsto.|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|Para modelos de rede neural e regressão logística, retorna um único valor que representa o tamanho do conjunto de treinamento de todo o modelo.|  
  
 Para obter a sintaxe de funções específicas, consulte [Referência de função de DMX &#40;extensões DMX&#41;](/sql/dmx/data-mining-extensions-dmx-function-reference).  
  
## <a name="see-also"></a>Consulte também  
 [Microsoft Neural Network Algorithm](microsoft-neural-network-algorithm.md)   
 [Microsoft Neural Network Algorithm Technical Reference](microsoft-neural-network-algorithm-technical-reference.md)   
 [Conteúdo do modelo de mineração para modelos de rede neural &#40;Analysis Services – Data Mining&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [Lição 5: Criação de rede Neural e modelos de regressão logística &#40;Tutorial de mineração de dados intermediário&#41;](../../tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
  
