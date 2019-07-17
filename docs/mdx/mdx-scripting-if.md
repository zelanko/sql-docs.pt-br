---
title: Se a instrução (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 41bd34fbd3d296f4aa38877e6d26e25eba9ae726
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138688"
---
# <a name="mdx-scripting---if"></a>Script MDX – IF


  Executa uma instrução se a condição for verdadeira.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IF expression THEN assignment END IF  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expressão*  
 Uma expressão MDX (Multidimensional Expressions) avaliada como um booliano que retorna verdadeiro ou falso.  
  
 *assignment*  
 Uma expressão MDX que atribui um valor a um subcubo ou uma propriedade calculada.  
  
## <a name="remarks"></a>Comentários  
 Use a instrução IF para fluxo de controle, que é diferente de [IIf &#40;MDX&#41; ](../mdx/iif-mdx.md) função e o [instrução CASE &#40;MDX&#41; ](../mdx/case-statement-mdx.md) que só pode ser usado para retornar valores ou objetos.  
  
## <a name="examples"></a>Exemplos  
 No exemplo a seguir, o escopo é restringido ao nível País da hierarquia Geografia do Cliente na dimensão Clientes. Se a medida atual for Quantidade de Vendas pela Internet, esse valor será definido como 10:  
  
 `SCOPE ([Customer].[Customer Geography].[Country].MEMBERS);`  
  
 `IF Measures.CurrentMember IS [Measures].[Internet Sales Amount] THEN this = 10 END IF;`  
  
 `END SCOPE`;  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
