---
description: BottomCount (DMX)
title: BottomCount (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a2b810d2b268e12c97857475e474d3ed597978ec
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431168"
---
# <a name="bottomcount-dmx"></a>BottomCount (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Retorna o número especificado de linhas inferiores em ordem crescente de classificação, conforme especificado por uma expressão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BottomCount(<table expression>, <rank expression>, <count>)  
```  
  
## <a name="applies-to"></a>Aplica-se A  
 Uma expressão que retorna uma tabela, como uma \<table column reference> , ou uma função que retorna uma tabela.  
  
## <a name="return-type"></a>Tipo de retorno  
 \<table expression>  
  
## <a name="remarks"></a>Comentários  
 O valor fornecido pelo \<rank expression> argumento determina a ordem crescente de classificação para as linhas que são fornecidas no \<table expression> argumento, e o número de linhas inferiores que é especificado no \<count> argumento é retornado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma consulta de previsão em relação ao modelo de associação que você cria usando o [tutorial de mineração de dados básico](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
 Para entender como o BottomCount funciona, pode ser útil primeiro executar uma consulta de previsão que retorna apenas a tabela aninhada.  
  
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
  
 A função BottomCount usa os resultados dessa consulta e retorna as linhas com valores menores que somam ao percentual especificado.  
  
```  
SELECT   
BottomCount  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    3)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 O primeiro argumento para a função BottomCount é o nome de uma coluna de tabela. Neste exemplo, a tabela aninhada é retornada chamando a função Predict e usando o argumento INCLUDE_STATISTICS.  
  
 O segundo argumento para a função BottomCount é a coluna na tabela aninhada que você usa para ordenar os resultados. Neste exemplo, a opção INCLUDE_STATISTICS retorna as colunas $SUPPORT, $PROBABILTY e $ADJUSTED PROBABILITY. Este exemplo usa $SUPPORT porque os valores de suporte não são fracionários e, portanto, são mais fáceis de verificar.  
  
 O terceiro argumento para a função BottomCount especifica o número de linhas. Para obter as três linhas com a menor classificação, ordenadas por $SUPPORT, digite 3.  
  
 Resultados do exemplo:  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Road Bottle Cage|1195|0, 80314537|0, 77173962|  
|Mountain Bottle Cage|1367|0, 91874454|0, 87780332|  
|Fender Set - Mountain|1415|0, 95100477|0, 90718432|  
  
 **Observação** Este exemplo é fornecido apenas para ilustrar o uso de BottomCount. Dependendo do tamanho do conjunto de dados, esta consulta pode demorar muito para ser executada.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções &#40;&#41;DMX ](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;&#41;DMX ](../dmx/general-prediction-functions-dmx.md)   
 [&#41;&#40;DMX BottomPercent ](../dmx/bottompercent-dmx.md)   
 [&#41;&#40;DMX BottomSum ](../dmx/bottomsum-dmx.md)   
 [&#41;&#40;DMX TopCount ](../dmx/topcount-dmx.md)  
  
  
