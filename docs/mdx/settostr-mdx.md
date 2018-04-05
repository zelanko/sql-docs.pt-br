---
title: SetToStr (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SETTOSTR
dev_langs:
- kbMDX
helpviewer_keywords:
- SetToStr function
ms.assetid: b761e002-26cd-460e-b424-fb8e306746fa
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1443875129e9376210032e3431c4f77b70b35c8c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="settostr-mdx"></a>SetToStr (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna uma cadeia com formato da linguagem MDX que corresponde a um conjunto especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SetToStr(Set_Expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
## <a name="remarks"></a>Remarks  
 Essa função é usada para transferir uma representação de cadeia de caracteres de um conjunto para análise de uma função externa. A cadeia de caracteres que é retornada está entre chaves {}, com cada item do conjunto separado por uma vírgula.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna uma cadeia de caracteres que contém todos os membros da hierarquia de atributo Geography.Country.  
  
```  
WITH MEMBER Measures.x AS SetToStr (Geography.Geography.Children)  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
