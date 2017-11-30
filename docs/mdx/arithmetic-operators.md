---
title: "Operadores aritméticos | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: arithmetic operators
ms.assetid: 1dff3e20-fe9d-4155-bf06-27d6458188e9
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 4f441cec66ad8d1a4f2610a81c096662fdcdca87
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="arithmetic-operators"></a>Operadores aritméticos
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Use operadores aritméticos em linguagem MDX para qualquer cálculo aritmético, incluindo adição, subtração, multiplicação e divisão.  
  
 O MDX oferece suporte para os operadores aritméticos listados na tabela a seguir.  
  
|Operador|Description|  
|--------------|-----------------|  
|[+ (Somar)](../mdx/add-mdx.md)|Soma dois números.|  
|[/ (Divisão)](../mdx/divide-mdx-operator-reference.md)|Divide um número pelo outro.|  
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
 [Referência de operador MDX &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operadores &#40; Sintaxe MDX &#41;](../mdx/operators-mdx-syntax.md)  
  
  
