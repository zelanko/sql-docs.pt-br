---
title: Elemento GranularityAttributeID (ASSL) | Microsoft Docs
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
apiname: GranularityAttributeID Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: GranularityAttributeID element
ms.assetid: 90e6c939-71bd-462a-a377-4854cb9d5266
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bac63fc3ccd2b9fc0ae1a1573497351ece870b9c
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="granularityattributeid-element-assl"></a>Elemento GranularityAttributeID (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém o identificador (ID) do atributo associado com o pai [MeasureGroupAttributeBinding](../../../analysis-services/scripting/data-type/measuregroupattributebinding-data-type-out-of-line-assl.md) tipo de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MeasureGroupAttributeBinding>  
   ...  
   <GranularityAttributeID>...</GranularityAttributeID>  
   ...  
</MeasureGroupAttributeBinding>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[MeasureGroupAttributeBinding](../../../analysis-services/scripting/data-type/measuregroupattributebinding-data-type-out-of-line-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre associações fora de linha, consulte [fontes de dados e associações &#40; SSAS Multidimensional &#41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
