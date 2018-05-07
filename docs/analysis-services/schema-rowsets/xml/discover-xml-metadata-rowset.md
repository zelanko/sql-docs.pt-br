---
title: Conjunto de linhas DISCOVER_XML_METADATA | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a01f73cb3ef8647f179143e4be8b71f9dceee755
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="discoverxmlmetadata-rowset"></a>Conjunto de linhas DISCOVER_XML_METADATA
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Retorna um documento XML que descreve um objeto solicitado. O conjunto de linhas que sempre é retornado consiste em uma linha e em uma coluna.  
  
 Se você chamar o [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método com o **DISCOVER_XML_METATDATA** valor de enumeração no [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) elemento, o **Discover**método retorna o **DISCOVER_XML_METATDATA** conjunto de linhas.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DISCOVER_XML_METADATA** contém a coluna a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**METADATA**|**DBTYPE_WSTR**||Um documento de XML que descreve o objeto solicitada pela restrição.|  
  
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
  
 A restrição, **ObjectExpansion**, está disponível para cada objeto principal de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Normalmente, o cliente usa as restrições para descrever os objetos OLAP para os quais o DDL deve ser retornada e usa a restrição **ObjectExpansion** para definir o grau de expansão no DDL retornado. A tabela a seguir indica se o valor de enumeração é permitido para [Alter elemento &#40;XMLA&#41; ](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md) comandos.  
  
|Valor de enumeração|Description|  
|-----------------------|-----------------|  
|**ReferenceOnly**|Retorna somente o nome/ID/carimbo de data/hora/estado solicitado para os objetos pedidos e todos os principais objetos descendentes de forma recursiva.|  
|**ObjectProperties**|Expande o objeto solicitado sem referências para objetos contidos (inclui os objetos secundários contidos expandidos).|  
|**ExpandObject**|Igual a *ObjectProperties*, mas também retorna o nome, a ID e o carimbo de data/hora para os principais objetos contidos.|  
|**ExpandFull**|Expande completamente o objeto solicitado de forma recursiva até a parte inferior de todos os objetos contidos.|  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis conjuntos de linhas de esquema](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
