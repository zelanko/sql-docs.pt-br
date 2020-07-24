---
title: Previsão (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d323794af598cb621b7fb8f9939cd2ae1c0f2746
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86968302"
---
# <a name="predict-dmx"></a>Predict (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  A função **Predict** retorna um valor previsto ou um conjunto de valores para uma coluna especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Predict(<scalar column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
Predict(<table column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
```  
  
## <a name="applies-to"></a>Aplica-se A  
 Uma referência de coluna escalar ou a uma referência de coluna de tabela.  
  
## <a name="return-type"></a>Tipo de retorno  
 \<scalar column reference>  
  
 ou  
  
 \<table column reference>  
  
 O tipo de retorno depende do tipo de coluna ao qual essa função se aplica.  
  
> [!NOTE]  
>  INCLUSIVE, EXCLUSIVE, INPUT_ONLY e INCLUDE_STATISTICS aplicam-se somente à referência da coluna da tabela, e EXCLUDE_NULL e INCLUDE_NULL aplicam-se apenas à referência da coluna escalar.  
  
## <a name="remarks"></a>Comentários  
 As opções incluem EXCLUDE_NULL (padrão), INCLUDE_NULL, INCLUSIVE, EXCLUSIVE (padrão), INPUT_ONLY e INCLUDE_STATISTICS.  
  
> [!NOTE]  
>  Para modelos de série temporal, a função Predict não oferece suporte a INCLUDE_STATISTICS.  
  
 O parâmetro INCLUDE_NODE_ID retorna a coluna $NODEID no resultado. NODE_ID é o nó de conteúdo no qual a previsão é executada para um caso particular. Esse parâmetro é opcional ao usar a previsão em colunas de tabela.  
  
 O parâmetro *n* aplica-se às colunas da tabela. Define o número de linhas retornadas com base no tipo de previsão. Se a coluna subjacente for Sequence, ela chamará a função **PredictSequence** . Se a coluna subjacente for Time Series, ela chamará a função **PredictTimeSeries** . Para tipos associativos de previsão, ele chama a função **PredictAssociation** .  
  
 A função **Predict** dá suporte a polimorfismo.  
  
 As formas abreviadas alternativas a seguir são usadas frequentemente:  
  
-   [Gênero] é uma alternativa para **previsão**([gênero], EXCLUDE_NULL).  
  
-   [Compras de produtos] é uma alternativa para **previsão**([compras de produtos], EXCLUDE_NULL, exclusivo).  
  
    > [!NOTE]  
    >  O próprio tipo de retorno dessa função é considerado uma referência de coluna. Isso significa que a função **Predict** pode ser usada como um argumento em outras funções que usam uma referência de coluna como um argumento (exceto para a própria função de **previsão** ).  
  
 A passagem de INCLUDE_STATISTICS para uma previsão em uma coluna com valor de tabela adiciona as colunas **$Probability** e **$support** à tabela resultante. Essas colunas descrevem a probabilidade de existência para o registro de tabela aninhada associada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa a função Predict para retornar os quatro produtos no banco de dados Adventure Works que têm mais probabilidade de serem vendidos juntos. Como a função está sendo prevista em relação a um modelo de mineração de regras de associação, ela automaticamente usa a função **PredictAssociation** , conforme descrito anteriormente.  
  
```  
SELECT  
    Predict([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,4)  
FROM     [Association]  
```  
  
 Resultados do exemplo:  
  
 Esta consulta retorna uma única linha de dados com uma coluna `Expression`, mas essa coluna contém a tabela aninhada a seguir.  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283016331743|0.252695851192499|  
|Water Bottle|2866|0.192620471805901|0.175205052318795|  
|Patch Kit|2113|0.142012232004839|0.132389356196586|  
|Mountain Tire Tube|1992|0.133879965051415|0.125304947722259|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40;&#41;DMX](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;&#41;DMX](../dmx/general-prediction-functions-dmx.md)  
  
  
