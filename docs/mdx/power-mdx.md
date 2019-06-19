---
title: ^ (Power) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 20b197f66a4af496d8235d3b38eb2fa82c1921db
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63278315"
---
# <a name="-power-mdx"></a>^ (Potência) (MDX)


  Executa uma operação aritmética que eleva um número por outro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Numeric_Expression ^ Numeric_Expression  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Numeric_Expression*  
 Uma linguagem MDX válida que retorna um valor numérico.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor com o tipo de dados do parâmetro com prioridade maior.  
  
## <a name="remarks"></a>Comentários  
 As duas expressões devem ser do mesmo tipo de dados ou uma expressão deve poder ser convertida implicitamente no tipo de dados da outra expressão. Se uma expressão for avaliada como um valor nulo, o operador retornará um valor nulo.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
