---
title: Elemento NameColumn (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3c80014144d33ad6995936883af52adfb0ebf1a3
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="namecolumn-element-assl"></a>Elemento NameColumn (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Identifica a coluna que fornece o nome do elemento pai.  
  
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
|Valor padrão|Veja a tabela abaixo.|  
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
 Se a coleção [KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md) de **DimensionAttribute** contiver um único elemento [KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md) que representa uma coluna de chave com um tipo de dados de cadeia de caracteres, os mesmos valores de **DataItem** serão usados como valores padrão para o elemento **NameColumn** .  
  
 Para obter mais informações sobre o **DataItem** tipo, incluindo uma tabela de objetos do Analysis Services Scripting Language (ASSL) e propriedades do **DataItem** de tipo, consulte [tipo de dados de item de dados & #40; ASSL & #41; ](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
 Os elementos que correspondem aos pais de **NameColumn** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.DimensionAttribute> e <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
