---
title: "Operadores de comparação | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- comparison operators [MDX]
ms.assetid: 4a4bbc76-c6a2-4b19-ae75-6ac3ac14df01
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 5c022d67e874ebd333d8634e642d17a14d0b577f
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="comparison-operators"></a>Operadores de comparação
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Os operadores de comparação são usados com dados escalares. Você pode usar operadores de comparação em qualquer linguagem MDX.  
  
 Para verificar uma condição, você também pode usar operadores de comparação em instruções MDX e funções, como o MDX [IIf](../mdx/iif-mdx.md) função. No entanto, se os operadores de comparação forem usados para verificar uma condição, certifique-se de que você tem as permissões adequadas antes de tentar alterar os dados com base nessa condição. Qualquer um que tenha acesso aos dados reais e possa consultá-los pode usar operadores de comparação em consultas adicionais. Mas esse acesso não indica que essas pessoas têm ou devem ter as permissões adequadas para alterar dados. Além disso, para manter a integridade dos dados, limite o número de pessoas que podem consultar e alterar os dados.  
  
 Os operadores de comparação avaliam um tipo de dados booliano, retornando TRUE ou FALSE com base no resultado da condição testada.  
  
 O MDX oferece suporte para os operadores de comparação listados na tabela a seguir.  
  
|Operador|Description|  
|--------------|-----------------|  
|[= (Igual a)](../mdx/equal-to-mdx.md)|Para argumentos não nulos, retorna TRUE se o argumento esquerdo for igual ao argumento direito; caso contrário, retorna FALSE.<br /><br /> Se um ou dois argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo, a não ser que a comparação `0=null` seja feita; nesse caso, o valor booliano contém TRUE.|  
|[<> (Igual a)](../mdx/not-equal-to-mdx.md)|Para argumentos não nulos, retorna TRUE se o argumento esquerdo não for igual ao argumento direito; caso contrário, retorna FALSE.<br /><br /> Se um ou os dois argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[> (Maior que)](../mdx/greater-than-mdx.md)|Para argumentos não nulos, retorna TRUE se o argumento esquerdo tiver um valor maior que o argumento direito; caso contrário, retorna FALSE.<br /><br /> Se um ou os dois argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[> = (maior ou igual a)](../mdx/greater-than-or-equal-to-mdx.md)|Para argumentos não nulos, retorna TRUE se o argumento esquerdo tiver um valor maior ou igual ao argumento direito; caso contrário, retorna FALSE.<br /><br /> Se um ou os dois argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[< (Menor que)](../mdx/less-than-mdx.md)|Para argumentos não nulos, retorna TRUE se o argumento esquerdo tiver um valor menor que o argumento direito; caso contrário, retorna FALSE.<br /><br /> Se um ou os dois argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
|[< = (menor ou igual a)](../mdx/less-than-or-equal-to-mdx.md)|Para argumentos não nulos, retorna TRUE se o argumento esquerdo tiver um valor menor ou igual ao argumento direito; caso contrário, retorna FALSE.<br /><br /> Se um ou os dois argumentos forem avaliados como um valor nulo, o operador retornará um valor nulo.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operadores &#40; Sintaxe MDX &#41;](../mdx/operators-mdx-syntax.md)  
  
  

