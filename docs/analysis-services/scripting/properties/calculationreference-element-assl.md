---
title: Elemento CalculationReference (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- CalculationReference Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- CalculationReference
helpviewer_keywords:
- CalculationReference element
ms.assetid: 4dd18b1f-55c3-4673-afbe-736d1bce8331
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 18df3c7f00efc4173b5651c2f2fb7528419278c3
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="calculationreference-element-assl"></a>Elemento CalculationReference (ASSL)
  Contém o nome do conjunto nomeado ou da célula calculada mencionado pelo [CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CalculationProperty>  
   ...  
   <CalculationReference>...</CalculationReference>  
   ...  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Se o valor da **CalculationReference** não corresponde o nome de um objeto existente nomeado definido ou calculada uma definição de célula, o **CalculationReference** será ignorado.  
  
 O elemento que corresponde ao pai do **CalculationReference** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.CalculationProperty>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento CalculationProperties & #40; ASSL & #41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)   
 [Elemento MdxScript & #40; ASSL & #41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)   
 [Elemento MdxScripts & #40; ASSL & #41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)   
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

