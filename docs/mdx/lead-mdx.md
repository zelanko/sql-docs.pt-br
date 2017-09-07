---
title: Cliente potencial (MDX) | Microsoft Docs
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
- LEAD
dev_langs:
- kbMDX
helpviewer_keywords:
- Lead function
ms.assetid: f3250092-7b98-40b5-8dca-77e3b50734a0
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 127c84f38fe85453fa3da7ae2b1c9752b05b6ba7
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="lead-mdx"></a>Lead (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o membro que é um número especificado de posições que seguem um membro especificado junto ao nível do membro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member_Expression.Lead( Index )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
 *Índice*  
 Uma expressão numérica válida que especifica várias posições de membro.  
  
## <a name="remarks"></a>Comentários  
 As posições de membros em um nível são determinadas pela ordem natural da hierarquia de atributo. A numeração das posições se baseia em zero.  
  
 Se o lead especificado for zero (0), o **levar** função retorna o membro especificado.  
  
 Se o lead especificado for negativo, o **levar** função retorna um membro anterior.  
  
 `Lead(1)`é equivalente a [NextMember](../mdx/nextmember-mdx.md) função. `Lead(-1)`é equivalente a [PrevMember](../mdx/prevmember-mdx.md) função.  
  
 O **levar** função é semelhante ao [latência](../mdx/lag-mdx.md) funcionar, exceto que o **latência** função procura na direção oposta a **levar** função. Ou seja, `Lead(n)` é equivalente a `Lag(-n)`.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o valor para dezembro de 2001:  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lead(-2) ON 0  
FROM [Adventure Works]  
  
```  
  
 O exemplo a seguir retorna o valor para março de 2002:  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lead(1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  

