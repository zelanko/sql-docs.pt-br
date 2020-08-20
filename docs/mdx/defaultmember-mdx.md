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
ms.openlocfilehash: 6037d5089b9d0fa67599728ce35082432b0a570c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456666"
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
 [Definir um membro padrão](https://docs.microsoft.com/analysis-services/multidimensional-models/attribute-properties-define-a-default-member)  
  
  
