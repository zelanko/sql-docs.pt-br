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
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63066244"
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
 O **AllMembers** função retorna um conjunto que contém todos os membros, que inclui membros calculados, no nível ou hierarquia especificado. O **AllMembers** função retorna os membros calculados mesmo se a hierarquia ou nível especificado não contém nenhum membro visível.  
  
> [!IMPORTANT]  
>  Quando uma dimensão contém apenas uma única hierarquia visível, a hierarquia pode ser mencionada pelo nome da dimensão ou pelo nome da hierarquia porque o nome da dimensão, nesse caso, é resolvido apenas na hierarquia visível. Por exemplo, `Measures.AllMembers` é uma expressão MDX válida porque é resolvida na única hierarquia da dimensão Measures.  
  
> [!NOTE]  
>  O **AllMembers** função é semanticamente semelhante para o [AddCalculatedMembers (MDX)](../mdx/addcalculatedmembers-mdx.md) função.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todos os membros na [`Date].[Calendar Year]` hierarquia de atributo no eixo da coluna, isso inclui os membros calculados e o conjunto de todos os filhos do `[Product].[Model Name]` hierarquia no eixo da linha de atributo a **Adventure Works** cubo.  
  
```  
SELECT  
   [Date].[Calendar Year].AllMembers ON COLUMNS,  
   [Product].[Model Name].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
 O exemplo a seguir retorna todos os membros a **medidas** dimensão no eixo da coluna, isso inclui todos os membros calculados e o conjunto de todos os filhos do `[Product].[Model Name]` hierarquia no eixo de linhas de atributos da **Adventure Works** cubo.  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [AddCalculatedMembers &#40;MDX&#41;](../mdx/addcalculatedmembers-mdx.md)   
 [Children &#40;MDX&#41;](../mdx/children-mdx.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
