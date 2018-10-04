---
title: Habilitado o elemento (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Enabled Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Enabled
helpviewer_keywords:
- Enabled element
ms.assetid: dbe57903-75c0-4060-a2b3-eab241d7469f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 116fe7904101d37ec39ea4f074467fd965ba1e77
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48061406"
---
# <a name="enabled-element-assl"></a>Elemento Enabled (ASSL)
  Indica se o elemento pai está habilitado.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CubeHierarchy> <!-- or ProactiveCaching -->  
   ...  
   <Enabled>...</Enabled>  
   ...  
</CubeHierarchy>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Booliano|  
|Valor padrão|True|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[CubeHierarchy](../data-type/hierarchy-data-type-assl.md), [ProactiveCaching](../objects/proactivecaching-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 Os elementos que correspondem aos pais de `Enabled` no modelo de objeto Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.CubeHierarchy> e <xref:Microsoft.AnalysisServices.ProactiveCaching>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
