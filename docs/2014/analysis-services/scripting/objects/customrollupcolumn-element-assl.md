---
title: Elemento CustomRollupColumn (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CustomRollupColumn Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CustomRollupColumn
helpviewer_keywords:
- CustomRollupColumn element
ms.assetid: 8c825f16-0d17-4ff8-bc18-b52cf11edba7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aa183bf49cb013f8cc23e2f991ef4ee8cbd184c5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48149306"
---
# <a name="customrollupcolumn-element-assl"></a>Elemento CustomRollupColumn (ASSL)
  Define os detalhes da coluna que fornece uma fórmula de acúmulo personalizada.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <CustomRollupColumn xsi:type="DataItem">...</CustomRollupColumn>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre o `DataItem` tipo, incluindo uma tabela de objetos do Analysis Services Scripting Language (ASSL) e propriedades do `DataItem` de tipo, consulte [tipo de dados DataItem &#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md).  
  
 O elemento que corresponde ao pai de `CustomRollupColumn` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
