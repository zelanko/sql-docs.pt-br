---
title: BottomCount (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- BOTTOMCOUNT
dev_langs:
- DMX
helpviewer_keywords:
- BottomCount function
ms.assetid: bbe2f1d6-c8b5-49ce-ae13-337114a50aee
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 6301719854c05bd6243df446a5f6f2cdfab52402
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="bottomcount-dmx"></a>BottomCount (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o número especificado de linhas inferiores em ordem crescente de classificação, conforme especificado por uma expressão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BottomCount(<table expression>, <rank expression>, <count>)  
```  
  
## <a name="applies-to"></a>Aplica-se a  
 Uma expressão que retorna uma tabela, como um \<referência de coluna de tabela >, ou uma função que retorna uma tabela.  
  
## <a name="return-type"></a>Tipo de retorno  
 \<expressão de tabela >  
  
## <a name="remarks"></a>Remarks  
 O valor que é fornecido pelo \<expressão de classificação > argumento determina a ordem de classificação crescente das linhas que são fornecidos no \<expressão de tabela > argumento e o número de linhas inferiores especificado no \<contagem > argumento será retornado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma consulta de previsão no modelo de associação que você cria usando o [Tutorial básico de mineração de dados](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
 Para entender como funciona a BottomCount, pode ser útil primeiro executar uma consulta de previsão que retorna apenas a tabela aninhada.  
  
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
  
 A função BottomCount utiliza os resultados dessa consulta e retorna as linhas com valor menor que totalizam a porcentagem especificada.  
  
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
  
 O primeiro argumento para a função BottomCount é o nome de uma coluna de tabela. Neste exemplo, a tabela aninhada é retornada da chamada da função de previsão e usando o argumento INCLUDE_STATISTICS.  
  
 O segundo argumento para a função BottomCount é a coluna na tabela aninhada que você pode usar para ordenar os resultados. Neste exemplo, a opção INCLUDE_STATISTICS retorna as colunas $SUPPORT, $PROBABILTY e $ADJUSTED PROBABILITY. Este exemplo usa $SUPPORT porque os valores de suporte não são fracionários e, portanto, são mais fáceis de verificar.  
  
 O terceiro argumento para a função BottomCount Especifica o número de linhas. Para obter as três linhas com a menor classificação, ordenadas por $SUPPORT, digite 3.  
  
 Resultados do exemplo:  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Road Bottle Cage|1195|0.080314537|0.077173962|  
|Mountain Bottle Cage|1367|0.091874454|0.087780332|  
|Fender Set - Mountain|1415|0.095100477|0.090718432|  
  
 **Observação** Este exemplo é fornecido apenas para ilustrar o uso de BottomCount. Dependendo do tamanho do conjunto de dados, esta consulta pode demorar muito para ser executada.  
  
## <a name="see-also"></a>Consulte também  
 [Funções &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funções de previsão geral &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [BottomPercent &#40;DMX&#41;](../dmx/bottompercent-dmx.md)   
 [BottomSum &#40;DMX&#41;](../dmx/bottomsum-dmx.md)   
 [TopCount &#40;DMX&#41;](../dmx/topcount-dmx.md)  
  
  
