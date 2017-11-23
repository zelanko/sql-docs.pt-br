---
title: Ancestral (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: ANCESTOR
dev_langs: kbMDX
helpviewer_keywords: Ancestor function
ms.assetid: b5bf2ce4-20df-4ebc-97eb-e44a6f64cc50
caps.latest.revision: "46"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2efc34d667dbb8a60925583f0f0b1615402c7f6c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="ancestor-mdx"></a>Ancestor (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Uma função que retorna o ancestral de um membro especificado em um nível especificado, ou à distância especificada, a partir do membro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Level syntax  
Ancestor(Member_Expression, Level_Expression)  
  
Numeric syntax  
Ancestor(Member_Expression, Distance)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
 *Level_Expression*  
 Uma linguagem MDX válida que retorna um nível.  
  
 *Distância*  
 Uma expressão numérica válida que especifica a distância do membro especificado.  
  
## <a name="remarks"></a>Comentários  
 Com o **ancestral** função, que você fornecer a função com uma expressão de membro MDX e, em seguida, forneça o uma expressão MDX de um nível que é um ancestral do membro ou uma expressão numérica que representa o número de níveis acima daquele membro. Com essas informações, o **ancestrais** função retorna o membro ancestral nesse nível.  
  
> [!NOTE]  
>  Para retornar um conjunto que contém o membro ancestral, em vez de apenas o membro ancestral, use o [ancestrais &#40; MDX &#41; ](../mdx/ancestors-mdx.md) função.  
  
 Se uma expressão de nível for especificada, o **ancestral** função retorna o ancestral de um membro especificado no nível especificado. Se o membro especificado não estiver dentro da mesma hierarquia que o nível especificado, a função retornará um erro.  
  
 Se uma distância for especificada, o **ancestral** função retorna o ancestral do membro especificado é o número de etapas especificadas na hierarquia especificada por uma expressão de membro. Um membro pode ser especificado como um membro de uma hierarquia de atributo, uma hierarquia definida pelo usuário ou, em alguns casos, uma hierarquia pai-filho. Um número 1 retorna o pai de um membro e um número 2 retorna o avô do membro (se houver um). Zero retorna o membro em si.  
  
> [!NOTE]  
>  Use este formulário do **ancestral** função para casos em que o nível do pai é desconhecido ou não pode ser nomeado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa uma expressão de nível e retorna o Valor de Vendas pela Internet para cada Estado-Província da Austrália e seu percentual do Valor de Vendas pala Internet para a Austrália.  
  
```  
WITH MEMBER Measures.x AS [Measures].[Internet Sales Amount] /   
   (  
   [Measures].[Internet Sales Amount],    
      Ancestor   
         (  
         [Customer].[Customer Geography].CurrentMember,  
            [Customer].[Customer Geography].[Country]  
         )  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{  
   Descendants   
      (  
        [Customer].[Customer Geography].[Country].&[Australia],  
           [Customer].[Customer Geography].[State-Province], SELF   
      )  
} ON 1  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir usa uma expressão numérica e retorna o Valor de Vendas pela Internet para cada Estado-Província da Austrália e seu percentual do Valor de Vendas pala Internet para todos os países.  
  
```  
WITH MEMBER Measures.x AS [Measures].[Internet Sales Amount] /   
   (  
      [Measures].[Internet Sales Amount],  
         Ancestor   
            ([Customer].[Customer Geography].CurrentMember, 2)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{  
   Descendants   
      (  
         [Customer].[Customer Geography].[Country].&[Australia],  
            [Customer].[Customer Geography].[State-Province], SELF   
      )  
} ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
