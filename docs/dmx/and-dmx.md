---
title: E (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ea3cacd8fe2d80e6037cf83df9eea1fd112a4b05
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86971804"
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
  
## <a name="return-value"></a>Valor Retornado  
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
 [Operadores lógicos &#40;&#41;DMX](../dmx/operators-logical.md)   
 [Operadores &#40;&#41;DMX](../dmx/operators-dmx.md)  
  
  
