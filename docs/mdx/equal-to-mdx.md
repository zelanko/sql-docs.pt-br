---
description: = (Igual a) (MDX)
title: = (Igual a) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5ec3cbcb928926d02dd6597116f8ce9af00bf8e4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494929"
---
# <a name="-equal-to-mdx"></a>= (Igual a) (MDX)


  Realiza uma operação de comparação que determina se o valor de uma expressão MDX (Multidimensional Expressions) é igual ao valor de outra expressão MDX.  
  
> [!NOTE]  
>  Para comparar objetos, use o operador [IS &#40;MDX&#41;](../mdx/is-mdx.md) . Por exemplo, use o operador IS quando você estiver verificando se o membro atual em um eixo de consulta é um membro específico.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
MDX_Expression = MDX_Expression   
```  
  
#### <a name="parameters"></a>Parâmetros  
 *MDX_Expression*  
 Uma expressão MDX válida.  
  
## <a name="return-value"></a>Valor de retorno  
 Um valor booliano baseado nas seguintes condições:  
  
-   **true** se o valor do primeiro parâmetro for igual ao valor do segundo parâmetro.  
  
-   **false** se o valor do primeiro parâmetro não for igual ao valor do segundo parâmetro.  
  
-   **true** se ambos os parâmetros forem nulos ou se um parâmetro for NULL e o outro parâmetro for 0.  
  
## <a name="examples"></a>Exemplos  
 A consulta a seguir mostra exemplos destas condições:  
  
 `With`  
  
 `--Returns true`  
  
 `Member [Measures].bool1 as 1=1`  
  
 `--Returns false`  
  
 `Member [Measures].bool2 as 1=0`  
  
 `--Returns true`  
  
 `Member [Measures].bool3 as null=null`  
  
 `--Returns true`  
  
 `Member [Measures].bool4 as 0=null`  
  
 `--Returns false`  
  
 `Member [Measures].bool5 as 1=null`  
  
 `Select {[Measures].bool1,[Measures].bool2,[Measures].bool3,[Measures].bool4,[Measures].bool5}`  
  
 `On 0`  
  
 `From [Adventure Works]`  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de operador MDX &#40;&#41;MDX ](../mdx/mdx-operator-reference-mdx.md)  
  
  
