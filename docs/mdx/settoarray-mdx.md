---
title: SetToArray (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SETTOARRAY
dev_langs:
- kbMDX
helpviewer_keywords:
- SetToArray function
ms.assetid: e408c626-3a2a-4ce9-aeb4-247301334893
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 410a88cdc83839e0fbdde75f7e0c5b4192fe1e0e
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="settoarray-mdx"></a>SetToArray (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Converte um ou mais conjuntos para uma matriz para uso em uma função definida pelo usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SetToArray(Set_Expression1 [ ,Set_Expression2,...n ][ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Set_Expression2*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Numeric_Expression*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
## <a name="remarks"></a>Comentários  
 O **SetToArray** função converte um ou mais conjuntos em uma matriz para uso em uma função definida pelo usuário. O número de dimensões na matriz resultante é igual ao número de conjuntos especificados.  
  
 A expressão numérica opcional pode fornecer os valores nas células da matriz. Se uma expressão numérica não for especificada, a junção cruzada dos conjuntos será avaliada no contexto atual.  
  
 As coordenadas da célula na matriz resultante correspondem à posição dos conjuntos na lista. Por exemplo, há três conjuntos: `SA`, `SB` e `SC`. Cada um desses conjuntos tem dois elementos. A instrução MDX, `SetToArray(SA, SB, SC)`, cria a matriz tridimensional a seguir:  
  
```  
(SA1, SB1, SC1) (SA2, SB1, SC1) (SA1, SB2, SC1) (SA2, SB2, SC1)   
(SA1, SB1, SC2) (SA2, SB1, SC2) (SA1, SB2, SC2) (SA2, SB2, SC2)   
```  
  
> [!NOTE]  
>  O tipo de retorno de **SetToArray** função é o tipo de VARIANTE, VT_ARRAY. Portanto, a saída de **SetToArray** função deve ser usada somente como entrada para uma função definida pelo usuário.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna uma matriz.  
  
```  
SetToArray([Geography].[Geography].Members, [Measures].[Internet Sales Amount])  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

