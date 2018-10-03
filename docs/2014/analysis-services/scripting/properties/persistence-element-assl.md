---
title: Elemento Persistence (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Persistence Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Persistence
helpviewer_keywords:
- Persistence element
ms.assetid: dafe3df2-4795-48ea-bebe-33c1a3bf18b6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c5e5ce2407b13d343d0490807dac5bdec0aede15
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48186416"
---
# <a name="persistence-element-assl"></a>Elemento Persistence (ASSL)
  Determina quais partes dos dados de origem ligados são dinâmicos e são verificados quanto à atualizações usando a frequência especificada pelo [RefreshPolicy](refreshpolicy-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionBinding> <!-- or MeasureGroupBinding -->  
   ...  
   <Persistence>...</Persistence>  
   ...  
</DimensionBinding>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*NotPersisted*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[DimensionBinding](../data-type/binding-data-type-assl.md), [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*NotPersisted*|Os metadados de origem, os membros e os dados são todos dinâmicos.|  
|*Metadados*|O metadados de origem é estático, mas os membros e os dados são dinâmicos.|  
|*Todos*|O metadados de origem, os membros e os dados são todos estáticos.|  
  
 A enumeração que corresponde aos valores permitidos para `Persistence` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.PersistenceType>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
