---
title: Prever (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: PREDICT
dev_langs: DMX
helpviewer_keywords: Predict function
ms.assetid: f02ff4b3-9bd7-409d-ad14-ead67b3206c4
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 448507936bab886a8d081ee487ab323a3a4a2ef4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="predict-dmx"></a>Predict (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  O **prever** função retorna um valor previsto ou conjunto de valores de uma coluna especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Predict(<scalar column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
Predict(<table column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
```  
  
## <a name="applies-to"></a>Aplica-se a  
 Uma referência de coluna escalar ou a uma referência de coluna de tabela.  
  
## <a name="return-type"></a>Tipo de retorno  
 \<referência de coluna escalar >  
  
 ou em  
  
 \<referência de coluna de tabela >  
  
 O tipo de retorno depende do tipo de coluna ao qual essa função se aplica.  
  
> [!NOTE]  
>  INCLUSIVE, EXCLUSIVE, INPUT_ONLY e INCLUDE_STATISTICS aplicam-se somente à referência da coluna da tabela, e EXCLUDE_NULL e INCLUDE_NULL aplicam-se apenas à referência da coluna escalar.  
  
## <a name="remarks"></a>Remarks  
 As opções incluem EXCLUDE_NULL (padrão), INCLUDE_NULL, INCLUSIVE, EXCLUSIVE (padrão), INPUT_ONLY e INCLUDE_STATISTICS.  
  
> [!NOTE]  
>  Para modelos de série temporal, a função de previsão não dá suporte a INCLUDE_STATISTICS.  
  
 O parâmetro INCLUDE_NODE_ID retorna a coluna $NODEID no resultado. NODE_ID é o nó de conteúdo no qual a previsão é executada para um caso particular. Esse parâmetro é opcional ao usar a previsão em colunas de tabela.  
  
 O  *n*  parâmetro se aplica a colunas de tabela. Define o número de linhas retornadas com base no tipo de previsão. Se a coluna subjacente for sequência, chamará o **PredictSequence** função. Se a coluna subjacente for série temporal, chamará o **PredictTimeSeries** função. Para tipos associativos de previsão, ele chama o **PredictAssociation** função.  
  
 O **prever** função oferece suporte a polimorfismo.  
  
 As formas abreviadas alternativas a seguir são usadas frequentemente:  
  
-   [Sexo] é uma alternativa para **prever**([sexo], EXCLUDE_NULL).  
  
-   [Compras de produtos] é uma alternativa para **prever**([compras de produtos], EXCLUDE_NULL, EXCLUSIVE).  
  
    > [!NOTE]  
    >  O próprio tipo de retorno dessa função é considerado uma referência de coluna. Isso significa que o **prever** função pode ser usada como um argumento em outras funções que usam uma referência de coluna como um argumento (exceto para o **prever** própria função).  
  
 Passar INCLUDE_STATISTICS para uma previsão em uma coluna com valor de tabela adiciona as colunas **$Probability** e **$Support** para a tabela resultante. Essas colunas descrevem a probabilidade de existência para o registro de tabela aninhada associada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa a função de previsão para retornar os quatro produtos no banco de dados Adventure Works que têm mais probabilidade de serem vendidos juntos. Como a função é previsão com relação um modelo de mineração de regras de associação, ele usa automaticamente o **PredictAssociation** funcionar conforme descrito anteriormente.  
  
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
 [Extensões de mineração de dados &#40; DMX &#41; Referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Funções de previsão geral &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
