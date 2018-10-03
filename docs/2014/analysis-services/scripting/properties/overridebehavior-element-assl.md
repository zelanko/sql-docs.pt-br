---
title: Elemento OverrideBehavior (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- OverrideBehavior Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- OverrideBehavior element
ms.assetid: 6a5b361a-6061-4b73-b1a7-1237fb77606c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 88cf3dd287e1b55fee5377e2238d4d7c738cfe16
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48203616"
---
# <a name="overridebehavior-element-assl"></a>Elemento OverrideBehavior (ASSL)
  Indica o comportamento substituto da relação descrita por um [AttributeRelationship](../objects/attributerelationship-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AttributeRelationship>  
   ...  
   <OverrideBehavior>...</OverrideBehavior>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Forte*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[AttributeRelationship](../objects/attributerelationship-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O elemento `OverrideBehavior` determina como o posicionamento no atributo relacionado afeta o posicionamento no atributo.  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Forte*|Indica o comportamento substituto da relação descrita por um elemento AttributeRelationship. Dita como o posicionamento em um atributo afeta a posição do outro.|  
|*Nenhuma*|Nenhum efeito.|  
  
 A enumeração que corresponde aos valores permitidos para `OverrideBehavior` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.OverrideBehavior>.  
  
## <a name="see-also"></a>Consulte também  
 [Atributos e hierarquias de atributo](../../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
