---
title: Elementos de sintaxe MDX (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b530205a5165c9be77710bf86e8600174be890dc
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581018"
---
# <a name="mdx-syntax-elements-mdx"></a>Elementos MDX Syntax (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  A linguagem MDX tem vários elementos que são usados por, ou influenciam, a maioria das instruções:  
  
|Termo|Definição|  
|----------|----------------|  
|[Identificadores](../mdx/identifiers-mdx.md)|Identificadores são os nomes de objetos como cubos, dimensões, membros e medidas.|  
|**Tipos de Dados**|Define os tipos de dados que são contidos por células, propriedades do membro e propriedades de célula. MDX aceita só o tipo de dados OLE VARIANT. Para obter mais informações sobre a coerção, a conversão e a manipulação do tipo de dados VARIANT, consulte "VARIANT e VARIANTARG" na documentação Platform SDK.|  
|[Expressões &#40;MDX&#41;](../mdx/expressions-mdx.md)|As expressões são unidades de sintaxe que [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] pode resolver para valores únicos de (escalares) ou objetos. As expressões incluem funções que retornam um único valor, uma expressão fixa e assim por diante.|  
|[Operadores](../mdx/operators-mdx-syntax.md)|Operadores são elementos de sintaxe que trabalham com uma ou mais expressões MDX simples para tornar as expressões MDX mais complexas.|  
|[Funções](../mdx/functions-mdx-syntax.md)|Funções são elementos de sintaxe que têm zero, um ou mais valores de entrada e retornam um valor escalar ou um objeto. Os exemplos incluem o [soma](../mdx/sum-mdx.md) função para adicionar vários valores, o [membros](../mdx/members-set-mdx.md) de função para retornar um conjunto de membros de uma dimensão ou nível e assim por diante.|  
|[Comentários](../mdx/comments-mdx-syntax.md)|Comentários são partes do texto inseridas em instruções MDX ou scripts para explicar o objetivo da instrução. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não executa comentários.|  
|[Palavras-chave reservadas](../mdx/reserved-keywords-mdx-syntax.md)|Palavras-chave reservadas são palavras reservadas para utilização do MDX e que não devem ser utilizadas para nomes de objetos usados em instruções MDX.|  
|[Membros, tuplas e conjuntos](../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)|Membros, tuplas e conjuntos são conceitos principais de dados multidimensionais que você deve compreender antes de criar uma consulta MDX.|  
  
## <a name="see-also"></a>Consulte também  
 [Expressões multidimensionais &#40;MDX&#41; referência](../mdx/multidimensional-expressions-mdx-reference.md)  
  
  
