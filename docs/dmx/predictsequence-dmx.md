---
title: PredictSequence (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: acb1982e61e622b150ee79af08e36ddcf24048ba
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970711"
---
# <a name="predictsequence-dmx"></a>PredictSequence (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Prediz valores de sequência futuros para um conjunto especificado de dados de sequência.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
PredictSequence(<table column reference>)  
PredictSequence(\<table column reference, n>)  
PredictSequence(\<table column reference, n-start, n-end>)  
```  
  
## <a name="return-type"></a>Tipo de retorno  
 Uma \<table expression>.  
  
## <a name="remarks"></a>Comentários  
 Se o parâmetro *n* for especificado, ele retornará os seguintes valores:  
  
-   Se *n* for maior que zero, os valores de sequência mais prováveis nas próximas *n* etapas.  
  
-   Se *n-Start* e *n-end* forem especificados, os valores de sequência de *n-Start* para *n-end*.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna uma sequência de cinco produtos com mais probabilidade de serem comprados por um cliente do banco de dados da [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)], com base no modelo de mineração MSC.  
  
```  
SELECT  
  PredictSequence([Sequence Clustering].[v Assoc Seq Line Items],5)  
From  
  [Sequence Clustering]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40;&#41;DMX](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;&#41;DMX](../dmx/general-prediction-functions-dmx.md)  
  
  
