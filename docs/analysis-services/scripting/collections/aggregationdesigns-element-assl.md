---
title: Elemento AggregationDesigns (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
apiname: AggregationDesigns Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AggregationDesigns
helpviewer_keywords: AggregationDesigns element
ms.assetid: 7291956a-9c53-41fe-af2e-2418e26956c5
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: aa241d6a8ae6bb050ae17ccd9dbea5c825304aa2
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="aggregationdesigns-element-assl"></a>Elemento AggregationDesigns (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém a coleção de designs de agregação que pode ser compartilhada por várias partições em um banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MeasureGroup>  
   ...  
   <AggregationDesigns>  
      <AggregationDesign>...</AggregationDesign>  
   </AggregationDesigns>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum (coleção)|  
|Valor padrão|Nenhum (coleção)|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|  
|Elementos filho|[AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.AggregationDesignCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Partition &#40; ASSL &#41;](../../../analysis-services/scripting/objects/partition-element-assl.md)   
 [Coleções de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
