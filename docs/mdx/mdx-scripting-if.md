---
description: Instrução IF (MDX)
title: Instrução IF (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 62b5a2e7d2ae04b7cd11bb08a3a65ddad903b6cc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429728"
---
# <a name="mdx-scripting---if"></a>Script MDX – IF


  Executa uma instrução se a condição for verdadeira.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IF expression THEN assignment END IF  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 Uma expressão MDX (Multidimensional Expressions) avaliada como um booliano que retorna verdadeiro ou falso.  
  
 *Design*  
 Uma expressão MDX que atribui um valor a um subcubo ou uma propriedade calculada.  
  
## <a name="remarks"></a>Comentários  
 Use a instrução IF para o fluxo de controle, que é diferente da função [IIf &#40;mdx&#41;](../mdx/iif-mdx.md) e da [instrução CASE &#40;MDX&#41;](../mdx/case-statement-mdx.md) que só pode ser usada para retornar valores ou objetos.  
  
## <a name="examples"></a>Exemplos  
 No exemplo a seguir, o escopo é restringido ao nível País da hierarquia Geografia do Cliente na dimensão Clientes. Se a medida atual for Quantidade de Vendas pela Internet, esse valor será definido como 10:  
  
 `SCOPE ([Customer].[Customer Geography].[Country].MEMBERS);`  
  
 `IF Measures.CurrentMember IS [Measures].[Internet Sales Amount] THEN this = 10 END IF;`  
  
 `END SCOPE`;  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
