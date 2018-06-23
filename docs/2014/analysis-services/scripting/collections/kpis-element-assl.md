---
title: Elemento KPIs (ASSL) | Microsoft Docs
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
- Kpis Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Kpis
helpviewer_keywords:
- Kpis element
ms.assetid: da4e32a0-1416-4d32-8b7f-7d74be23c9d4
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 892e5997802b2d24d23ac9cb7e3be4ecb1b401c3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116265"
---
# <a name="kpis-element-assl"></a>Elemento Kpis (ASSL)
  Contém a coleção de indicadores chave de desempenho ([Kpi](../objects/kpi-element-assl.md) elementos) associado ao elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Cube><!-- or Perspective -->  
   ...  
   <Kpis>  
      <Kpi>...</Kpi> <!-- parent: Cube -->  
<!-- or -->  
      <Kpi xsi:type="PerspectiveKpi">...</Kpi> <!-- parent: Perspective -->  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Cubo](../objects/cube-element-assl.md), [perspectiva](../objects/perspective-element-assl.md)|  
  
|Ancestral ou pai|Elemento filho|  
|------------------------|-------------------|  
|[Cube](../objects/cube-element-assl.md)|[KPI](../objects/kpi-element-assl.md)|  
|[Perspectiva](../objects/perspective-element-assl.md)|[KPI](../objects/kpi-element-assl.md) do tipo [PerspectiveKpi](../data-type/perspectivekpi-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.KpiCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Coleções &#40;ASSL&#41;](collections-assl.md)  
  
  