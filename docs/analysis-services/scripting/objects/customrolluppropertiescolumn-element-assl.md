---
title: Elemento CustomRollupPropertiesColumn (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: CustomRollupPropertiesColumn Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: CustomRollupPropertiesColumn
helpviewer_keywords: CustomRollupPropertiesColumn element
ms.assetid: 7f4a9825-c768-4523-acb3-511a5160fd44
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 54d0f48463a629c0c8b34a31df6c82900b79f9c6
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="customrolluppropertiescolumn-element-assl"></a>Elemento CustomRollupPropertiesColumn (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Define os detalhes de uma coluna que fornece as propriedades de uma fórmula de acúmulo personalizado.  
  
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
  
## <a name="remarks"></a>Comentários  
 Para obter informações adicionais sobre o **DataItem** tipo, incluindo uma tabela de objetos do Analysis Services Scripting Language (ASSL) e propriedades do **DataItem** de tipo, consulte [dados DataItem Tipo de &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
 O elemento que corresponde ao pai do **CustomRollupPropertiesColumn** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento CustomRollupColumn &#40; ASSL &#41;](../../../analysis-services/scripting/objects/customrollupcolumn-element-assl.md)   
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
