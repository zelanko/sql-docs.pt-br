---
description: PredictSequence (DMX)
title: PredictSequence (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 31f99205f3e23db23c5c2a38750f75212763e8de
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426098"
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
 Um \<table expression>.  
  
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
 [Funções &#40;&#41;DMX ](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;&#41;DMX ](../dmx/general-prediction-functions-dmx.md)  
  
  
