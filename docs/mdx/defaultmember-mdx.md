---
title: DefaultMember (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 04c99c0882bd71d1ad56c8d4f42bf3744756c81b
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580238"
---
# <a name="defaultmember-mdx"></a>DefaultMember (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
  
