---
title: Elemento ReportParameter (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ReportParameter Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ReportParameter
helpviewer_keywords:
- ReportParameter element
ms.assetid: 653a5c64-f1af-4796-bb7b-b44a40e52901
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fdc677b6aabd9d07275b977dd3d3af3145ea00a8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48093456"
---
# <a name="reportparameter-element-assl"></a>Elemento ReportParameter (ASSL)
  Contém o nome e o valor de um parâmetro que é passado para um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] relatório em tempo de execução.  
  
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|None|  
|Valor padrão|None|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[ReportParameters](../collections/reportparameters-element-assl.md)|  
|Elementos filho|[Nome](../properties/name-element-assl.md), [Value](../properties/value-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento `Value` deve conter uma linguagem MDX.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.ReportParameter>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados ReportAction &#40;ASSL&#41;](../data-type/action-data-type-assl.md)   
 [Elemento Action &#40;ASSL&#41;](action-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
