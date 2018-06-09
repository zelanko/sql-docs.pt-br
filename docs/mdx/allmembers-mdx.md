---
title: AllMembers (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 92cde0acf07f62d0678da6dd96efa707dedc1a1f
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34739665"
---
# <a name="allmembers-mdx"></a>AllMembers (MDX)


  Avalia uma expressão de nível ou hierarquia e retorna um conjunto que contém todos os membros do nível ou hierarquia especificado, que inclui todos os membros calculados no nível ou hierarquia.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Hierarchy syntax  
Hierarchy_Expression.AllMembers  
  
Level syntax  
Level_Expression.AllMembers  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expressão_Hierarquia*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
 *Level_Expression*  
 Uma linguagem MDX válida que retorna um nível.  
  
## <a name="remarks"></a>Remarks  
 O **AllMembers** função retorna um conjunto que contém todos os membros, incluindo membros calculados, a hierarquia ou nível especificado. O **AllMembers** função retorna os membros calculados mesmo se a hierarquia ou nível especificado não contém nenhum membro visível.  
  
> [!IMPORTANT]  
>  Quando uma dimensão contém apenas uma única hierarquia visível, a hierarquia pode ser mencionada pelo nome da dimensão ou pelo nome da hierarquia porque o nome da dimensão, nesse caso, é resolvido apenas na hierarquia visível. Por exemplo, `Measures.AllMembers` é uma expressão MDX válida porque é resolvida na única hierarquia da dimensão Measures.  
  
> [!NOTE]  
>  O **AllMembers** função é semanticamente semelhante do [AddCalculatedMembers (MDX)](../mdx/addcalculatedmembers-mdx.md) função.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todos os membros de [`Date].[Calendar Year]` hierarquia de atributo no eixo da coluna, isso inclui membros calculados e o conjunto de todos os filhos do `[Product].[Model Name]` hierarquia no eixo da linha de atributo a **Adventure Works** cubo.  
  
```  
SELECT  
   [Date].[Calendar Year].AllMembers ON COLUMNS,  
   [Product].[Model Name].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
 O exemplo a seguir retorna todos os membros de **medidas** dimensão no eixo da coluna, isso inclui todos os membros calculados e o conjunto de todos os filhos do `[Product].[Model Name]` hierarquia no eixo da linha de atributo a **Adventure Works** cubo.  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [AddCalculatedMembers &#40;MDX&#41;](../mdx/addcalculatedmembers-mdx.md)   
 [Filhos &#40;MDX&#41;](../mdx/children-mdx.md)   
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
