---
title: Tipo de dados StandardAction (ASSL) | Microsoft Docs
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
- StandardAction Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- StandardAction
helpviewer_keywords:
- StandardAction data type
ms.assetid: 81b574d5-06c1-4587-8bd2-0e5c5e3b1d99
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: bdf3282c6f75cc762ae67a9fab9fc641f25fa3a4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009634"
---
# <a name="standardaction-data-type-assl"></a>Tipo de dados StandardAction (ASSL)
  Define um tipo de dados derivado que representa qualquer [ação](../objects/action-element-assl.md) elemento diferente de um [DrillThroughAction](action-data-type-assl.md) elemento ou um [ReportAction](reportaction-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<StandardAction>  
   <!-- The following elements extend Action -->  
   <Expression>...</Expression>  
</StandardAction>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|[Ação](action-data-type-assl.md)|  
|Tipos de dados derivados|Nenhum|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|[Expression](../properties/expression-element-assl.md)|  
|Elementos derivados|[Ação](../objects/action-element-assl.md) ([ações](../collections/actions-element-assl.md) coleção de [cubo](../objects/cube-element-assl.md) ou [perspectiva](../objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.StandardAction>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  