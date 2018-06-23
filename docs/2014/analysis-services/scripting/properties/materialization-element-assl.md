---
title: Elemento Materialization (ASSL) | Microsoft Docs
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
- Materialization Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Materialization element
ms.assetid: a87a95ae-d89c-4005-b22c-47c8991673b7
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 08e3607d1cb04f3a4483d43ead544edbbcf42a16
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118200"
---
# <a name="materialization-element-assl"></a>Elemento Materialization (ASSL)
  Indica o tipo de relação entre o grupo de medidas e a dimensão de referência.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ReferenceMeasureGroupDimension >  
   ...  
   <Materialization>...</Materialization>  
   ...  
</ReferenceMeasureGroupDimension>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Indireta*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[ReferenceMeasureGroupDimension](../data-type/dimension-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Regular*|A dimensão de referência tem uma relação regular, assim como com dimensões regulares.|  
|*Indireta*|A dimensão de referência tem uma relação indireta, assim como com dimensões muitos para muitos.|  
  
 O elemento que corresponde ao pai do `Materialization` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ReferenceMeasureGroupDimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de dimensão &#40;ASSL&#41;](../objects/dimension-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  