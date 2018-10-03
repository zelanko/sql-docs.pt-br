---
title: Elemento RefreshPolicy (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- RefreshPolicy Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- RefreshPolicy
helpviewer_keywords:
- RefreshPolicy element
ms.assetid: f4c36280-1a39-4f1c-a3ab-fbeb81742d6d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6322c725a0c4b339425b9cc9e10aa6596c9fc34c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48144426"
---
# <a name="refreshpolicy-element-assl"></a>Elemento RefreshPolicy (ASSL)
  Determina a frequência com que a parte dinâmica do grupo de medidas ou dimensões (conforme especificado pela [persistência](persistence-element-assl.md) elemento) é verificada quanto a alterações.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionBinding> <!-- or MeasureGroupBinding -->  
   ...  
   <RefreshPolicy>...</RefreshPolicy>  
   ...  
</DimensionBinding>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
|Ancestral ou pai|Valor Padrão|  
|------------------------|-------------------|  
|[DimensionBinding](../data-type/binding-data-type-assl.md)|*ByQuery*|  
|[MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)|None|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[DimensionBinding](../data-type/binding-data-type-assl.md), [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*ByQuery*|Cada consulta verifica se os dados de origem foram alterados.|  
|*ByInterval*|Fonte de dados é verificada apenas para que as alterações no intervalo especificado por [RefreshInterval](refreshinterval-element-assl.md).|  
  
 A enumeração que corresponde aos valores permitidos para `RefreshPolicy` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.RefreshPolicy>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Persistence &#40;ASSL&#41;](persistence-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
