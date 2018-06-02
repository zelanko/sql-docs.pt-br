---
title: MeasureGroupMeasures (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cf6992f80d52a98e2b242e17fc1bfff242d9dd21
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580748"
---
# <a name="measuregroupmeasures-mdx"></a>MeasureGroupMeasures (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna um conjunto de medidas que pertence ao grupo de medidas especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
MEASUREGROUPMEASURES(MeasureGroupName)  
```  
  
## <a name="arguments"></a>Argumentos  
 *MeasureGroupName*  
 Uma expressão de cadeia de caracteres válida que contém o nome do grupo de medidas a partir do qual o conjunto de medidas será recuperado.  
  
## <a name="remarks"></a>Remarks  
 A cadeia de caracteres especificada deve coincidir exatamente com o nome do grupo de medidas. Os colchetes para nomes de grupo de medidas com espaços não são necessários.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna todas as medidas no grupo de medidas Vendas da Internet no cubo Adventure Works.  
  
```  
SELECT MeasureGroupMeasures('Internet Sales') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
