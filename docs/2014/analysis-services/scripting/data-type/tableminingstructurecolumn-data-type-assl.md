---
title: Tipo de dados TableMiningStructureColumn (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- TableMiningStructureColumn Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TableMiningStructureColumn
helpviewer_keywords:
- TableMiningStructureColumn data type
ms.assetid: 350358b0-f2fc-43c3-957d-884c59fa879e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e5195118322ff7de4b618dbbe11743639101c625
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48082766"
---
# <a name="tableminingstructurecolumn-data-type-assl"></a>Tipo de dados TableMiningStructureColumn (ASSL)
  Define um tipo de dados derivado que representa uma [MiningStructureColumn](miningstructurecolumn-data-type-assl.md) elemento que contém tabelas aninhadas, em vez de valores escalares associados com o [ScalarMiningStructureColumn](scalarminingstructurecolumn-data-type-assl.md) elemento que contém valores escalares.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<TableMiningStructureColumn>  
   <!-- The following elements extend MiningStructureColumn -->  
   <ForeignKeyColumn>..</ForeignKeyColumn>  
   <SourceMeasureGroup>..</SourceMeasureGroup>  
   <Columns>..</Columns>  
   <Translations>..</Translations>  
</TableMiningStructureColumn>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|[MiningStructureColumn](miningstructurecolumn-data-type-assl.md)|  
|Tipos de dados derivados|None|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|None|  
|Elementos filho|[Colunas](../collections/columns-element-assl.md), [ForeignKeyColumn](../objects/column-element-assl.md), [SourceMeasureGroup](../objects/group-element-assl.md), [traduções](../collections/translations-element-assl.md)|  
|Elementos derivados|[Coluna](../objects/column-element-assl.md) ([colunas](../collections/columns-element-assl.md) coleção de [MiningStructure](../objects/miningstructure-element-assl.md))|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
