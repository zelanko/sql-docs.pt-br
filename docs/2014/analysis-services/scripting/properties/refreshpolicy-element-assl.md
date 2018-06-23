---
title: Elemento RefreshPolicy (ASSL) | Microsoft Docs
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
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 6d2dc0549eb8151f93c817e9e59bc1a8990fac87
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36005713"
---
# <a name="refreshpolicy-element-assl"></a>Elemento RefreshPolicy (ASSL)
  Determina a frequência a parte dinâmica do grupo de medidas ou dimensões (conforme especificado pelo [persistência](persistence-element-assl.md) elemento) é verificada para alterações.  
  
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
|[MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)|Nenhum|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[DimensionBinding](../data-type/binding-data-type-assl.md), [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*ByQuery*|Cada consulta verifica se os dados de origem foram alterados.|  
|*ByInterval*|Fonte de dados é verificada apenas para as alterações no intervalo especificado por [RefreshInterval](refreshinterval-element-assl.md).|  
  
 A enumeração que corresponde aos valores permitidos para `RefreshPolicy` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.RefreshPolicy>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Persistence &#40;ASSL&#41;](persistence-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  