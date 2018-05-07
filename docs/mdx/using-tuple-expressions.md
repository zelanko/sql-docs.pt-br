---
title: Usando expressões de tupla | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- single-member tuples [MDX]
- expressions [MDX], tuples
- one-member tuples
- tuples
- implicit tuples
ms.assetid: 0b802b76-9123-405e-ae43-d438754724ba
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: fba6675213e513806f27c85fe881fc3efdeb0166
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="using-tuple-expressions"></a>Usando expressões de tupla
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Uma tupla é composta por um membro de cada dimensão contida em um cubo. Desse modo, uma tupla identifica de modo exclusivo uma única célula do cubo.  
  
> [!NOTE]  
>  Uma tupla que faz referência a um ou mais membros que não são válidos é considerada uma tupla vazia.  
  
 A expressão completa de um identificador de tupla é composta por um ou mais membros especificados explicitamente, entre parênteses:  
  
 (*Member_expression* [,*Member_expression* ...])  
  
 Uma tupla pode ser completamente qualificada, pode conter membros implícitos ou pode conter um único membro.  
  
## <a name="tuples-and-implicit-members"></a>Tuplas e membros implícitos  
 Uma tupla que especifica explicitamente um único membro de cada dimensão contida em um cubo é considerada uma tupla completamente qualificada. No entanto, uma tupla não precisa ser completamente qualificada.  
  
 Qualquer dimensão não mencionada explicitamente em uma tupla é mencionada de modo implícito. O membro para a dimensão mencionada implicitamente depende da estrutura da dimensão e das relações de atributo definidas nela. Se houver uma referência explícita a uma hierarquia na mesma dimensão da hierarquia mencionada implicitamente e houver uma relação direta ou indireta definida entre as hierarquias mencionadas explícita e implicitamente, a tupla se comportará como se contivesse o membro na hierarquia mencionada implicitamente que existe com o membro na hierarquia mencionada explicitamente. Por exemplo, se um cubo contiver uma dimensão Cliente com os atributos Cidade e País e houver uma relação definida entre esses dois atributos de modo que uma Cidade tenha um País e um País possa conter várias Cidades, a inclusão explícita da Cidade “Londres” à sua tupla fará referência implícita ao País “Reino Unido”. No entanto, se não houver nenhuma relação de atributo definida, a relação se dará na direção oposta (por exemplo, embora uma Cidade possa ter uma relação com o País, você não pode determinar a Cidade em que alguém vive sabendo somente o País de residência) ou, se não houver nenhuma relação direta entre os dois atributos definidos (poderia existir uma relação definida entre Cliente e Cidade e Cliente e País, mas nenhuma relação foi definida entre Cidade e País), as seguintes regras serão válidas:  
  
-   Se a hierarquia mencionada implicitamente tiver um membro padrão, o membro padrão será adicionado à tupla.  
  
-   Se a hierarquia mencionada implicitamente não tem nenhum membro padrão, o **(All)** membro da hierarquia padrão é usado.  
  
-   Se a hierarquia mencionada implicitamente não tiver nenhum membro padrão, o primeiro membro do nível mais alto da hierarquia será utilizado.  
  
## <a name="one-member-tuples"></a>Tuplas de um membro  
 Se a expressão de tupla tiver um único membro, o MDX converterá o membro em uma tupla de um membro para avaliar a expressão. Em outras palavras, fornecer a expressão de membro `[Measures].[TestMeasure]` em vez de uma expressão de tupla é funcionalmente equivalente à expressão de tupla `( [Measures].[TestMeasure] ).`  
  
## <a name="see-also"></a>Consulte também  
 [Expressões &#40;MDX&#41;](../mdx/expressions-mdx.md)   
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
