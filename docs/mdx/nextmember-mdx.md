---
title: NextMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4535b837d81db10f41f1445a7051678ce4fdd688
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742175"
---
# <a name="nextmember-mdx"></a>NextMember (MDX)


  Retorna o próximo membro no nível que contém um membro especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member_Expression.NextMember   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Remarks  
 O **NextMember** função retorna o próximo membro, no mesmo nível, que contém o membro especificado.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o membro Agosto de 2001 como o próximo membro para o membro Julho de 2001.  
  
```  
SELECT [Date].[Calendar].[Month].[July 2001].NextMember ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
