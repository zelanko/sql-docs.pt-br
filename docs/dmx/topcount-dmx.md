---
title: TopCount (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0d4c83626c11def14f1ed9f745fca54e94995c97
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970241"
---
# <a name="topcount-dmx"></a>TopCount (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Retorna o número especificado de linhas superiores em ordem decrescente de classificação, conforme especificado por uma expressão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
TopCount(<table expression>, <rank expression>, <count>)  
```  
  
## <a name="applies-to"></a>Aplica-se A  
 Uma expressão que retorna uma tabela, como uma \<table column reference> , ou uma função que retorna uma tabela.  
  
## <a name="return-type"></a>Tipo de retorno  
 \<table expression>  
  
## <a name="remarks"></a>Comentários  
 O valor fornecido pelo \<rank expression> argumento determina a ordem decrescente de classificação para as linhas que são fornecidas no \<table expression> argumento, e o número de linhas superiores que é especificado no \<count> argumento é retornado.  
  
 A função TopCount foi introduzida originalmente para habilitar previsões associativas e, em geral, produz os mesmos resultados de uma instrução que inclui cláusulas **selecionar Top** e **order by** . Você obterá um melhor desempenho para previsões associativas se usar a função **Predict (DMX)** , que dá suporte à especificação de um número de previsões a serem retornadas.  
  
 No entanto, há situações em que talvez você ainda precise usar o TopCount. Por exemplo, o DMX não dá suporte ao qualificador **Top** em uma instrução de subseleção. A função de [&#41;de PredictHistogram &#40;DMX](../dmx/predicthistogram-dmx.md) também não oferece suporte à adição de **Top**.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir são consultas de previsão em relação ao modelo de associação que você cria usando o [tutorial de mineração de dados básico](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). As consultas retornam os mesmos resultados, mas o primeiro exemplo usa TopCount e o segundo exemplo usa a função Predict.  
  
 Para entender como o TopCount funciona, pode ser útil primeiro executar uma consulta de previsão que retorna apenas a tabela aninhada.  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 10)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
> [!NOTE]  
>  Neste exemplo, o valor fornecido como entrada contém uma única aspa e, portanto, deve ser precedido por outra aspa. Se você não tiver certeza da sintaxe para inserção de um caractere de escape, use o Construtor de Consultas de Previsão para criar a consulta. Quando você seleciona o valor da lista suspensa, o caractere de escape exigido é inserido. Para obter mais informações, consulte [criar uma consulta singleton no designer de mineração de dados](https://docs.microsoft.com/analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer).  
  
 Resultados do exemplo:  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0,291283016|0,252695851|  
|Water Bottle|2866|0,192620472|0,175205052|  
|Patch kit|2113|0,142012232|0,132389356|  
|Mountain Tire Tube|1992|0,133879965|0,125304948|  
|Mountain-200|1755|0,117951475|0,111260823|  
|Tubo de pneu de estrada|1588|0,106727603|0,101229538|  
|Capacete para Ciclismo|1473|0, 98998589|0, 94256014|  
|Fender Set - Mountain|1415|0, 95100477|0, 90718432|  
|Mountain Bottle Cage|1367|0, 91874454|0, 87780332|  
|Road Bottle Cage|1195|0, 80314537|0, 77173962|  
  
 A função TopCount usa os resultados dessa consulta e retorna o número especificado de linhas de menor valor.  
  
```  
SELECT   
TopCount  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    3)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 O primeiro argumento para a função TopCount é o nome de uma coluna de tabela. Neste exemplo, a tabela aninhada é retornada chamando a função Predict e usando o argumento INCLUDE_STATISTICS.  
  
 O segundo argumento para a função TopCount é a coluna na tabela aninhada que você usa para ordenar os resultados. Neste exemplo, a opção INCLUDE_STATISTICS retorna as colunas $SUPPORT, $PROBABILTY e $ADJUSTED PROBABILITY. Este exemplo usa $SUPPORT para classificar os resultados.  
  
 O terceiro argumento para a função TopCount especifica o número de linhas a serem retornadas, como um inteiro. Para obter os três principais produtos, ordenados por $SUPPORT, digite 3.  
  
 Resultados do exemplo:  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0,29...|0,25...|  
|Water Bottle|2866|0,19...|0,17...|  
|Patch kit|2113|0,14...|0,13...|  
  
 No entanto, esse tipo de consulta pode afetar o desempenho em uma configuração de produção. Isso é porque a consulta retorna um conjunto de todas as previsões do algoritmo, classifica essas previsões e retorna as três principais.  
  
 O exemplo a seguir fornece uma instrução alternativa que retorna os mesmos resultados, mas é executada de maneira significativamente mais rápida. Este exemplo substitui TopCount pela função Predict, que aceita várias previsões como um argumento. Este exemplo também usa a palavra-chave **$support** para recuperar diretamente a coluna da tabela aninhada.  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3, $SUPPORT)  
```  
  
 Os resultados contêm as três principais previsões classificadas pelo valor de suporte. Você pode substituir $SUPPORT por $PROBABILITY ou $ADJUSTED_PROBABILITY para retornar previsões classificadas por probabilidade ou probabilidade ajustada. Para obter mais informações, consulte **Predict (DMX)**.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções &#40;&#41;DMX](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;&#41;DMX](../dmx/general-prediction-functions-dmx.md)   
 [&#41;&#40;DMX BottomCount](../dmx/bottomcount-dmx.md)   
 [&#41;&#40;DMX TopPercent](../dmx/toppercent-dmx.md)   
 [TopSum &#40;&#41;DMX](../dmx/topsum-dmx.md)  
  
  
