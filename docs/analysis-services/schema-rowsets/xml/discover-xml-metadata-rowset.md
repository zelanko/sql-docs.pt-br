---
title: Conjunto de linhas DISCOVER_XML_METADATA | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DISCOVER_XML_METADATA
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_XML_METADATA rowset
ms.assetid: 0befd026-db1b-43ac-b0e6-734abb56a4b1
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d0f2a0a63ff4d08a3a273f303a956b49f4932a21
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="discoverxmlmetadata-rowset"></a>Conjunto de linhas DISCOVER_XML_METADATA
  Retorna um documento XML que descreve um objeto solicitado. O conjunto de linhas que sempre é retornado consiste em uma linha e em uma coluna.  
  
 Se você chamar o [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método com o **DISCOVER_XML_METATDATA** valor de enumeração no [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) elemento, o **Discover**método retorna o **DISCOVER_XML_METATDATA** conjunto de linhas.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DISCOVER_XML_METADATA** contém a coluna a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**METADADOS**|**DBTYPE_WSTR**||Um documento de XML que descreve o objeto solicitada pela restrição.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
> [!IMPORTANT]  
>  O conjunto de linhas **DISCOVER_XML_METADATA** não pode ser consultado por meio da sintaxe do comando SELECT. No entanto, o **DISCOVER_XML_METADATA** conjunto de linhas pode ser consultado usando <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas **DISCOVER_XML_METADATA** pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**DatabaseID**|**DBTYPE_WSTR**|Opcional.|  
|**DimensionID**|**DBTYPE_WSTR**|Opcional.|  
|**CubeID**|**DBTYPE_WSTR**|Opcional.|  
|**MeasureGroupID**|**DBTYPE_WSTR**|Opcional.|  
|**PartitionID**|**DBTYPE_WSTR**|Opcional.|  
|**PerspectiveID**|**DBTYPE_WSTR**|Opcional.|  
|**DimensionPermissionID**|**DBTYPE_WSTR**|Opcional.|  
|**RoleID**|**DBTYPE_WSTR**|Opcional.|  
|**DatabasePermissionID**|**DBTYPE_WSTR**|Opcional.|  
|**MiningModelID**|**DBTYPE_WSTR**|Opcional.|  
|**MiningModelPermissionID**|**DBTYPE_WSTR**|Opcional.|  
|**DataSourceID**|**DBTYPE_WSTR**|Opcional.|  
|**MiningStructureID**|**DBTYPE_WSTR**|Opcional.|  
|**AggregationDesignID**|**DBTYPE_WSTR**|Opcional.|  
|**TraceID**|**DBTYPE_WSTR**|Opcional.|  
|**MiningStructurePermissionID**|**DBTYPE_WSTR**|Opcional.|  
|**CubePermissionID**|**DBTYPE_WSTR**|Opcional.|  
|**ID de assembly**|**DBTYPE_WSTR**|Opcional.|  
|**MdxScriptID**|**DBTYPE_WSTR**|Opcional.|  
|**DataSourceViewID**|**DBTYPE_WSTR**|Opcional.|  
|**DataSourcePermissionID**|**DBTYPE_WSTR**|Opcional.|  
|**ObjectExpansion**|**DBTYPE_WSTR**|Opcional.|  
  
 A restrição, **ObjectExpansion**, está disponível para cada objeto principal de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Normalmente, o cliente usa as restrições para descrever os objetos OLAP para os quais o DDL deve ser retornada e usa a restrição **ObjectExpansion** para definir o grau de expansão no DDL retornado. A tabela a seguir indica se o valor de enumeração é permitido para [elemento Alter &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md) comandos.  
  
|Valor de enumeração|Description|  
|-----------------------|-----------------|  
|**ReferenceOnly**|Retorna somente o nome/ID/carimbo de data/hora/estado solicitado para os objetos pedidos e todos os principais objetos descendentes de forma recursiva.|  
|**ObjectProperties**|Expande o objeto solicitado sem referências para objetos contidos (inclui os objetos secundários contidos expandidos).|  
|**ExpandObject**|Igual a *ObjectProperties*, mas também retorna o nome, a ID e o carimbo de data/hora para os principais objetos contidos.|  
|**ExpandFull**|Expande completamente o objeto solicitado de forma recursiva até a parte inferior de todos os objetos contidos.|  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis conjuntos de linhas de esquema](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

