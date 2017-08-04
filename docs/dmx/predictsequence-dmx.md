---
title: PredictSequence (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PredictSequence
dev_langs:
- DMX
helpviewer_keywords:
- PredictSequence function
ms.assetid: c2992dfc-b99d-4430-8dcd-21ad3ffd4590
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e9ddd402be082937ec828a86d82a238d121e55dd
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="predictsequence-dmx"></a>PredictSequence (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 Se o  *n*  parâmetro for especificado, ele retorna os seguintes valores:  
  
-   Se  *n*  é maior que zero, os valores de sequência mais prováveis nas próximas  *n*  etapas.  
  
-   Se ambos os *n-start* e *n-end* forem especificados, os valores de sequência de *n-start* para *n-end*.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna uma sequência de cinco produtos com mais probabilidade de serem comprados por um cliente do banco de dados da [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)], com base no modelo de mineração MSC.  
  
```  
SELECT  
  PredictSequence([Sequence Clustering].[v Assoc Seq Line Items],5)  
From  
  [Sequence Clustering]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40; DMX &#41; Referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Funções de previsão geral &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  

