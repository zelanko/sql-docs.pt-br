---
title: Elemento KpiID (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- KpiID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- KpiID
helpviewer_keywords:
- KpiID element
ms.assetid: a76395bc-bc84-40f8-9770-6275842f93b5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f89e393249215ebf700cfde543f8b645a268536b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48090496"
---
# <a name="kpiid-element-assl"></a>Elemento KpiID (ASSL)
  Contém um identificador (ID) que associa um [Kpi](../objects/kpi-element-assl.md) elemento com um [perspectiva](../objects/perspective-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<PerspectiveKpi>  
      ...  
   <KpiID>...</KpiID>  
   ...  
</PerspectiveKpi>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|None|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[PerspectiveKpi](../data-type/perspectivekpi-data-type-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O elemento que corresponde ao pai de `KpiID` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.PerspectiveKpi>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades (ASSL)](properties-assl.md)  
  
  
