---
title: Elemento MembersWithData (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MembersWithData Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MembersWithData
helpviewer_keywords:
- MembersWithData element
ms.assetid: 845087a2-b12d-4344-a8be-85ca61155296
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 17a3fced7327c1fb2211b1c80f774ae859757952
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48089637"
---
# <a name="memberswithdata-element-assl"></a>Elemento MembersWithData (ASSL)
  Determina se devem ou não exibir membros de dados para membros não folha no atributo pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <MembersWithData>...</MembersWithData>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*NonLeafDataVisible*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O valor da `MembersWithData` elemento é usado somente por atributos pai (em outras palavras, o valor da [uso](usage-element-dimensionattribute-assl.md) elemento do `DimensionAttribute` elemento pai é definido como *pai*) para determinar se Para exibir membros de dados para membros não folha no atributo pai. Para obter mais informações sobre membros de dados, consulte [Atributos em hierarquias pai-filho](../../multidimensional-models/parent-child-dimension-attributes.md).  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*NonLeafDataHidden*|Dados não folha estão ocultos.|  
|*NonLeafDataVisible*|Dados não folha estão visíveis.|  
  
 A enumeração que corresponde aos valores permitidos para `MembersWithData` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MembersWithData>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento MembersWithDataCaption &#40;ASSL&#41;](caption-element-assl.md)   
 [Tipo de dados DimensionAttribute &#40;ASSL&#41;](../data-type/dimensionattribute-data-type-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
