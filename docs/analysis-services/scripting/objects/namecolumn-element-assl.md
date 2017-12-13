---
title: Elemento NameColumn (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: NameColumn Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: NameColumn
helpviewer_keywords: NameColumn element
ms.assetid: 9ff79f2e-26d7-4ab9-a166-14c2c2d1fc07
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3187047bdb1dab69e4c0abc0273a9eaec220ced4
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="namecolumn-element-assl"></a>Elemento NameColumn (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Identifica a coluna que fornece o nome do elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttribute> <!-- or ScalarMiningStructureColumn -->  
   ...  
   <NameColumn xsi:type="DataItem">...</NameColumn>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[O item de dados](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|Valor padrão|Consulte a tabela a seguir.|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
|Ancestral ou pai|Valor padrão|  
|------------------------|-------------------|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|Varia (consulte Comentários)|  
|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|Nenhuma|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Se o [KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md) coleção de **DimensionAttribute** contém um único [KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md) elemento que representa uma coluna de chave com um tipo de dados de cadeia de caracteres, os mesmos **DataItem** valores são usados como valores padrão para o **NameColumn** elemento.  
  
 Para obter mais informações sobre o **DataItem** tipo, incluindo uma tabela de objetos do Analysis Services Scripting Language (ASSL) e propriedades do **DataItem** de tipo, consulte [tipo de dados de item de dados &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
 Os elementos que correspondem aos pais de **NameColumn** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.DimensionAttribute> e <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
