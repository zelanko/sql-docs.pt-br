---
title: Operadores aritméticos | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4bf4a182c73acb18d649de3888f735f8842964dc
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34576948"
---
# <a name="arithmetic-operators"></a>Operadores aritméticos
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Use operadores aritméticos em linguagem MDX para qualquer cálculo aritmético, incluindo adição, subtração, multiplicação e divisão.  
  
 O MDX oferece suporte para os operadores aritméticos listados na tabela a seguir.  
  
|Operador|Description|  
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
  
-   Quando todos os operadores aritméticos em uma expressão tem o mesmo nível de precedência, a ordem de execução é da esquerda para direita.  
  
-   Expressões entre parênteses têm precedência sobre todas as outras operações.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operadores &#40;sintaxe MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
  
