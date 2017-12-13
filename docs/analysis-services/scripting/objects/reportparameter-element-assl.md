---
title: Elemento ReportParameter (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
apiname: ReportParameter Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ReportParameter
helpviewer_keywords: ReportParameter element
ms.assetid: 653a5c64-f1af-4796-bb7b-b44a40e52901
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b270fa9fb739c6afdb7edb14aaa8b7dab998a815
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="reportparameter-element---assl"></a>Elemento ReportParameter - ASSL
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém o nome e o valor de um parâmetro que é passado para um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] relatório em tempo de execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ReportParameters>  
      <ReportParameter>  
      <Name>...</Name>  
      <Value>...</Value>  
   </ReportParameter>  
</ReportParameters>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[ReportParameters](../../../analysis-services/scripting/collections/reportparameters-element-assl.md)|  
|Elementos filho|[Nome](../../../analysis-services/scripting/properties/name-element-assl.md), [Value](../../../analysis-services/scripting/properties/value-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento **Value** deve conter uma linguagem MDX.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.ReportParameter>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados ReportAction &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)   
 [Elemento de ação &#40; ASSL &#41;](../../../analysis-services/scripting/objects/action-element-assl.md)   
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
