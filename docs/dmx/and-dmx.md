---
description: AND (DMX)
title: E (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 17dabee823323c63a2d36a21cd79b81e9a323803
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431198"
---
# <a name="and-dmx"></a>AND (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Realiza uma conjunção lógica em duas expressões numéricas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Expression1 AND Expression2  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Expression1*  
 Expressão DMX (Data Mining Extensions) válida que retorna um valor numérico.  
  
 *Expression2*  
 Expressão DMX válida que retorna um valor numérico.  
  
## <a name="return-value"></a>Valor de retorno  
 Valor booliano que retorna TRUE quando ambos os parâmetros avaliam como TRUE; do contrário, FALSE.  
  
## <a name="remarks"></a>Comentários  
 Os parâmetros são todos tratados como valores boolianos (0 como FALSE; do contrário, TRUE) antes de o operador realizar a conjunção lógica. A tabela a seguir lista os valores retornados com base nas várias combinações de valores de parâmetro.  
  
|Se a Expression1 for|Se a Expression2 for|O valor de retorno será|  
|-----------------------|-----------------------|---------------------|  
|TRUE|TRUE|TRUE|  
|TRUE|FALSE|FALSE|  
|FALSE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de operador de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores lógicos &#40;&#41;DMX ](../dmx/operators-logical.md)   
 [Operadores &#40;&#41;DMX ](../dmx/operators-dmx.md)  
  
  
