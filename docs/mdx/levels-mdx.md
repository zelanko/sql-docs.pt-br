---
description: Função Levels (MDX)
title: Níveis (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f3b0a7eaea166fdefbfd947faf95b58f74bdb8be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429868"
---
# <a name="levels-mdx"></a>Função Levels (MDX)


  Retorna o nível cuja posição em uma dimensão ou hierarquia é especificada por uma expressão numérica ou cujo nome é especificado por uma expressão de cadeia de caracteres.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Numeric expression syntax  
Hierarchy_Expression.Levels( Level_Number )  
  
String expression syntax  
Hierarchy_Expression.Levels( Level_Name )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Hierarchy_Expression*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
 *Level_Number*  
 Uma expressão numérica válida que especifica um número de nível.  
  
 *Level_Name*  
 Uma expressão de cadeia de caracteres válida que especifica um nome de nível.  
  
## <a name="remarks"></a>Comentários  
 Se um número de nível for especificado, a função **Levels** retornará o nível associado à posição de base zero especificada.  
  
 Se um nome de nível for especificado, a função **Levels** retornará o nível especificado.  
  
> [!NOTE]  
>  Use a sintaxe de expressão de cadeia de caracteres para funções definidas pelo usuário.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir ilustram cada uma das sintaxes de função de **níveis** .  
  
### <a name="numeric"></a>Numérico  
 O exemplo a seguir retorna o nível País:  
  
```  
SELECT [Geography].[Geography].Levels(1) ON 0  
FROM [Adventure Works]  
```  
  
### <a name="string"></a>String  
 O exemplo a seguir retorna o nível País:  
  
```  
SELECT [Geography].[Geography].Levels('Country') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
