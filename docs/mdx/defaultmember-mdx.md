---
title: DefaultMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3a0c11acadcbdcadfd9398baff09db9292c87eb2
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740125"
---
# <a name="defaultmember-mdx"></a>DefaultMember (MDX)


  Retorna o membro padrão de uma hierarquia.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Hierarchy_Expression.DefaultMember  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expressão_Hierarquia*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
## <a name="remarks"></a>Remarks  
 O membro padrão em um atributo é usado para avaliar as expressões quando um atributo não for incluído em uma consulta.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa o **DefaultMember** função, em conjunto com o **nome** função para retornar o membro padrão para a dimensão de moeda de destino no cubo Adventure Works. O exemplo retorna **dólar americano**. O **nome** função é usada para retornar o nome da medida em vez da propriedade padrão de medida, que é **valor**.  
  
```  
WITH MEMBER Measures.x AS   
   [Destination Currency].[Destination Currency].DefaultMember.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Definir um membro padrão](../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)  
  
  
