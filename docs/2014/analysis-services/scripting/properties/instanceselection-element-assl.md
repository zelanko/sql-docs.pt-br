---
title: Elemento InstanceSelection (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- InstanceSelection Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- InstanceSelection element
ms.assetid: 908a2da9-274c-40d2-87dc-4641cb8d77e6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 41587ee5acd29ca8038e188a3a3a5681bb7b91d0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48131456"
---
# <a name="instanceselection-element-assl"></a>Elemento InstanceSelection (ASSL)
  Fornece uma dica para aplicativos cliente para sugerir como uma lista de itens deve ser exibida, com base no número esperado de itens na lista.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <InstanceSelection>...</InstanceSelection>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Nenhuma*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres a seguir:  
  
|Valor|Description|  
|-----------|-----------------|  
|*Nenhuma*|Não exiba uma lista de seleções. Permita os usuários insiram valores diretamente.|  
|*Lista suspensa*|O número de itens é muito pequeno para ser exibido em uma lista suspensa.|  
|*Listaa*|O número de itens é muito grande para uma lista suspensa, mas não requer filtragem.|  
|*FilteredList*|O número de itens é grande o suficiente para exigir que os usuários filtrem os itens a serem exibidos.|  
|*MandatoryFilter*|O número de itens é tão grande que a exibição deve sempre ser filtrada.|  
  
 A enumeração que corresponde aos valores permitidos para `InstanceSelection` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.InstanceSelection>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
