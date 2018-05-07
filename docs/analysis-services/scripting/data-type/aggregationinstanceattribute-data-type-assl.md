---
title: Tipo de dados AggregationInstanceAttribute (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 66bbd4ac60351c24a4705c857f18248fdea4f946
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="aggregationinstanceattribute-data-type-assl"></a>Tipo de dados AggregationInstanceAttribute (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define um tipo de dados primitivos que representa informações sobre um atributo usado por uma instância de agregação.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AggregationInstanceAttribute>  
   <AttributeID>...</AttributeID>  
   <KeyColumns>...</KeyColumns>  
</AggregationInstanceAttribute>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhuma|  
|Tipos de dados derivados|Nenhuma|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|[AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md), [KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md)|  
|Elementos derivados|[Atributo](../../../analysis-services/scripting/objects/attribute-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.AggregationInstanceAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
