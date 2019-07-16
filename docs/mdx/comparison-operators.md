---
title: Operadores de comparação | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4e3aa00334d98af02521005679174feb3b28c55f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001517"
---
# <a name="comparison-operators"></a>Operadores de comparação


  Os operadores de comparação são usados com dados escalares. Você pode usar operadores de comparação em qualquer linguagem MDX.  
  
 Para verificar uma condição, você também pode usar operadores de comparação em instruções MDX e funções, como o MDX [IIf](../mdx/iif-mdx.md) função. No entanto, se os operadores de comparação forem usados para verificar uma condição, certifique-se de que você tem as permissões adequadas antes de tentar alterar os dados com base nessa condição. Qualquer um que tenha acesso aos dados reais e possa consultá-los pode usar operadores de comparação em consultas adicionais. Mas esse acesso não indica que essas pessoas têm ou devem ter as permissões adequadas para alterar dados. Além disso, para manter a integridade dos dados, limite o número de pessoas que podem consultar e alterar os dados.  
  
 Os operadores de comparação avaliam um tipo de dados booliano, retornando TRUE ou FALSE com base no resultado da condição testada.  
  
 O MDX oferece suporte para os operadores de comparação listados na tabela a seguir.  
  
|Operador|Descrição|  
|--------------|-----------------|  
|[= (Igual a)](../mdx/equal-to-mdx.md)|Para argumentos não nulos, retorna TRUE se o argumento esquerdo for igual ao argumento direito; caso contrário, retorna FALSE.<br /><br /> Se um ou dois argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo, a não ser que a comparação `0=null` seja feita; nesse caso, o valor booliano contém TRUE.|  
|[<> (Diferente de)](../mdx/not-equal-to-mdx.md)|Para argumentos não nulos, retorna TRUE se o argumento esquerdo não for igual ao argumento direito; caso contrário, retorna FALSE.<br /><br /> Se um ou os dois argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[> (Maior que)](../mdx/greater-than-mdx.md)|Para argumentos não nulos, retorna TRUE se o argumento esquerdo tiver um valor maior que o argumento direito; caso contrário, retorna FALSE.<br /><br /> Se um ou os dois argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[>= (Maior ou igual a)](../mdx/greater-than-or-equal-to-mdx.md)|Para argumentos não nulos, retorna TRUE se o argumento esquerdo tiver um valor maior ou igual ao argumento direito; caso contrário, retorna FALSE.<br /><br /> Se um ou os dois argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[< (Menor que)](../mdx/less-than-mdx.md)|Para argumentos não nulos, retorna TRUE se o argumento esquerdo tiver um valor que é menor que o argumento direito; Caso contrário, FALSE.<br /><br /> Se um ou os dois argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[<= (Menor ou igual a)](../mdx/less-than-or-equal-to-mdx.md)|Para argumentos não nulos, retorna TRUE se o argumento esquerdo tiver um valor menor ou igual ao argumento direito; caso contrário, retorna FALSE.<br /><br /> Se um ou os dois argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operadores &#40;sintaxe MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
  
