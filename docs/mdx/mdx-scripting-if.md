---
title: "Se a instrução (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: statements [MDX], IF
ms.assetid: 8830cce5-9e06-4f89-a555-295bb0d0a8a1
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 67376067c26a3eae41d0c090a141367fcf5cc396
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-scripting---if"></a>Script MDX - se
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Executa uma instrução se a condição for verdadeira.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IF expression THEN assignment END IF  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 Uma expressão MDX (Multidimensional Expressions) avaliada como um booliano que retorna verdadeiro ou falso.  
  
 *atribuição*  
 Uma expressão MDX que atribui um valor a um subcubo ou uma propriedade calculada.  
  
## <a name="remarks"></a>Remarks  
 Use a instrução IF para fluxo de controle, que é diferente de [IIf &#40; MDX &#41; ](../mdx/iif-mdx.md) função e o [instrução CASE &#40; MDX &#41; ](../mdx/case-statement-mdx.md) que só pode ser usado para retornar valores ou objetos.  
  
## <a name="examples"></a>Exemplos  
 No exemplo a seguir, o escopo é restringido ao nível País da hierarquia Geografia do Cliente na dimensão Clientes. Se a medida atual for Quantidade de Vendas pela Internet, esse valor será definido como 10:  
  
 `SCOPE ([Customer].[Customer Geography].[Country].MEMBERS);`  
  
 `IF Measures.CurrentMember IS [Measures].[Internet Sales Amount] THEN this = 10 END IF;`  
  
 `END SCOPE`;  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
