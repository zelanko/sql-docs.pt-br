---
title: Elemento ForeignKeyColumns (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
apiname: ForeignKeyColumns Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ForeignKeyColumns
helpviewer_keywords: ForeignKeyColumns element
ms.assetid: 0a673c1a-73dd-4217-aa41-56b340b5e1ab
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: cac758cbd601462d819331e04813372f2a1f042b
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="foreignkeycolumns-element-assl"></a>Elemento ForeignKeyColumns (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém a coleção de colunas que identificam a junção à tabela pai de uma fonte de dados relacional.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningStructureColumn xsi:type="TableMiningStructureColumn">  
   ...  
   <ForeignKeyColumns>  
      <ForeignKeyColumn xsi:type="DataItem">...</ForeignKeyColumn>  
...</ForeignKeyColumns>  
   ...  
</MiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md) do tipo [TableMiningStructureColumn](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)|  
|Elementos filho|[ForeignKeyColumn](../../../analysis-services/scripting/objects/foreignkeycolumn-element-assl.md) do tipo [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Elemento MiningStructure &#40; ASSL &#41;](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)   
 [Coleções de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
