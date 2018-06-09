---
title: OU (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 668e8f1955290c31ee63ca5b81fc5e9c286d54c4
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742445"
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
 Um valor booliano que retorna **true** se um ou ambos os argumentos forem avaliados como **true**; caso contrário, **false**.  
  
## <a name="remarks"></a>Remarks  
 O **ou** operador trata ambos os argumentos como valores boolianos (zero, 0, como **false**; caso contrário, **true**) antes que o operador realize a disjunção lógica. A tabela a seguir ilustra como o **ou** operador executa a disjunção lógica.  
  
|*Expression1*|*Expression2*|Valor retornado|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**true**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
|**false**|**false**|**false**|  
  
## <a name="example"></a>Exemplo  
 A consulta a seguir contém uma medida calculada que retorna a cadeia de caracteres "CASADO OU HOMEM" (MARRIED OR MALE) se o membro atual na hierarquia de Gênero da dimensão de Cliente for Masculino ou o membro atual na hierarquia Status Matrimonial da dimensão de Cliente for Casado; caso contrário, ela retornará a cadeia de caracteres "MULHER OU SOLTEIRA" (UNMARRIED OR FEMALE).  
  
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
  
  
