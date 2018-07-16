---
title: Padrão de elemento (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Default Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DEFAULT
helpviewer_keywords:
- Default element
ms.assetid: 02c1844c-51fb-44fe-aafb-001e53ad293c
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f9003b574d2fd38e39eff0dc9e32ea3015d0fa99
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37304176"
---
# <a name="default-element-assl"></a>Elemento Default (ASSL)
  Determina se o [DrillThroughAction](../data-type/action-data-type-assl.md) é a ação de detalhamento padrão.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DrillThroughAction>  
   ...  
   <Default>...</Default  
   ...  
</ServerProperty>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Booliano|  
|Valor padrão|`False`|  
|Cardinalidade|0-1: elemento opcional que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[DrillThroughAction](../data-type/action-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O elemento que corresponde ao pai de `Default` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DrillThroughAction>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
