---
title: OR (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ae6b6602d7968bb444dcf4838537bb000b97dd53
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63278254"
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
  
## <a name="return-value"></a>Valor retornado  
 Um valor booliano que retorna **verdadeira** se um ou ambos os argumentos forem avaliados como **verdadeiro**; caso contrário, **false**.  
  
## <a name="remarks"></a>Comentários  
 O **ou** operador trata ambos os argumentos como valores boolianos (zero, 0, como **falso**; caso contrário, **verdadeiro**) antes que o operador realize a disjunção lógica. A tabela a seguir ilustra como o **ou** operador executa a disjunção lógica.  
  
|*Expression1*|*Expression2*|Valor retornado|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**true**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
|**false**|**false**|**false**|  
  
## <a name="example"></a>Exemplo  
 A consulta a seguir contém uma medida calculada que retorna a cadeia de caracteres "CASADO ou HOMEM" se o membro atual na hierarquia de Gênero da dimensão cliente for Masculino ou o membro atual na hierarquia Status matrimonial da dimensão cliente for casado; Caso contrário, ele retorna a cadeia de caracteres "Sem CASAMENTO ou FEMALE".  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
