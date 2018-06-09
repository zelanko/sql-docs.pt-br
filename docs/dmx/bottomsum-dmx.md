---
title: BottomSum (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6a6356e70aa6694e04a9112e44a22825f0dc7a52
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34842779"
---
# <a name="bottomsum-dmx"></a>BottomSum (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna, em ordem crescente de classificação, as linhas mais baixas de uma tabela, cujo total cumulativo é, no mínimo, um valor especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BottomSum(<table expression>, <rank expression>, <sum>)  
```  
  
## <a name="applies-to"></a>Aplica-se a  
 Uma expressão que retorna uma tabela, como um \<referência de coluna de tabela >, ou uma função que retorna uma tabela.  
  
## <a name="return-type"></a>Tipo de retorno  
 \<expressão de tabela >  
  
## <a name="remarks"></a>Remarks  
 O **BottomSum** função retorna as linhas mais baixas em ordem crescente de classificação. A classificação baseia-se no valor avaliado do \<expressão de classificação > argumento para cada linha, de modo que a soma da \<expressão de classificação > valores é pelo menos o total dado especificado pelo \<soma > argumento. **BottomSum** retorna o menor número de elementos possível embora ainda assim atenda o valor de soma especificado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma consulta de previsão no modelo de associação que você cria usando o [Tutorial básico de mineração de dados](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
 Para entender como funciona a BottomSum, pode ser útil primeiro executar uma consulta de previsão que retorna apenas a tabela aninhada.  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 10)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
> [!NOTE]  
>  Neste exemplo, o valor fornecido como entrada contém uma única aspa e, portanto, deve ser precedido por outra aspa. Se você não tiver certeza da sintaxe para inserção de um caractere de escape, use o Construtor de Consultas de Previsão para criar a consulta. Quando você seleciona o valor da lista suspensa, o caractere de escape exigido é inserido. Para obter mais informações, consulte [criar uma consulta Singleton no Designer de mineração de dados](../analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer.md).  
  
 Resultados do exemplo:  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283016|0.252695851|  
|Water Bottle|2866|0.192620472|0.175205052|  
|Patch kit|2113|0.142012232|0.132389356|  
|Mountain Tire Tube|1992|0.133879965|0.125304948|  
|Mountain-200|1755|0.117951475|0.111260823|  
|Tubo de pneu de estrada|1588|0.106727603|0.101229538|  
|Capacete para Ciclismo|1473|0.098998589|0.094256014|  
|Fender Set - Mountain|1415|0.095100477|0.090718432|  
|Mountain Bottle Cage|1367|0.091874454|0.087780332|  
|Road Bottle Cage|1195|0.080314537|0.077173962|  
  
 A função BottomSum utiliza os resultados dessa consulta e retorna as linhas com os menores valores que totalizam a contagem especificada.  
  
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
  
 O primeiro argumento para a função BottomSum é o nome de uma coluna de tabela. Neste exemplo, a tabela aninhada é retornada da chamada da função de previsão e usando o argumento INCLUDE_STATISTICS.  
  
 O segundo argumento para a função BottomSum é a coluna na tabela aninhada que você pode usar para ordenar os resultados. Neste exemplo, a opção INCLUDE_STATISTICS retorna as colunas $SUPPORT, $PROBABILTY e $ADJUSTED PROBABILITY. Este exemplo usa $PROBABILITY para retornar linhas que totalizam pelo menos 50% de probabilidade.  
  
 O terceiro argumento para a função BottomSum Especifica a soma de destino, como um duplo. Para obter as linhas dos produtos de menor contagem que totalizam até 10 por cento de probabilidade, digite .1.  
  
 Resultados do exemplo:  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Road Bottle Cage|1195|0.08…|0.07…|  
|Mountain Bottle Cage|1367|0.09…|0.08…|  
  
 **Observação** neste exemplo é fornecido apenas para ilustrar o uso de BottomSum. Dependendo do tamanho do conjunto de dados, esta consulta pode demorar muito para ser executada.  
  
## <a name="see-also"></a>Consulte também  
 [Funções &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funções de previsão geral &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [BottomPercent &#40;DMX&#41;](../dmx/bottompercent-dmx.md)  
  
  
