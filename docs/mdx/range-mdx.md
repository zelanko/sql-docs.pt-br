---
title: ': (Intervalo) (MDX) | Microsoft Docs'
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 152158128a58cc2df12c0975b9c00976800fe64d
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581188"
---
# <a name="-range-mdx"></a>: (Intervalo) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Executa uma operação definida que retorna um conjunto ordenado naturalmente, com dois membros especificados como pontos de extremidade, e todos os membros entre os dois membros especificados incluídos como membros do conjunto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member_Expression : Member_Expression      
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="return-value"></a>Valor retornado  
 Um conjunto que contém os membros especificados e todos os membros entre os membros especificados.  
  
## <a name="remarks"></a>Remarks  
 Ambos os parâmetros devem especificar membros dentro do mesmo nível e hierarquia de uma determinada dimensão. Se ambos os parâmetros especificam o mesmo membro, o **: (intervalo)** retorna um conjunto que contém o membro especificado. Se o primeiro parâmetro for nulo, o conjunto irá conter todos os membros desde o início do nível do membro especificado no segundo parâmetro até e incluindo esse membro. Se o segundo parâmetro for nulo, o conjunto irá conter todos os membros do membro especificado no primeiro parâmetro até e incluindo o último membro no mesmo nível.  
  
 Esse operador de conjunto não tem nenhum equivalente funcional no MDX.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir demonstra o uso desse operador.  
  
```  
-- This query returns the freight cost per user  
-- for products, averaged by month, for the first quarter.  
With Member [Measures].[Freight Per Customer] as  
 (  
     [Measures].[Internet Freight Cost]  
     /   
     [Measures].[Customer Count]  
)  
  
SELECT   
    {[Ship Date].[Calendar].[Month].&[2004]&[1] : [Ship Date].[Calendar].[Month].&[2004]&[3]} ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Freight Per Customer])  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
