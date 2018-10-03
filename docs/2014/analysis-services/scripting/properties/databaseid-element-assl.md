---
title: Elemento DatabaseID (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DatabaseID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- DatabaseID element
ms.assetid: 6bcf2bd5-b037-4964-bc72-42e0c89f9716
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 13d1969af83e4fa4bfba07eead0f822c5a81ad43
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48066926"
---
# <a name="databaseid-element-assl"></a>Elemento DatabaseID (ASSL)
  Identifica o [banco de dados](../objects/database-element-assl.md) elemento associado a uma limite de linha [associação](../data-type/binding-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttributeBinding> <!-- or MeasureGroupAttributeBinding -->  
   ...  
   <DatabaseID>...</DatabaseID>  
   ...  
</DimensionAttributeBinding>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|None|  
|Cardinalidade|1-1: elemento obrigatório que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[DimensionAttributeBinding](../data-type/dimensionattributebinding-data-type-out-of-line-assl.md), [MeasureGroupAttributeBinding](../data-type/measuregroupattributebinding-data-type-out-of-line-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre associações fora de linha, consulte [fontes de dados e associações &#40;Multidimensional do SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
