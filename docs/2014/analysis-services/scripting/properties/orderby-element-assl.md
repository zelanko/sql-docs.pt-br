---
title: Elemento OrderBy (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- OrderBy Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- OrderBy
helpviewer_keywords:
- OrderBy element
ms.assetid: d7a0564b-430e-44eb-913a-fe1f98917d0f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 95ed1ce8e5b9df8340b41b8ec24e713dae9739ab
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48168726"
---
# <a name="orderby-element-assl"></a>Elemento OrderBy (ASSL)
  Descreve como ordenar os membros contidos no atributo.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttribute>  
   ...  
      <OrderBy>...</OrderBy>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Nome*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Nome*|Ordene pelo nome de membro.|  
|*Chave*|Ordene pela chave de membro.|  
|*AttributeKey*|Ordene pela chave de membro do atributo especificado na [OrderByAttributeID](id-element-assl.md) elemento de `DimensionAttribute`.|  
|*AttributeName*|Ordene pelo nome de membro do atributo especificado no elemento `OrderByAttributeID` de `DimensionAttribute`.|  
  
 A enumeração que corresponde aos valores permitidos para `OrderBy` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.OrderBy>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
