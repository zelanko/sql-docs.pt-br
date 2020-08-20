---
description: Ancestor (MDX)
title: Ancestral (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9e08a0f281a9e48c3416bb00f6ee47322d554d9c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461658"
---
# <a name="ancestor-mdx"></a>Ancestor (MDX)


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
  
 *Alcance*  
 Uma expressão numérica válida que especifica a distância do membro especificado.  
  
## <a name="remarks"></a>Comentários  
 Com a função **Ancestor** , você fornece a função com uma expressão de membro MDX e, em seguida, fornece uma expressão MDX de um nível que é um ancestral do membro ou uma expressão numérica que representa o número de níveis acima daquele membro. Com essas informações, a função **ancestrais** retorna o membro ancestral nesse nível.  
  
> [!NOTE]  
>  Para retornar um conjunto que contém o membro ancestral, em vez de apenas o membro ancestral, use a função [ancestrais &#40;MDX&#41;](../mdx/ancestors-mdx.md) .  
  
 Se uma expressão de nível for especificada, a função **Ancestor** retornará o ancestral do membro especificado no nível especificado. Se o membro especificado não estiver dentro da mesma hierarquia que o nível especificado, a função retornará um erro.  
  
 Se uma distância for especificada, a função **Ancestor** retornará o ancestral do membro especificado que é o número de etapas especificado na hierarquia especificada pela expressão de membro. Um membro pode ser especificado como um membro de uma hierarquia de atributo, uma hierarquia definida pelo usuário ou, em alguns casos, uma hierarquia pai-filho. Um número 1 retorna o pai de um membro e um número 2 retorna o avô do membro (se houver um). Zero retorna o membro em si.  
  
> [!NOTE]  
>  Use esse formulário da função **ancestral** para casos em que o nível do pai é desconhecido ou não pode ser nomeado.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
