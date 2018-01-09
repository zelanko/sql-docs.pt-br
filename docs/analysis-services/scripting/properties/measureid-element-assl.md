---
title: Elemento MeasureID (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: MeasureID Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: MeasureID
helpviewer_keywords: MeasureID element
ms.assetid: 8457aebc-8fdd-4683-8640-baaf9d89b2a2
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6b90ac9a14b35cd0d451fa8b5298b30d5b9d7d82
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="measureid-element-assl"></a>Elemento MeasureID (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Associa um [medidas](../../../analysis-services/scripting/objects/measure-element-assl.md) elemento com o elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MeasureBinding> <!-- or AggregationInstanceMeasure, PerspectiveMeasure -->  
   ...  
   <MeasureID>...</MeasureID>  
   ...  
</MeasureBinding>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[AggregationInstanceMeasure](../../../analysis-services/scripting/data-type/aggregationinstancemeasure-data-type-assl.md), [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md), [PerspectiveMeasure](../../../analysis-services/scripting/data-type/perspectivemeasure-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Os elementos que correspondem aos pais de **MeasureID** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.AggregationInstanceMeasure>, <xref:Microsoft.AnalysisServices.MeasureBinding>, e <xref:Microsoft.AnalysisServices.PerspectiveMeasure>.  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
