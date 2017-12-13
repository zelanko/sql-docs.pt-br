---
title: Elemento KPIs (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
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
apiname: Kpis Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Kpis
helpviewer_keywords: Kpis element
ms.assetid: da4e32a0-1416-4d32-8b7f-7d74be23c9d4
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: be0fde074002913e807c961dbb9c39d85ec4f78b
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="kpis-element-assl"></a>Elemento Kpis (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém a coleção de indicadores chave de desempenho ([Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md) elementos) associado ao elemento pai.  
  
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Cubo](../../../analysis-services/scripting/objects/cube-element-assl.md), [perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md)|  
|Elementos filho|Consulte a tabela a seguir.|  
  
|Ancestral ou pai|Elemento filho|  
|------------------------|-------------------|  
|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|[KPI](../../../analysis-services/scripting/objects/kpi-element-assl.md)|  
|[Perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md)|[KPI](../../../analysis-services/scripting/objects/kpi-element-assl.md) do tipo [PerspectiveKpi](../../../analysis-services/scripting/data-type/perspectivekpi-data-type-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.KpiCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Coleções de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
