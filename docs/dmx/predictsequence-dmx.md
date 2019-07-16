---
title: PredictSequence (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c6828b77af36b5dbbc50fbca0210961a7f2ed20c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041926"
---
# <a name="predictsequence-dmx"></a>PredictSequence (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Prediz valores de sequência futuros para um conjunto especificado de dados de sequência.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
PredictSequence(<table column reference>)  
PredictSequence(\<table column reference, n>)  
PredictSequence(\<table column reference, n-start, n-end>)  
```  
  
## <a name="return-type"></a>Tipo de retorno  
 Um \<expressão de tabela >.  
  
## <a name="remarks"></a>Comentários  
 Se o *n* parâmetro for especificado, ele retorna os seguintes valores:  
  
-   Se *n* é maior que zero, os valores de sequência mais prováveis nas próximas *n* etapas.  
  
-   Se os dois *n-start* e *n-end* forem especificados, a sequência de valores de *n início* para *n-end*.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna uma sequência de cinco produtos com mais probabilidade de serem comprados por um cliente do banco de dados da [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)], com base no modelo de mineração MSC.  
  
```  
SELECT  
  PredictSequence([Sequence Clustering].[v Assoc Seq Line Items],5)  
From  
  [Sequence Clustering]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
