---
title: Tipo de dados PerspectiveKpi (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- PerspectiveKpi Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PerspectiveKpi
helpviewer_keywords:
- PerspectiveKpi data type
ms.assetid: e8d19ec8-70d3-4947-904a-fb81fcac9afd
caps.latest.revision: 31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ca2bc8d765e7ffe5a0111a22d8b2e5977a17f010
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37215916"
---
# <a name="perspectivekpi-data-type-assl"></a>Tipo de dados PerspectiveKpi (ASSL)
  Define um tipo de dados primitivo que representa informações sobre um indicador chave de desempenho (KPI) em um [perspectiva](../objects/perspective-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<PerspectiveKpi>  
   <KpiID>...</KpiID>  
   <Annotations>...</Annotations>  
</PerspectiveKpi>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhum|  
|Tipos de dados derivados|Nenhum|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|[Anotações](../collections/annotations-element-assl.md), [KpiID](../properties/id-element-assl.md)|  
|Elementos derivados|[KPI](../objects/kpi-element-assl.md) ([Kpis](../collections/kpis-element-assl.md) coleção de [perspectiva](../objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.PerspectiveKpi>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
