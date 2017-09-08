---
title: "O nível (MDX) | Microsoft Docs"
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
- LEVEL
dev_langs:
- kbMDX
helpviewer_keywords:
- Level function
ms.assetid: 10bbe4ac-44bc-45c7-81a1-85423fbeaab1
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 311bbd9138a12d7f4013bd5e21538f9acae59ec9
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="level-mdx"></a>Level (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o nível de um membro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member_Expression.Level  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Um válido MDX (Multidimensional Expression) que retorna um membro.  
  
### <a name="examples"></a>Exemplos  
 O exemplo a seguir usa o **nível** função para retornar todos os meses no cubo Adventure Works.  
  
```  
SELECT[Date].[Fiscal].[Month].[February 2002].Level.Members ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir usa o **nível** função para retornar o nome do nível para o suporte de bicicleta multifuncional na hierarquia de atributo de nome do modelo no cubo Adventure Works.  
  
```  
WITH MEMBER Measures.x AS   
   [Product].[Model Name].[All-Purpose Bike Stand].Level.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

