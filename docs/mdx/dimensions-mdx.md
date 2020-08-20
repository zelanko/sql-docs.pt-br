---
description: Dimensions (MDX)
title: Dimensões (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c98167516f9e01525ecd351389c885c48626636e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491413"
---
# <a name="dimensions-mdx"></a>Dimensions (MDX)


  Retorna uma hierarquia especificada por uma expressão numérica ou de cadeia de caracteres.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Numeric expression syntax  
Dimensions(Hierarchy_Number)  
  
String expression syntax  
Dimensions(Hierarchy_Name)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Hierarchy_Number*  
 Uma expressão numérica válida que especifica o número de uma hierarquia.  
  
 *Hierarchy_Name*  
 Uma expressão de cadeia de caracteres válida que especifica o nome de uma hierarquia.  
  
## <a name="remarks"></a>Comentários  
 Se um número de hierarquia for especificado, a função **Dimensions** retornará uma hierarquia cuja posição baseada em zero dentro do cubo é o número de hierarquia especificado.  
  
 Se um nome de hierarquia for especificado, a função **Dimensions** retornará a hierarquia especificada. Normalmente, você usa essa versão de cadeia de caracteres da função **Dimensions** com funções definidas pelo usuário.  
  
> [!NOTE]  
>  A dimensão **medidas** é sempre representada por `Dimensions(0)` .  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir usam a função **Dimensions** para retornar o nome, a contagem de níveis e a contagem de membros de uma hierarquia especificada, usando uma expressão numérica e uma expressão de cadeia de caracteres.  
  
```  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Name  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Levels.Count  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Members.Count  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Name  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Levels.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Members.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
