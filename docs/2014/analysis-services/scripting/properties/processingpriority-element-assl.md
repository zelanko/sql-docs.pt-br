---
title: Elemento ProcessingPriority (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ProcessingPriority Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ProcessingPriority element
ms.assetid: 95d07f1c-ef8d-4e38-9682-ebb7719dbe52
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 68a37c316cee72697cc24d23152b2b7035ea2386
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48121546"
---
# <a name="processingpriority-element-assl"></a>Elemento ProcessingPriority (ASSL)
  Determina a prioridade de processamento do objeto pai durante as operações em segundo plano, como agregações lentas, indexação ou cluster.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Dimension> <!-- or MeasureGroup, Partition -->  
   ...  
   <ProcessingPriority>...</ProcessingPriority>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Integer|  
|Valor padrão|`0`|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Dimensão](../data-type/dimension-data-type-assl.md), [MeasureGroup](../objects/group-element-assl.md), [partição](../objects/partition-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 Os elementos que correspondem aos pais de `ProcessingPriority` no modelo de objeto AMO (Objetos de Gerenciamento de Análise) são <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.MeasureGroup> e <xref:Microsoft.AnalysisServices.Partition>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
