---
title: LinkMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8a00388e067878d9c2165cbae6844f8020b7c63e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67905599"
---
# <a name="linkmember-mdx"></a>LinkMember (MDX)


  Retorna o membro equivalente a um membro especificado em uma hierarquia especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
LinkMember(Member_Expression, Hierarchy_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
 *Hierarchy_Expression*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
## <a name="remarks"></a>Comentários  
 A função **LinkMember** retorna o membro da hierarquia especificada que corresponde aos valores de chave em cada nível do membro especificado em uma hierarquia relacionada. Os atributos em cada nível devem ter a mesma cardinalidade de chave e tipo de dados. Em hierarquias não naturais, se houver mais de uma correspondência para um valor de chave do atributo, o resultado será um erro ou indeterminado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa a função **LinkMember** para retornar a medida padrão no cubo Adventure Works para o ascendentes do membro 1 de julho de 2002 da hierarquia de atributo Date. Date na hierarquia do calendário.  
  
```  
SELECT  Hierarchize  
   (Ascendants   
      (LinkMember   
         ([Date].[Date].[July 1, 2002], [Date].[Calendar]  
         )  
       )  
    ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Hierarquiar &#40;&#41;MDX](../mdx/hierarchize-mdx.md)   
 [Ascendentes&#41;MDX &#40;](../mdx/ascendants-mdx.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
