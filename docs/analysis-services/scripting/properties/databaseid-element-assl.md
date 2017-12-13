---
title: Elemento DatabaseID (ASSL) | Microsoft Docs
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
apiname: DatabaseID Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DatabaseID element
ms.assetid: 6bcf2bd5-b037-4964-bc72-42e0c89f9716
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fd42d1f7b2e6a545af23fc98174ec9c9a445e431
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="databaseid-element-assl"></a>Elemento DatabaseID (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Identifica o [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento associado a uma limite de linha [associação](../../../analysis-services/scripting/data-type/binding-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttributeBinding> <!-- or MeasureGroupAttributeBinding -->  
   ...  
   <DatabaseID>...</DatabaseID>  
   ...  
</DimensionAttributeBinding>  
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
|Elemento pai|[DimensionAttributeBinding](../../../analysis-services/scripting/data-type/dimensionattributebinding-data-type-out-of-line-assl.md), [MeasureGroupAttributeBinding](../../../analysis-services/scripting/data-type/measuregroupattributebinding-data-type-out-of-line-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre associações fora de linha, consulte [fontes de dados e associações &#40; SSAS Multidimensional &#41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
