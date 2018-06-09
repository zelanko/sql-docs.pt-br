---
title: MemberValue (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 73a54986a951095b16465cd4934b4dfd447d38bb
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742165"
---
# <a name="membervalue-mdx"></a>MemberValue (MDX)


  Retorna o valor de um membro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member_Expression.MemberValue  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que é avaliada como um membro.  
  
## <a name="return-value"></a>Valor retornado  
 O valor do membro retornado contém as seguintes informações, listadas na ordem em que essas informações são exibidas no valor de retorno:  
  
-   A associação de valor, caso ela tenha sido definida.  
  
-   A chave com o tipo de dados originais se não houver nenhuma associação de nome ou a chave e a legenda estão ligadas a mesma coluna.  
  
-   A legenda do membro.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna a associação de valor, a chave do membro e a legenda da primeira data na dimensão Data do cubo Adventure Works.  
  
```  
WITH MEMBER Measures.ValueColumn as [Date].[Calendar].[July 1, 2001].MemberValue  
MEMBER Measures.KeyColumn as [Date].[Calendar].[July 1, 2001].Member_Key  
MEMBER Measures.NameColumn as [Date].[Calendar].[July 1, 2001].Member_Name  
  
SELECT {Measures.ValueColumn, Measures.KeyColumn, Measures.NameColumn}  ON 0  
from [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
