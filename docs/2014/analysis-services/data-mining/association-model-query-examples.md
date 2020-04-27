---
title: Exemplos de consulta de modelo de associação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- itemsets [Analysis Services]
- association algorithms [Analysis Services]
- rules [Data Mining]
- association rules
- content queries [DMX]
ms.assetid: 68b39f5c-c439-44ac-8046-6f2d36649059
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a31052c0d239010407941141997fca8fc343f9cf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66086118"
---
# <a name="association-model-query-examples"></a>Exemplos de consulta de um modelo de associação
  Ao criar uma consulta em um modelo de mineração de dados, você pode criar uma consulta de conteúdo, que fornece detalhes sobre as regras e os conjuntos de itens descobertos durante a análise ou criar uma consulta de previsão, que usa as associações descobertas nos dados para fazer previsões. Para um modelo de associação, normalmente, as previsões baseiam-se em regras e pode ser usadas para fazer recomendações, enquanto as consultas em conteúdo geralmente exploram a relação entre os conjuntos de itens. Você também pode recuperar metadados sobre o modelo.  
  
 Esta seção explica como criar esses tipos de consulta para modelos que se baseiam no algoritmo Regras de Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Consultas de conteúdo**  
  
 [Obtendo dados de metadados do modelo com o DMX](#bkmk_Query1)  
  
 [Obtendo metadados do conjunto de linhas do esquema](#bkmk_Query2)  
  
 [Recuperando os parâmetros originais do modelo](#bkmk_Query3)  
  
 [Recuperando uma lista de conjuntos de itens e produtos](#bkmk_Query4)  
  
 [Retornando os 10 principais conjuntos de itens](#bkmk_Query5)  
  
 **Consultas de previsão**  
  
 [Prevendo itens associados](#bkmk_Query6)  
  
 [Determinando a confiança dos conjuntos de itens relacionados](#bkmk_Query7)  
  
##  <a name="finding-information-about-the-model"></a><a name="bkmk_top2"></a> Localizando informações sobre o modelo  
 Todos os modelos de mineração expõem o conteúdo assimilado pelo algoritmo de acordo com um esquema padronizado, chamado de conjunto de linhas do esquema do modelo de mineração. Você pode criar consultas para o conjunto de linhas do esquema do modelo de mineração usando instruções DMX (Data Mining Extensions) ou procedimentos armazenados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], você também pode consultar diretamente os conjuntos de linhas de esquema como tabelas do sistema, usando uma sintaxe similar ao SQL.  
  
###  <a name="sample-query-1-getting-model-metadata-by-using-dmx"></a><a name="bkmk_Query1"></a>Exemplo de consulta 1: obtendo metadados de modelo usando DMX  
 A consulta a seguir retorna os metadados básicos sobre o modelo de associação, `Association`, como o nome do modelo, o banco de dados onde o modelo é armazenado e o número de nós filho do modelo. Esta consulta usa uma consulta de conteúdo DMX para recuperar os metadados do nó pai do modelo:  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY], NODE_DESCRIPTION  
FROM Association.CONTENT  
WHERE NODE_TYPE = 1  
```  
  
> [!NOTE]  
>  É necessário colocar o nome da coluna, CHILDREN_CARDINALITY, entre colchetes para diferenciá-lo da palavra-chave reservada MDX do mesmo nome.  
  
 Resultados do exemplo:  
  
|||  
|-|-|  
|MODEL_CATALOG|Teste de Associação|  
|MODEL_NAME|Associação|  
|NODE_CAPTION|Modelo de regras de associação|  
|NODE_SUPPORT|14879|  
|CHILDREN_CARDINALITY|942|  
|NODE_DESCRIPTION|Modelo de regras de associação; ITEMSET_COUNT=679; RULE_COUNT=263; MIN_SUPPORT=14; MAX_SUPPORT=4334; MIN_ITEMSET_SIZE=0; MAX_ITEMSET_SIZE=3; MIN_PROBABILITY=0.400390625; MAX_PROBABILITY=1; MIN_LIFT=0.14309369632511; MAX_LIFT=1.95758227647523|  
  
 Para obter uma definição do que essas colunas significam em um modelo de associação, consulte [Conteúdo do modelo de mineração para modelos de associação &#40;Analysis Services – Data Mining&#41;](mining-model-content-for-association-models-analysis-services-data-mining.md).  
  
 [Retornar ao início](#bkmk_top2)  
  
###  <a name="sample-query-2-getting-additional-metadata-from-the-schema-rowset"></a><a name="bkmk_Query2"></a> Exemplo de consulta 2: Obtendo metadados adicionais do conjunto de linhas de esquema  
 É possível consultar o conjunto de linhas de esquema de mineração de dados para encontrar as mesmas informações retornadas em uma consulta de conteúdo DMX. No entanto, o conjunto de linhas de esquema fornece algumas colunas adicionais, como a data em que o modelo foi processado, a estrutura de mineração e o nome da coluna usada como atributo previsível.  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, SERVICE_NAME, PREDICTION_ENTITY,   
MINING_STRUCTURE, LAST_PROCESSED  
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Association'  
```  
  
 Resultados do exemplo:  
  
|||  
|-|-|  
|MODEL_CATALOG|Adventure Works DW Multidimensional 2012|  
|MODEL_NAME|Associação|  
|SERVICE_NAME|Modelo de regras de associação|  
|PREDICTION_ENTITY|v Assoc Seq Line Items|  
|MINING_STRUCTURE|Associação|  
|LAST_PROCESSED|9/29/2007 10:21:24 PM|  
  
 [Retornar ao início](#bkmk_top2)  
  
###  <a name="sample-query-3-retrieving-original-parameters-for-model"></a><a name="bkmk_Query3"></a> Exemplo de consulta 3: Recuperando parâmetros originais do modelo  
 A consulta a seguir retorna uma única coluna que contém detalhes sobre as configurações de parâmetros que foram usados na criação do modelo.  
  
```  
SELECT MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Association'  
```  
  
 Resultados do exemplo:  
  
 MAXIMUM_ITEMSET_COUNT=200000,MAXIMUM_ITEMSET_SIZE=3,MAXIMUM_SUPPORT=1,MINIMUM_SUPPORT=9.40923449156529E-04,MINIMUM_IMPORTANCE=-999999999,MINIMUM_ITEMSET_SIZE=0,MINIMUM_PROBABILITY=0.4  
  
 [Retornar ao início](#bkmk_top2)  
  
## <a name="finding-information-about-rules-and-itemsets"></a>Localizando informações sobre regras e conjuntos de itens  
 Existem dois usos comuns para um modelo de associação: descobrir informações sobre conjuntos de itens frequentes e extrair detalhes sobre regras e conjuntos de itens específicos. Por exemplo, convém extrair uma lista de regras cuja pontuação indicou serem especialmente interessantes ou criar uma lista dos conjuntos de itens mais comuns. Para recuperar essas informações, use uma consulta de conteúdo DMX. Você também procura essas informações usando o **Visualizador de Associação da Microsoft**.  
  
###  <a name="sample-query-4-retrieving-list-of-itemsets-and-products"></a><a name="bkmk_Query4"></a> Exemplo de consulta 4: Recuperando a lista de conjuntos de itens e produtos  
 A consulta a seguir recupera todos os conjuntos de itens com uma tabela aninhada que lista os produtos incluídos em cada conjunto de itens. A coluna NODE_NAME contém a ID exclusiva do conjunto de itens do modelo, enquanto NODE_CAPTION fornece um texto que descreve os itens. Nesse exemplo, a tabela aninhada é simplificada, de modo que o conjunto de itens que contém dois produtos irá gerar duas linhas nos resultados. É possível omitir a palavra-chave FLATTENED se o cliente oferecer suporte a dados hierárquicos.  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,  
NODE_PROBABILITY, NODE_SUPPORT,  
(SELECT ATTRIBUTE_NAME FROM NODE_DISTRIBUTION) as PurchasedProducts  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
```  
  
 Resultados do exemplo:  
  
|||  
|-|-|  
|NODE_NAME|37|  
|NODE_CAPTION|Sport-100 = Existing|  
|NODE_PROBABILITY|0.291283016331743|  
|NODE_SUPPORT|4334|  
|PURCHASEDPRODUCTS.ATTRIBUTE_NAME|v Assoc Seq Line Items(Sport-100)|  
  
 [Retornar ao início](#bkmk_top2)  
  
###  <a name="sample-query-5-returning-top-10-itemsets"></a><a name="bkmk_Query5"></a> Exemplo de consulta 5: Retornando os 10 principais conjuntos de itens  
 Este exemplo demonstra como usar parte das funções de agrupamento e ordenação que o DMX fornece por padrão. A consulta retorna os 10 principais conjuntos de itens quando ordenada pelo suporte de cada nó. Observe que não é necessário agrupar explicitamente os resultados como se fosse o Transact-SQL; no entanto, você pode usar apenas uma função de agregação em cada consulta.  
  
```  
SELECT TOP 10 (NODE_SUPPORT),NODE_NAME, NODE_CAPTION  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
```  
  
 Resultados do exemplo:  
  
|||  
|-|-|  
|NODE_SUPPORT|4334|  
|NODE_NAME|37|  
|NODE_CAPTION|Sport-100 = Existing|  
  
 [Retornar ao início](#bkmk_top2)  
  
## <a name="making-predictions-using-the-model"></a>Fazendo predições com o modelo  
 Um modelo de regras de associação é usado frequentemente para gerar recomendações que se baseiam em correlações descobertas nos conjuntos de itens. Portanto, quando você cria uma consulta de previsão com base em um modelo de regras de associação, está normalmente usando as regras no modelo fazer suposições com base em novos dados.  [PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx) é a função que retorna recomendações e tem vários argumentos que você pode usar para personalizar os resultados da consulta.  
  
 Outro exemplo de onde as consultas em um modelo de associação podem ser úteis é para retornar a confiança de várias regras e conjuntos de itens para que você possa comparar a eficiência de estratégias diferentes de venda cruzada. Os exemplos seguintes ilustram como criar essas consultas.  
  
###  <a name="sample-query-6-predicting-associated-items"></a><a name="bkmk_Query6"></a> Exemplo de consulta 6: Prevendo itens associados  
 Este exemplo usa o modelo de associação criado no [Tutorial de mineração de dados intermediário &#40;Analysis Services – Mineração de Dados&#41;](../../tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md). Ele demonstra como criar uma consulta de previsão que informa quais produtos recomendar para um cliente que comprou um determinado produto. Esse tipo de consulta, em que você fornece valores para o modelo em uma instrução `SELECT...UNION`, é chamada de consulta singleton. Como a coluna de modelo previsível que corresponde aos novos valores é uma tabela aninhada, use uma cláusula `SELECT` para mapear o novo valor à coluna da tabela aninhada, `[Model]`, e outra cláusula `SELECT` para mapear a coluna da tabela aninhada à coluna de nível de caso, `[v Assoc Seq Line Items]`. Adicionar a palavra-chave INCLUDE-STATISTICS à consulta permitirá que você veja a probabilidade e o suporte das recomendações.  
  
```  
SELECT PredictAssociation([Association].[vAssocSeqLineItems],INCLUDE_STATISTICS, 3)  
FROM [Association]  
NATURAL PREDICTION JOIN   
(SELECT  
(SELECT 'Classic Vest' as [Model])  
AS [v Assoc Seq Line Items])  
AS t  
```  
  
 Resultados do exemplo:  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283|0.252696|  
|Water Bottle|2866|0.19262|0.175205|  
|Patch kit|2113|0.142012|0.132389|  
  
 [Retornar ao início](#bkmk_top2)  
  
###  <a name="sample-query-7-determining-confidence-for-related-itemsets"></a><a name="bkmk_Query7"></a> Exemplo de consulta 7: Determinando a confiança dos conjuntos de itens relacionados  
 Embora as regras sejam úteis para gerar recomendações, os conjuntos de itens são mais interessantes para uma análise mais profunda dos padrões no conjunto de dados. Por exemplo, se você não ficar satisfeito com a recomendação retornada pelo exemplo de consulta anterior, pode examinar outros conjuntos de itens que contêm Product A para poder ter uma ideia melhor se Product A é um acessório que as pessoas tendem a comprar com todos os tipos de produtos ou se A é fortemente correlacionado às compras de determinados produtos. A forma mais fácil de explorar essas relações é filtrando os conjuntos de itens no Visualizador de Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] ; no entanto, é possível recuperar as mesmas informações com um consulta.  
  
 O exemplo de consulta a seguir retorna todos os conjuntos de itens que incluem o item Garrafa de Água, inclusive o item único Garrafa de água.  
  
```  
SELECT TOP 100 FROM   
(  
SELECT FLATTENED NODE_CAPTION, NODE_SUPPORT,   
(SELECT ATTRIBUTE_NAME from NODE_DISTRIBUTION  
WHERE ATTRIBUTE_NAME = 'v Assoc Seq Line Items(Water Bottle)') as D  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
) AS Items  
WHERE [D.ATTRIBUTE_NAME] <> NULL  
ORDER BY NODE_SUPPORT DESC  
```  
  
 Resultados do exemplo:  
  
|NODE_CAPTION|NODE_SUPPORT|D.ATTRIBUTE_NAME|  
|-------------------|-------------------|-----------------------|  
|Water Bottle = Existing|2866|v Assoc Seq Line Items(Water Bottle)|  
|Mountain Bottle Cage = Existing, Water Bottle = Existing|1136|v Assoc Seq Line Items(Water Bottle)|  
|Road Bottle Cage = Existing, Water Bottle = Existing|1068|v Assoc Seq Line Items(Water Bottle)|  
|Water Bottle = Existing, Sport-100 = Existing|734|v Assoc Seq Line Items(Water Bottle)|  
  
 Essa consulta retorna as duas linhas da tabela aninhada que correspondem aos critérios e todas as linhas da tabela de casos ou externa. Portanto, adicione uma condição que elimine as linhas da tabela de casos que tiverem um valor nulo para o nome do atributo de destino.  
  
 [Retornar ao início](#bkmk_top2)  
  
## <a name="function-list"></a>Lista de funções  
 Todos os algoritmos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] dão suporte a um conjunto comum de funções. Entretanto, o algoritmo Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] oferece suporte para funções adicionais relacionadas na tabela a seguir.  
  
|||  
|-|-|  
|Função de previsão|Uso|  
|[IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx)|Determina se um nó é um filho de outro nó no gráfico de rede neural.|  
|[IsInNode &#40;DMX&#41;](/sql/dmx/isinnode-dmx)|Indica se o nó especificado contém o caso atual.|  
|[PredictAdjustedProbability &#40;DMX&#41;](/sql/dmx/predictadjustedprobability-dmx)|Retorna a probabilidade ponderada.|  
|[PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx)|Prevê associação de membro em um conjunto de dados associativo.|  
|[PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)|Retorna uma tabela de valores relacionados ao valor previsto atual.|  
|[PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)|Retorna Node_ID para cada caso.|  
|[PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx)|Retorna a probabilidade para o valor previsto.|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|Retorna o valor de suporte para um estado especificado.|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|Retorna a variância para o valor previsto.|  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmo de associação da Microsoft](microsoft-association-algorithm.md)   
 [Referência técnica do algoritmo de associação da Microsoft](microsoft-association-algorithm-technical-reference.md)   
 [Conteúdo do modelo de mineração para modelos de associação &#40;Analysis Services – Data Mining&#41;](mining-model-content-for-association-models-analysis-services-data-mining.md)  
  
  
