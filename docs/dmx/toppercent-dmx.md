---
title: TopPercent (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: acd35dc68c4f42231aa6f71d6cc2a150ff027811
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68893058"
---
# <a name="toppercent-dmx"></a>TopPercent (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  A função **TopPercent** retorna, em ordem de diminuição da classificação, as linhas mais superiores de uma tabela cujo total cumulativo é pelo menos um percentual especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
TopPercent(<table expression>, <rank expression>, <percent>)  
```  
  
## <a name="applies-to"></a>Aplica-se A  
 Uma expressão que retorna uma tabela, como uma referência \<de coluna de tabela> ou uma função que retorna uma tabela.  
  
## <a name="return-type"></a>Tipo de retorno  
 \<> de expressão de tabela  
  
## <a name="remarks"></a>Comentários  
 A função **TopPercent** retorna as linhas mais superiores em ordem decrescente de classificação com base no valor avaliado da expressão de \<classificação> argumento para cada linha, de modo que a soma da expressão \<de classificação> valores seja pelo menos a porcentagem especificada pelo argumento \<percentual>. **TopPercent** retorna o menor número de elementos possíveis ao mesmo tempo em que atende ao valor percentual especificado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma consulta de previsão em relação ao modelo de associação que você cria usando o [tutorial de mineração de dados básico](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
 Para entender como o TopPercent funciona, pode ser útil primeiro executar uma consulta de previsão que retorna apenas a tabela aninhada.  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 10)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
> [!NOTE]  
>  Neste exemplo, o valor fornecido como entrada contém uma única aspa e, portanto, deve ser precedido por outra aspa. Se você não tiver certeza da sintaxe para inserção de um caractere de escape, use o Construtor de Consultas de Previsão para criar a consulta. Quando você seleciona o valor da lista suspensa, o caractere de escape exigido é inserido. Para obter mais informações, consulte [criar uma consulta singleton no designer de mineração de dados](https://docs.microsoft.com/analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer).  
  
 Exemplos de resultados:  
  
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
  
 A função TopPercent usa os resultados dessa consulta e retorna as linhas com os maiores valores que somam ao percentual especificado.  
  
```  
SELECT   
TopPercent  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    50)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 O primeiro argumento para a função TopPercent é o nome de uma coluna de tabela. Neste exemplo, a tabela aninhada é retornada chamando a função Predict e usando o argumento INCLUDE_STATISTICS.  
  
 O segundo argumento para a função TopPercent é a coluna na tabela aninhada que você usa para ordenar os resultados. Neste exemplo, a opção INCLUDE_STATISTICS retorna as colunas $SUPPORT, $PROBABILTY e $ADJUSTED PROBABILITY. Este exemplo usa $SUPPORT porque os valores de suporte não são fracionários e, portanto, são mais fáceis de verificar.  
  
 O terceiro argumento para a função TopPercent especifica a porcentagem, como um Double. Para obter as linhas dos principais produtos que totalizam até 50 por cento do suporte total, digite 50.  
  
 Exemplos de resultados:  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0,29...|0,25...|  
|Water Bottle|2866|0,19...|0,17...|  
|Patch kit|2113|0,14...|0,13...|  
|Mountain Tire Tube|1992|0,133...|0,12...|  
  
 **Observação** Este exemplo é fornecido apenas para ilustrar o uso de TopPercent. Dependendo do tamanho do conjunto de dados, esta consulta pode demorar muito para ser executada.  
  
> [!WARNING]  
>  As funções MDX para TOPPERCENT e BOTTOMPERCENT podem gerar resultados inesperados quando os valores usados para calcular o percentual incluem números negativos. Esse comportamento não afeta as funções DMX. Para obter mais informações, consulte [BottomPercent &#40;MDX&#41;](../mdx/bottompercent-mdx.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40;&#41;DMX](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;&#41;DMX](../dmx/general-prediction-functions-dmx.md)  
  
  
