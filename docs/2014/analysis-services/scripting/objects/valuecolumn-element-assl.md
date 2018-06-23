---
title: Elemento ValueColumn (ASSL) | Microsoft Docs
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
- ValueColumn Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ValueColumn element
ms.assetid: 6c2d6822-8ecc-46df-9fa9-bb92ac716c36
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5cac1df12074e26cc375835a98231a79e101f0d9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122264"
---
# <a name="valuecolumn-element-assl"></a>Elemento ValueColumn (ASSL)
  Identifica a coluna que fornece o valor do elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <ValueColumn xsi:type="DataItem">...</ValueColumn>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[O item de dados](../data-type/dataitem-data-type-assl.md)|  
|Valor padrão|Varia (consulte Comentários)|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Se o [NameColumn](namecolumn-element-assl.md) elemento `DimensionAttribute` for especificado, o mesmo `DataItem` valores são usados como valores padrão para o `ValueColumn` elemento. Se o `NameColumn` elemento `DimensionAttribute` não for especificado e o [KeyColumns](../collections/keycolumns-element-assl.md) coleção de `DimensionAttribute` contém um único [KeyColumn](keycolumn-element-assl.md) elemento que representa uma coluna de chave com uma cadeia de caracteres tipo de dados, os mesmos `DataItem` valores são usados como valores padrão para o `ValueColumn` elemento.  
  
 Para obter mais informações sobre o `DataItem` tipo, incluindo uma tabela de objetos do Analysis Services Scripting Language (ASSL) e propriedades do `DataItem` de tipo, consulte [o tipo de dados DataItem &#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md).  
  
 Os elementos que correspondem aos pais de `NameColumn` no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.DimensionAttribute> e <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  