---
title: Retardo (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 04b06d1cbe14ee83915bd5626337720acf9bd2a9
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83670344"
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
  
## <a name="remarks"></a>Comentários  
 Se a função **lag** for usada em um modelo em que a coluna Key time está localizada em uma tabela aninhada, a função deverá estar localizada dentro da Subseleção da instrução.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna casos que se encaixam nos últimos 12 meses da data usada para treinar o modelo.  
  
```  
SELECT * FROM [Forecasting].CASES  
WHERE Lag() < 12  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40;&#41;DMX](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;&#41;DMX](../dmx/general-prediction-functions-dmx.md)  
  
  
