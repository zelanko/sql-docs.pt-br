---
title: MeasureGroupMeasures (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: MeasureGroupMeasures function
ms.assetid: 69d9b205-1ca7-4741-9ca9-c7926bc87ead
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: baacb5ee83ecd45bc994cc462b04d35d6d3ca15a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="measuregroupmeasures-mdx"></a>MeasureGroupMeasures (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna um conjunto de medidas que pertence ao grupo de medidas especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
MEASUREGROUPMEASURES(MeasureGroupName)  
```  
  
## <a name="arguments"></a>Argumentos  
 *MeasureGroupName*  
 Uma expressão de cadeia de caracteres válida que contém o nome do grupo de medidas a partir do qual o conjunto de medidas será recuperado.  
  
## <a name="remarks"></a>Comentários  
 A cadeia de caracteres especificada deve coincidir exatamente com o nome do grupo de medidas. Os colchetes para nomes de grupo de medidas com espaços não são necessários.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna todas as medidas no grupo de medidas Vendas da Internet no cubo Adventure Works.  
  
```  
SELECT MeasureGroupMeasures('Internet Sales') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
