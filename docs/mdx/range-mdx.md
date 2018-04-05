---
title: ': (Intervalo) (MDX) | Microsoft Docs'
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
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
ms.workload: Inactive
ms.openlocfilehash: e9ca2a16a74ce772ce7737c6c30581522d6d30f1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
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
  
## <a name="return-value"></a>Valor de retorno  
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
  
## <a name="see-also"></a>Consulte Também  
 [Referência de operador MDX &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
