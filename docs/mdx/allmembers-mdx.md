---
description: AllMembers (MDX)
title: Todos os membros (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ba70d4ad8b301cbd8af2fd76ce058f2dab2e4a4c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461668"
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
 *Hierarchy_Expression*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
 *Level_Expression*  
 Uma linguagem MDX válida que retorna um nível.  
  
## <a name="remarks"></a>Comentários  
 A função **Mymembers** retorna um conjunto que contém todos os membros, que inclui membros calculados, na hierarquia ou no nível especificado. A função **Mymembers** retorna os membros calculados mesmo se a hierarquia ou o nível especificado não contiver nenhum membro visível.  
  
> [!IMPORTANT]  
>  Quando uma dimensão contém apenas uma única hierarquia visível, a hierarquia pode ser mencionada pelo nome da dimensão ou pelo nome da hierarquia porque o nome da dimensão, nesse caso, é resolvido apenas na hierarquia visível. Por exemplo, `Measures.AllMembers` é uma expressão MDX válida porque é resolvida na única hierarquia da dimensão Measures.  
  
> [!NOTE]  
>  A função **Mymembers** é semanticamente semelhante à função [AddCalculatedMembers (MDX)](../mdx/addcalculatedmembers-mdx.md) .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todos os membros na [ `Date].[Calendar Year]` hierarquia de atributo no eixo de coluna, incluindo membros calculados e o conjunto de todos os filhos da `[Product].[Model Name]` hierarquia de atributo no eixo de linha do cubo **Adventure Works** .  
  
```  
SELECT  
   [Date].[Calendar Year].AllMembers ON COLUMNS,  
   [Product].[Model Name].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
 O exemplo a seguir retorna todos os membros da dimensão **medidas** no eixo de coluna, incluindo todos os membros calculados e o conjunto de todos os filhos da `[Product].[Model Name]` hierarquia de atributo no eixo de linha do cubo **Adventure Works** .  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [AddCalculatedMembers&#41;MDX &#40;](../mdx/addcalculatedmembers-mdx.md)   
 [&#41;de &#40;MDX de filhos ](../mdx/children-mdx.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
