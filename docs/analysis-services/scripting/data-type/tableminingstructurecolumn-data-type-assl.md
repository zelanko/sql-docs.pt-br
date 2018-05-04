---
title: Tipo de dados TableMiningStructureColumn (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- TableMiningStructureColumn Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TableMiningStructureColumn
helpviewer_keywords:
- TableMiningStructureColumn data type
ms.assetid: 350358b0-f2fc-43c3-957d-884c59fa879e
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 8502f99229bf19bcf83f1889a18f198394c40f2d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="tableminingstructurecolumn-data-type-assl"></a>Tipo de dados TableMiningStructureColumn (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define um tipo de dados derivado que representa um elemento [MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md) que contém tabelas aninhadas, em oposição aos valores escalares associados ao elemento [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md) que contém valores escalares.  
  
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|[MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)|  
|Tipos de dados derivados|Nenhuma|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|[Columns](../../../analysis-services/scripting/collections/columns-element-assl.md), [ForeignKeyColumn](../../../analysis-services/scripting/objects/foreignkeycolumn-element-assl.md), [SourceMeasureGroup](../../../analysis-services/scripting/objects/sourcemeasuregroup-element-assl.md), [Translations](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
|Elementos derivados|[Column](../../../analysis-services/scripting/objects/column-element-assl.md) (coleção[Columns](../../../analysis-services/scripting/collections/columns-element-assl.md) de [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
