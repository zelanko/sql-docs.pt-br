---
title: "Dimensões (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: Dimensions
dev_langs: kbMDX
helpviewer_keywords: Dimensions function
ms.assetid: 64f63aa0-ef74-4415-a0c9-8acc6cd81739
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 3f72a2c998b9bff25494a14bdd35ed6f599b85e6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="dimensions-mdx"></a>Dimensions (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 Se o número de uma hierarquia for especificado, o **dimensões** função retorna o número da hierarquia de uma hierarquia cuja posição baseada em zero dentro do cubo é especificada.  
  
 Se um nome de hierarquia for especificado, o **dimensões** função retorna a hierarquia especificada. Normalmente, você pode usar esta versão de cadeia de caracteres do **dimensões** função com funções definidas pelo usuário.  
  
> [!NOTE]  
>  O **medidas** dimensão sempre é representada pelo `Dimensions(0)`.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir usam o **dimensões** função para retornar o nome, a contagem de níveis e a contagem de membros de uma hierarquia especificada, usando uma expressão numérica e uma expressão de cadeia de caracteres.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
