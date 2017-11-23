---
title: = (Igual a) (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: =
dev_langs: kbMDX
helpviewer_keywords:
- equals operator (=)
- = (equals operator)
ms.assetid: 5e1f3b58-a646-4fc1-a3f1-19090a5437b7
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: bd73ffe855c5bd4053aecfacfe41183b92e8457e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="-equal-to-mdx"></a>= (Igual a) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Realiza uma operação de comparação que determina se o valor de uma expressão MDX (Multidimensional Expressions) é igual ao valor de outra expressão MDX.  
  
> [!NOTE]  
>  Para comparar objetos, use o [IS &#40; MDX &#41; ](../mdx/is-mdx.md) operador. Por exemplo, use o operador IS quando você estiver verificando se o membro atual em um eixo de consulta é um membro específico.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
MDX_Expression = MDX_Expression   
```  
  
#### <a name="parameters"></a>Parâmetros  
 *MDX_Expression*  
 Uma expressão MDX válida.  
  
## <a name="return-value"></a>Valor de retorno  
 Um valor booliano baseado nas seguintes condições:  
  
-   **True** se o valor do primeiro parâmetro for igual ao valor do segundo parâmetro.  
  
-   **False** se o valor do primeiro parâmetro não for igual ao valor do segundo parâmetro.  
  
-   **True** se ambos os parâmetros forem nulos, ou um parâmetro for nulo e o outro parâmetro é 0.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
