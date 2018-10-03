---
title: Elemento Members (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Members Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Members
helpviewer_keywords:
- Members element
ms.assetid: 4bf585a3-b681-486d-852b-1244c5658a04
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b7d2be7834c48c5a65877ae6fd480f2a7d6ea459
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48191056"
---
# <a name="members-element-assl"></a>Elemento Members (ASSL)
  Contém a coleção de elementos [Member](../objects/member-element-assl.md) do elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Group> <!-- or Role --<  
   ...  
   <Members>  
      <Member>...</Member>  
   </Members>  
   ...  
</Group>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|None|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Group](../objects/group-element-assl.md), [Role](../objects/role-element-assl.md)|  
|Elementos filho|[Membro](../objects/member-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 Os elementos que correspondem aos pais de `Members` no modelo de objeto Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.Group> e <xref:Microsoft.AnalysisServices.Role>.  
  
## <a name="see-also"></a>Consulte também  
 [Coleções &#40;ASSL&#41;](collections-assl.md)  
  
  
