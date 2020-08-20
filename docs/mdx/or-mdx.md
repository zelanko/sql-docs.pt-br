---
description: OR (MDX)
title: OU (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d5ea3e65dd9bad768ef829858d42d6e4adea7a72
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471748"
---
# <a name="or-mdx"></a>OR (MDX)


  Realiza uma disjunção lógica em duas expressões numéricas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Expression1 OR Expression2   
```  
  
#### <a name="parameters"></a>Parâmetros  
 Expression1  
 Uma linguagem MDX válida que retorna um valor numérico.  
  
 Expression2  
 Uma expressão MDX válida que retorna um valor numérico.  
  
## <a name="return-value"></a>Valor de retorno  
 Um valor booliano que retorna **true** se um ou ambos os argumentos forem avaliados como **true**; caso contrário, **false**.  
  
## <a name="remarks"></a>Comentários  
 O operador **or** trata os dois argumentos como valores Boolianos (zero, 0, como **false**; caso contrário, **true**) antes que o operador execute a disjunção lógica. A tabela a seguir ilustra como o operador **or** executa a disjunção lógica.  
  
|*Expression1*|*Expression2*|Valor de retorno|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**true**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
|**false**|**false**|**false**|  
  
## <a name="example"></a>Exemplo  
 A consulta a seguir contém uma medida calculada que retorna a cadeia de caracteres "casado ou masculino" se o membro atual na hierarquia de gênero da dimensão do cliente for masculino ou o membro atual na hierarquia de status civil da dimensão do cliente for casado; caso contrário, ele retorna a cadeia de caracteres "incasado ou feminino".  
  
```  
WITH  
MEMBER MEASURES.ORDEMO AS  
IIF(  
([Customer].[Gender].CURRENTMEMBER IS [Customer].[Gender].&[M])  
OR  
([Customer].[Marital Status].CURRENTMEMBER IS [Customer].[Marital Status].&[M]),  
"MARRIED OR MALE",  
"UNMARRIED OR FEMALE")  
SELECT [Customer].[Gender].[Gender].MEMBERS ON 0,  
[Customer].[Marital Status].[Marital Status].MEMBERS ON 1  
FROM [Adventure Works]  
WHERE(MEASURES.ORDEMO)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de operador MDX &#40;&#41;MDX ](../mdx/mdx-operator-reference-mdx.md)  
  
  
