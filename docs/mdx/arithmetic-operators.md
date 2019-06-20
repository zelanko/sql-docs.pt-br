---
title: Operadores aritméticos | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c422df08152eaf9266a6ca3408bfce12e023c2a3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63284519"
---
# <a name="arithmetic-operators"></a>Operadores aritméticos


  Use operadores aritméticos em linguagem MDX para qualquer cálculo aritmético, incluindo adição, subtração, multiplicação e divisão.  
  
 O MDX oferece suporte para os operadores aritméticos listados na tabela a seguir.  
  
|Operador|Descrição|  
|--------------|-----------------|  
|[+ (Somar)](../mdx/add-mdx.md)|Soma dois números.|  
|[/ (dividir)](../mdx/divide-mdx-operator-reference.md)|Divide um número pelo outro.|  
|[* (Multiplicar)](../mdx/multiply-mdx.md)|Multiplica dois números.|  
|[- (Subtrair)](../mdx/subtract-mdx.md)|Subtrai dois números.|  
|^ (Potência)|Eleva um número pelo outro.|  
  
> [!NOTE]  
>  A linguagem MDX não inclui uma função para obter a raiz quadrada de um número. Para obter a raiz quadrada de um número, eleve-o à potência de 0,5 usando o operador ^.  
  
## <a name="order-of-precedence"></a>Ordem de precedência  
 As regras a seguir determinam a ordem de prioridade dos operadores aritméticos em uma expressão MDX:  
  
-   Quando houver mais de um operador aritmético em uma expressão, o MDX efetua a multiplicação e a divisão primeiramente, seguidas da subtração e da adição.  
  
-   Quando todos os operadores aritméticos em uma expressão tem o mesmo nível de precedência, a ordem de execução é esquerda para a direita.  
  
-   Expressões entre parênteses têm precedência sobre todas as outras operações.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operadores &#40;sintaxe MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
  
