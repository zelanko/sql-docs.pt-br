---
title: Elemento Member (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Member Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Member
helpviewer_keywords:
- Member element
ms.assetid: 03b4cfcb-ce87-452f-9e25-8745c0423f56
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c96454974357dbdd9510b1cf6f768b6e1c487a90
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126076"
---
# <a name="member-element-assl"></a>Elemento Member (ASSL)
  Contém o nome de um membro de um elemento [Group](group-element-assl.md) ou de um elemento [Role](role-element-assl.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Members>  
   <Member>  
      <Name>...</Name>  
   </Member>  
</Members>  
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
|Elementos pai|[Membros](../collections/members-element-assl.md)|  
|Elementos filho|[Nome](../properties/name-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 Os elementos que correspondem aos pais de `Member` no modelo de objeto Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.Group> e <xref:Microsoft.AnalysisServices.Role>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
