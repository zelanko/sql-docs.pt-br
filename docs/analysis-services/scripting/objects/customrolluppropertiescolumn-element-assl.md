---
title: Elemento CustomRollupPropertiesColumn (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fa9c3fa0ed54db502c4843f65ea9055e02d5a30e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="customrolluppropertiescolumn-element-assl"></a>Elemento CustomRollupPropertiesColumn (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define os detalhes de uma coluna que fornece as propriedades de uma fórmula de acúmulo personalizada.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <CustomRollupPropertiesColumn xsi:type="DataItem">...</CustomRollupPropertiesColumn>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[O item de dados](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 Para obter informações adicionais sobre o **DataItem** tipo, incluindo uma tabela de objetos do Analysis Services Scripting Language (ASSL) e propriedades do **DataItem** de tipo, consulte [dados DataItem Tipo &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
 O elemento que corresponde ao pai do **CustomRollupPropertiesColumn** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento CustomRollupColumn &#40;ASSL&#41;](../../../analysis-services/scripting/objects/customrollupcolumn-element-assl.md)   
 [Objetos de & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
