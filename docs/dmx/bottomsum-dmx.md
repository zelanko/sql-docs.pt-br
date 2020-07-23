---
title: BottomSum (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cceeac44646b904a7d7e1b45bd3c92d4ad07a0d5
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969923"
---
# <a name="bottomsum-dmx"></a>BottomSum (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Retorna, em ordem crescente de classificação, as linhas mais baixas de uma tabela, cujo total cumulativo é, no mínimo, um valor especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BottomSum(<table expression>, <rank expression>, <sum>)  
```  
  
## <a name="applies-to"></a>Aplica-se A  
 Uma expressão que retorna uma tabela, como uma \<table column reference> , ou uma função que retorna uma tabela.  
  
## <a name="return-type"></a>Tipo de retorno  
 \<table expression>  
  
## <a name="remarks"></a>Comentários  
 A função **BottomSum** retorna as linhas inferiores em ordem crescente de classificação. A classificação é baseada no valor avaliado do \<rank expression> argumento para cada linha, de modo que a soma dos \<rank expression> valores seja pelo menos o total determinado especificado pelo \<sum> argumento. **BottomSum** retorna o menor número de elementos possíveis ao mesmo tempo em que atende ao valor SUM especificado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma consulta de previsão em relação ao modelo de associação que você cria usando o [tutorial de mineração de dados básico](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
 Para entender como o BottomSum funciona, pode ser útil primeiro executar uma consulta de previsão que retorna apenas a tabela aninhada.  
  
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
  
 A função BottomSum usa os resultados dessa consulta e retorna as linhas com os valores mais baixos que somam à contagem especificada.  
  
```  
SELECT   
BottomSum  
    (  
    Predict([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $PROBABILITY,  
    .1)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 O primeiro argumento para a função BottomSum é o nome de uma coluna de tabela. Neste exemplo, a tabela aninhada é retornada chamando a função Predict e usando o argumento INCLUDE_STATISTICS.  
  
 O segundo argumento para a função BottomSum é a coluna na tabela aninhada que você usa para ordenar os resultados. Neste exemplo, a opção INCLUDE_STATISTICS retorna as colunas $SUPPORT, $PROBABILTY e $ADJUSTED PROBABILITY. Este exemplo usa $PROBABILITY para retornar linhas que totalizam pelo menos 50% de probabilidade.  
  
 O terceiro argumento para a função BottomSum especifica a soma de destino, como um Double. Para obter as linhas dos produtos de menor contagem que totalizam até 10 por cento de probabilidade, digite .1.  
  
 Resultados do exemplo:  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Road Bottle Cage|1195|0, 8...|0, 7...|  
|Mountain Bottle Cage|1367|0, 9...|0, 8...|  
  
 **Observação** Este exemplo é fornecido apenas para ilustrar o uso de BottomSum. Dependendo do tamanho do conjunto de dados, esta consulta pode demorar muito para ser executada.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções &#40;&#41;DMX](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;&#41;DMX](../dmx/general-prediction-functions-dmx.md)   
 [&#41;&#40;DMX BottomPercent](../dmx/bottompercent-dmx.md)  
  
  
