---
title: ': (Intervalo) (MDX) | Microsoft Docs'
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
- ':'
dev_langs:
- kbMDX
helpviewer_keywords:
- ': (range operator)'
- range operator (:)
ms.assetid: f9b36aca-4efd-49b4-9e4f-12914c1b24a6
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b80f453f0553404d1d337e15e9194f7d4b97ccd7
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="-range-mdx"></a>: (Intervalo) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Executa uma operação definida que retorna um conjunto ordenado naturalmente, com dois membros especificados como pontos de extremidade, e todos os membros entre os dois membros especificados incluídos como membros do conjunto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member_Expression : Member_Expression      
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="return-value"></a>Valor de retorno  
 Um conjunto que contém os membros especificados e todos os membros entre os membros especificados.  
  
## <a name="remarks"></a>Comentários  
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
 [Referência de operador MDX &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

