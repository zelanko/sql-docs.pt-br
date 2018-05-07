---
title: Latência (DMX) | Microsoft Docs
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
- LAG
dev_langs:
- DMX
helpviewer_keywords:
- Lag function
ms.assetid: 2da6df1a-5506-4871-a0f0-83292f1df41e
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 929924bc7ef571a64bc4d7f6c26d20dece081821
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="lag-dmx"></a>Latência (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna a fração de tempo entre a data do caso atual e a última data do conjunto de treinamento.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Lag()  
```  
  
## <a name="return-type"></a>Tipo de retorno  
 Valor escalar do número inteiro de tipo.  
  
## <a name="remarks"></a>Remarks  
 Se o **latência** função é usada em um modelo em que a coluna KEY TIME está localizada dentro de uma tabela aninhada, a função deve ser localizada dentro da instrução de Subseleção.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna casos que se encaixam nos últimos 12 meses da data usada para treinar o modelo.  
  
```  
SELECT * FROM [Forecasting].CASES  
WHERE Lag() < 12  
```  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funções de previsão geral &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
