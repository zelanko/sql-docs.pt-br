---
title: "Usado em traços de códigos de tipo de objeto de Analysis Services | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: trace-events
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: e4119db1-4a41-4335-9b33-f1ea95564300
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e6daef93ce07609173a3595adbb409c4b13607e2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="analysis-services-object-type-codes-used-in-traces"></a>Códigos de tipo de objeto de Analysis Services usados em traços
  Esta página exibe o tipo de objeto (um número com seis dígitos) de cada objeto em um modelo de dados do Analysis Services. Estes códigos aparecem em logs de rastreamento e são usados para identificar o tipo de objeto associado a um bloqueio específico. Por exemplo, um tempo limite de bloqueio em um banco de dados indicará o tipo de objeto 100002, que é o tipo de objeto de banco de dados.  
  
> [!NOTE]  
>  Há mais códigos listados abaixo do que realmente aparecerá em um log de rastreamento. A lista abaixo é uma lista abrangente dos códigos de tipo para cada objeto, mas apenas objetos que fazem um bloqueio apresentará um código de tipo de objeto em um log de rastreamento.  
  
## <a name="object-type-reference"></a>Referência ao tipo de objeto  
  
|Tipo de objeto|Nome do objeto|  
|-----------------|-----------------|  
|100000|Servidor|  
|100001|Comando|  
|100002|Banco de dados|  
|100003|DataSource|  
|100004|DataPermission|  
|100005|Função|  
|100006|Dimensão|  
|100007|DimensionAttribute|  
|100008|Hierarquia|  
|100009|Nível|  
|100010|Cube|  
|100011|CubePermission|  
|100012|CubeDimension|  
|100013|CubeAttribute|  
|100014|CubeHierarchy|  
|100016|MeasureGroup|  
|100017|MeasureGroupDimension|  
|100018|MeasureGroupAttribute|  
|100020|Measure|  
|100021|Partition|  
|100025|AggregationDesign|  
|100026|AggregationDesignDimension|  
|100027|AggregationDesignAttribute|  
|100028|Agregação|  
|100029|AggregationDimension|  
|100030|AggregationAttribute|  
|100032|MiningStructure|  
|100033|MiningStructureColumn|  
|100037|MiningModel|  
|100038|MiningModelColumn|  
|100039|AlgorithmParameter|  
|100041|MiningModelPermission|  
|100042|DimensionPermission|  
|100043|MiningStructurePermission|  
|100044|Assembly|  
|100045|DatabaseRole|  
|100046|AttributePermission|  
|100047|CubeAttributePermission|  
|100048|CellPermission|  
|100049|CubeDimensionPermission|  
|100050|Rastreamento|  
|100051|ServerAssembly|  
|100052|CubeAssembly|  
|100053|Comando|  
|100054|KPI|  
|100055|DataSourceView|  
|100056|Perspective|  
|100100|CommandCollection|  
|100101|DatabaseCollection|  
|100102|DataSourceCollection|  
|100103|DataPermission|  
|100104|RoleCollection|  
|100105|DimensionCollection|  
|100106|DimensionAttributeCollection|  
|100107|HierarchyCollection|  
|100108|LevelCollection|  
|100109|CubeCollection|  
|100110|CubePermissionCollection|  
|100111|CubeDimensionCollection|  
|100112|CubeAttributeCollection|  
|100113|CubeHierarchyCollection|  
|100115|MeasureGroupCollection|  
|100116|MeasureGroupDimensionCollection|  
|100117|MeasureGroupAttributeCollection|  
|100119|MeasureCollection|  
|100120|PartitionCollection|  
|100124|AggregationDesignCollection|  
|100125|AggregationDesignDimensionCollection|  
|100126|AggregationDesignAttributeCollection|  
|100127|AggregationCollection|  
|100128|AggregationDimensionCollection|  
|100129|AggregationAttributeCollection|  
|100131|MiningStructureCollection|  
|100132|MiningStructureColumnCollection|  
|100136|MiningModelCollection|  
|100137|MiningModelColumnCollection|  
|100138|AlgorithmParameterCollection|  
|100140|MiningModelPermissionCollection|  
|100141|DimensionPermissionCollection|  
|100142|MiningStructurePermissionCollection|  
|100143|AssemblyCollection|  
|100144|DatabaseRoleCollecction|  
|100145|AttributePermissionCollection|  
|100146|CubeAttributePermissionCollection|  
|100147|CellPermissionCollection|  
|100148|CubeDimensionPermissionCollection|  
|100149|TraceCollection|  
|100150|ServerAssemblyCollection|  
|100151|CubeAssemblyCollection|  
|100152|CommandCollection|  
|100153|KpiCollection|  
|100154|DataSourceViewCollection|  
|100155|PerspectiveCollection|  
  
  
