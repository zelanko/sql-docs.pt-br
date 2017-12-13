---
title: Elemento AttributeHierarchyDisplayFolder (ASSL) | Microsoft Docs
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
apiname: AttributeHierarchyDisplayFolder Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AttributeHierarchyDisplayFolder
helpviewer_keywords: AttributeHierarchyDisplayFolder element
ms.assetid: d4a3aff7-553e-416c-9c42-819a96ae264d
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2d294374564978b8d7a6b57a2df35914849d81e6
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="attributehierarchydisplayfolder-element-assl"></a>Elemento AttributeHierarchyDisplayFolder (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Identifica a pasta na qual exibir a hierarquia de atributo associados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttribute>  
      ...  
      <AttributeHierarchyDisplayFolder>...  
   </AttributeHierarchyDisplayFolder>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O elemento que corresponde ao pai do **AttributeHierarchyDisplayFolder** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
