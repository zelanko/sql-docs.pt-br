---
title: Dimensões (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b2703122b67debf0749abcd2ea01114fb6ecaa06
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63248139"
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
 Se o número de uma hierarquia for especificado, o **dimensões** função retorna o número da hierarquia de uma hierarquia cuja posição baseada em zero dentro do cubo é especificada.  
  
 Se um nome de hierarquia for especificado, o **dimensões** função retorna a hierarquia especificada. Normalmente, você pode usar esta versão de cadeia de caracteres da **dimensões** função com funções definidas pelo usuário.  
  
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
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
