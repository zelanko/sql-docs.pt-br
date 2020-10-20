---
description: DefaultMember (MDX)
title: DefaultMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7363d650073b301eba6b29d509590e22dee5661a
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196020"
---
# <a name="defaultmember-mdx"></a>DefaultMember (MDX)


  Retorna o membro padrão de uma hierarquia.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Hierarchy_Expression.DefaultMember  
```  
  
## <a name="arguments"></a>Argumentos  
 *Hierarchy_Expression*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
## <a name="remarks"></a>Comentários  
 O membro padrão em um atributo é usado para avaliar as expressões quando um atributo não for incluído em uma consulta.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa a função **DefaultMember** , em conjunto com a função **Name** , para retornar o membro padrão para a dimensão de moeda de destino no cubo Adventure Works. O exemplo retorna **dólar americano**. A função **Name** é usada para retornar o nome da medida, em vez da propriedade padrão da medida, que é **valor**.  
  
```  
WITH MEMBER Measures.x AS   
   [Destination Currency].[Destination Currency].DefaultMember.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40;&#41;MDX ](../mdx/mdx-function-reference-mdx.md)   
 [Definir um membro padrão](/analysis-services/multidimensional-models/attribute-properties-define-a-default-member)  
  
