---
title: Elemento ValueColumn (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ValueColumn Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: ValueColumn element
ms.assetid: 6c2d6822-8ecc-46df-9fa9-bb92ac716c36
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4413367639b3cc712e2b068ef0b34fce1f277431
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[O item de dados](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|Valor padrão|Varia (consulte Comentários)|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Se o [NameColumn](../../../analysis-services/scripting/objects/namecolumn-element-assl.md) elemento **DimensionAttribute** for especificado, o mesmo **DataItem** valores são usados como valores padrão para o **ValueColumn** elemento. Se o **NameColumn** elemento **DimensionAttribute** não for especificado e o [KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md) coleção de **DimensionAttribute** contém uma única [KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md) elemento que representa uma coluna de chave com um tipo de dados de cadeia de caracteres, o mesmo **DataItem** valores são usados como valores padrão para o **ValueColumn** elemento.  
  
 Para obter mais informações sobre o **DataItem** tipo, incluindo uma tabela de objetos do Analysis Services Scripting Language (ASSL) e propriedades do **DataItem** de tipo, consulte [tipo de dados de item de dados &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
 Os elementos que correspondem aos pais de **NameColumn** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.DimensionAttribute> e <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
