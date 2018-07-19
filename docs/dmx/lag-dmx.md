---
title: Latência (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0f984e50b2c6a800a66f689d88b21dfcb487e282
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38042824"
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
 Se o **Lag** função é usada em um modelo em que a coluna KEY TIME está localizada dentro de uma tabela aninhada, a função deve ser localizada dentro da instrução de Subseleção.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna casos que se encaixam nos últimos 12 meses da data usada para treinar o modelo.  
  
```  
SELECT * FROM [Forecasting].CASES  
WHERE Lag() < 12  
```  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
