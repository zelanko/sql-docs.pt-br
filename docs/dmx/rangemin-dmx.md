---
title: RangeMin (DMX) | Microsoft Docs
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
f1_keywords: RangeMin
dev_langs: DMX
helpviewer_keywords: RangeMin function
ms.assetid: 64159bbe-7016-4f67-91d9-5c5f6ceb6c25
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 16d56170a3b4c995a7c93c3f9acf699e3f4e3071
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="rangemin-dmx"></a>RangeMin (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna a parte final inferior da partição prevista que é descoberta para a coluna de dados discretos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RangeMin(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>Aplica-se a  
 Colunas escalares.  
  
## <a name="return-type"></a>Tipo de retorno  
 Valor escalar.  
  
## <a name="remarks"></a>Remarks  
 O **RangeMin** função pode ser usada em [SELECT DISTINCT FROM &#60; modelo de &#62; &#40; DMX &#41;](../dmx/select-distinct-from-model-dmx.md) consultas. Quando usada com esse tipo de consulta, a referência da coluna escalar poderá conter colunas contínuas ou distintas que são tanto previsíveis como de entrada.  
  
 Quando usado com [SELECT FROM &#60; modelo de &#62; JUNÇÃO de previsão &#40; DMX &#41; ](../dmx/select-from-model-prediction-join-dmx.md), o **RangeMin**, **RangeMid**, e **RangeMax** funções retornam os valores de limite real da partição especificada. Por exemplo, se uma previsão for realizada em uma coluna de dados discretos, a consulta retornará o número de partição previsto na coluna de dados discretos. O **RangeMin**, **RangeMid**, e **RangeMax** funções descrevem a partição que especifica a previsão. Quando o **RangeMin** função é usada com uma instrução PREDICTION JOIN, a referência de coluna escalar só pode conter colunas previsíveis discretas.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna valores mínimo, máximo e médio para a coluna contínua Yearly Income no modelo de mineração Árvore de decisão.  
  
```  
SELECT DISTINCT   
    RangeMin([Yearly Income]) AS [Bucket Minimum],  
    RangeMid([Yearly Income]) AS [Bucket Average],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Extensões de mineração de dados &#40; DMX &#41; Referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Funções de previsão geral &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [RangeMax &#40; DMX &#41;](../dmx/rangemax-dmx.md)   
 [RangeMid &#40; DMX &#41;](../dmx/rangemid-dmx.md)  
  
  
