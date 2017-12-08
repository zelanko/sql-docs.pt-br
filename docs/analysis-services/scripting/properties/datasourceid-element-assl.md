---
title: Elemento DataSourceID (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DataSourceID Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DataSourceID
helpviewer_keywords: DataSourceID element
ms.assetid: 2d71ba53-1684-4da0-8da4-fb75033c971b
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f5176889adcb83b5fc1635b07658a617ebcd6b2f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="datasourceid-element-assl"></a>Elemento DataSourceID (ASSL)
  Identifica o [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md) associado ao elemento pai do elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CubeBinding> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <DataSourceID>...</DataSourceID>  
   ...  
</CubeBinding>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|Depende do contexto|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[CubeBinding](../../../analysis-services/scripting/data-type/cubebinding-data-type-out-of-line-assl.md), [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md), [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md), [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md), [QueryBinding](../../../analysis-services/scripting/data-type/querybinding-data-type-assl.md), [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md), [TableBinding](../../../analysis-services/scripting/data-type/tablebinding-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Os elementos que correspondem aos pais de **DataSourceID** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.CubeDimensionBinding>, <xref:Microsoft.AnalysisServices.DimensionBinding>, <xref:Microsoft.AnalysisServices.MeasureGroupBinding>, <xref:Microsoft.AnalysisServices.QueryBinding>, <xref:Microsoft.AnalysisServices.DataSourceView>e <xref:Microsoft.AnalysisServices.TableBinding>.  
  
## <a name="see-also"></a>Consulte também  
 [ID do elemento &#40; ASSL &#41;](../../../analysis-services/scripting/properties/id-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
