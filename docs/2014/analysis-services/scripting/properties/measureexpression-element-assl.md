---
title: Elemento MeasureExpression (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MeasureExpression Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MeasureExpression
helpviewer_keywords:
- MeasureExpression element
ms.assetid: a0b6490d-a793-41be-8c97-41b08e1580a1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: edcf32c71f681bf6d8892b8848dfaa67ca8674b1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48113386"
---
# <a name="measureexpression-element-assl"></a>Elemento MeasureExpression (ASSL)
  Contém a linguagem MDX que define como são obtidos os valores de medida pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Measure>  
   ...  
   <MeasureExpression>...</MeasureExpression>  
   ...  
</Measure>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Medida](../objects/measure-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O elemento que corresponde ao pai de `MeasureExpression` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Measure>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
