---
title: OU (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- OR
dev_langs:
- kbMDX
helpviewer_keywords:
- OR operator
ms.assetid: 7634c08a-5b70-44cd-9422-6555fed6ae05
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 217b6d803e73c3b9d38865a5443d04af5afdf9f9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="or-mdx"></a>OR (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Remarks  
 O **ou** operador trata ambos os argumentos como valores boolianos (zero, 0, como **false**; caso contrário, **true**) antes que o operador realize a disjunção lógica. A tabela a seguir ilustra como o **ou** operador executa a disjunção lógica.  
  
|*Expression1*|*Expression2*|Valor de retorno|  
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
  
  
