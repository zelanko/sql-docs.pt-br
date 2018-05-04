---
title: Níveis (MDX) | Microsoft Docs
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
- Levels
dev_langs:
- kbMDX
helpviewer_keywords:
- Levels function
ms.assetid: 1a989cc9-8aa8-4ec3-b5e9-795d6fa84983
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 0c75ebacdd811ebd64b242b74b3279d01f181c50
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="levels-mdx"></a>Função Levels (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o nível cuja posição em uma dimensão ou hierarquia é especificada por uma expressão numérica ou cujo nome é especificado por uma expressão de cadeia de caracteres.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Numeric expression syntax  
Hierarchy_Expression.Levels( Level_Number )  
  
String expression syntax  
Hierarchy_Expression.Levels( Level_Name )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expressão_Hierarquia*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
 *Level_Number*  
 Uma expressão numérica válida que especifica um número de nível.  
  
 *Level_Name*  
 Uma expressão de cadeia de caracteres válida que especifica um nome de nível.  
  
## <a name="remarks"></a>Remarks  
 Se um número de nível for especificado, o **níveis** função retorna o nível associado à posição de base zero especificada.  
  
 Se um nome de nível for especificado, o **níveis** função retorna o nível especificado.  
  
> [!NOTE]  
>  Use a sintaxe de expressão de cadeia de caracteres para funções definidas pelo usuário.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir ilustram cada o **níveis** sintaxes de função.  
  
### <a name="numeric"></a>Numérico  
 O exemplo a seguir retorna o nível País:  
  
```  
SELECT [Geography].[Geography].Levels(1) ON 0  
FROM [Adventure Works]  
```  
  
### <a name="string"></a>Cadeia de caracteres  
 O exemplo a seguir retorna o nível País:  
  
```  
SELECT [Geography].[Geography].Levels('Country') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
