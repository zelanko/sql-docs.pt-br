---
title: Elemento Visible (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Visible Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Visible
helpviewer_keywords:
- Visible element
ms.assetid: 3e9baf1b-351f-4ebf-b57d-13d561f72d6f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a28fa446eb1753ce85458a19b849729f57c67a7a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48166656"
---
# <a name="visible-element-assl"></a>Elemento Visible (ASSL)
  Determina a visibilidade do elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CalculationProperty> <!-- or one of the elements listed below in the Element Relationships table -->  
  
   <Visible >...</Visible >  
  
</CalculationProperty>  
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
|Elementos pai|[CalculationProperty](../objects/calculationproperty-element-assl.md), [cubo](../objects/cube-element-assl.md), [CubeDimension](../data-type/dimension-data-type-assl.md), [CubeHierarchy](../data-type/hierarchy-data-type-assl.md), [banco de dados](../objects/database-element-assl.md), [medidas ](../objects/measure-element-assl.md), [MemberProperty](../objects/attributerelationship-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O elemento `Visible` determina se os componentes da interface de usuário devem exibir o elemento pai.  
  
 Os elementos que correspondem aos pais de `Visible` no modelo de objeto AMO (Objetos de Gerenciamento de Análise) são <xref:Microsoft.AnalysisServices.CalculationProperty>, <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.CubeDimension>, <xref:Microsoft.AnalysisServices.CubeHierarchy>, <xref:Microsoft.AnalysisServices.Database> e <xref:Microsoft.AnalysisServices.Measure>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
