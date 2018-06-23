---
title: Tipo de dados PerspectiveCalculation (ASSL) | Microsoft Docs
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
- PerspectiveCalculation Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PerspectiveCalculation
helpviewer_keywords:
- PerspectiveCalculation data type
ms.assetid: 5a5173d2-c96d-4a55-a35c-0cbfd5b0e599
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 1214bc349c09f02f522569b26dd48e82d5e42b99
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130857"
---
# <a name="perspectivecalculation-data-type-assl"></a>Tipo de dados PerspectiveCalculation (ASSL)
  Define um tipo de dados primitivo que representa a relação entre um cálculo e um [perspectiva](../objects/perspective-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<PerspectiveCalculation>  
      <Name>...</Name>  
   <Type>...</Type>  
   <Annotations>...</Annotations>  
</PerspectiveCalculation>  
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
|Elementos filho|[Anotações](../collections/annotations-element-assl.md), [nome](../properties/name-element-assl.md), [tipo](../properties/type-element-perspectivecalculation-assl.md)|  
|Elementos derivados|[Cálculo](../objects/calculation-element-assl.md) ([cálculos](../collections/calculations-element-assl.md) coleção de [perspectiva](../objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.PerspectiveCalculation>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  