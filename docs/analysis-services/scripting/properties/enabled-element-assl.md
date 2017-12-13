---
title: Habilitado (ASSL) do elemento | Microsoft Docs
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
apiname: Enabled Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Enabled
helpviewer_keywords: Enabled element
ms.assetid: dbe57903-75c0-4060-a2b3-eab241d7469f
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d4272a37a3d8a7017ad7074bcc929fe10e0d77b3
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="enabled-element-assl"></a>Elemento Enabled (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Indica se o elemento pai está habilitado.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CubeHierarchy> <!-- or ProactiveCaching -->  
   ...  
   <Enabled>...</Enabled>  
   ...  
</CubeHierarchy>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Boolean|  
|Valor padrão|Verdadeiro|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md), [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Os elementos que correspondem aos pais de **habilitado** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.CubeHierarchy> e <xref:Microsoft.AnalysisServices.ProactiveCaching>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
