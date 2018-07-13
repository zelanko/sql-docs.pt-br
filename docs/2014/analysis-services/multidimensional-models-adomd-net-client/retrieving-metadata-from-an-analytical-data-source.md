---
title: Recuperando metadados de uma fonte de dados analíticos | Microsoft Docs
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
helpviewer_keywords:
- metadata [ADOMD.NET]
- retrieving metadata
ms.assetid: 00043ebd-7164-4ceb-b945-6e44378ea00a
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2beb806c4a76aa3ac6062f8e6ae0e44c007520ae
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37151667"
---
# <a name="retrieving-metadata-from-an-analytical-data-source"></a>Retrieving Metadata from an Analytical Data Source
  Os metadados são importantes para aplicativos que recuperam dados analíticos e que trabalham com eles. Na recuperação de dados de uma fonte relacional, a dimensionalidade de tais dados será previsível, até mesmo com conjuntos de dados aninhados. Os conjuntos de resultados de um banco de dados relacional são tipicamente bidimensionais ou escalares em estrutura. No entanto, os dados recuperados de fontes de dados analíticos podem ser de dimensionalidade variável, organizados em hierarquias potencialmente profundas.  
  
 Para manipular a complexidade de recuperação de metadados de fontes de dados analíticos, ADOMD.NET oferece dois formulários de recuperação de metadados:  
  
 **O modelo de objeto**  
 O modelo de objeto do ADOMD.NET é geralmente mais fácil usar do que os conjuntos de linhas do esquema. Para a maioria dos cenários, você pode acessar os metadados de vários objetos de banco de dados simplesmente usando o modelo de objeto. O ADOMD.NET exibe o modelo de objeto por meio de <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>.  
  
 Para obter mais informações: [trabalhando com o modelo de objeto do ADOMD.NET](retrieving-metadata-working-with-adomd-net-object-model.md)  
  
 **Conjuntos de linhas de esquema**  
 Uma abordagem completa, embora mais difícil, de recuperar metadados é usar conjuntos de linhas do esquema. Um conjunto de linhas de esquema é um conjunto de linhas OLE DB que encapsula a descrição de todos os objetos de um tipo específico no banco de dados. As informações de esquema de uma fonte de dados analíticos incluem bancos de dados ou catálogos disponíveis na fonte de dados, nos cubos e nos modelos de mineração de um banco de dados, funções existentes para cubos da fonte de dados e assim por diante. Esses metadados podem ser recuperados por meio do método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>, passando um `GUID` ou um nome XMLA (XML for Analysis).  
  
 Para obter mais informações: [Working with Schema Rowsets in ADOMD.NET](retrieving-metadata-working-with-schema-rowsets.md))  
  
 Cada um desses métodos de recuperação de metadados acessa tipos diferentes de metadados. A tabela a seguir descreve os diferentes metadados disponíveis para cada método e os métodos usados para acessá-los.  
  
|GUID (usado em conjuntos de linhas do esquema)|Nome XMLA (usado em conjuntos de linhas do esquema)|Modelo de objeto do ADOMD.NET|  
|-------------------------------------|------------------------------------------|----------------------------|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Actions>|[Conjunto de linhas MDSCHEMA_ACTIONS](../schema-rowsets/ole-db-olap/mdschema-actions-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Catalogs>|[Conjunto de linhas DBSCHEMA_CATALOGS](../schema-rowsets/ole-db/dbschema-catalogs-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Columns>|[Conjunto de linhas DBSCHEMA_COLUMNS](../schema-rowsets/ole-db/dbschema-columns-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Connections>|`DISCOVER_CONNECTIONS`||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Cubes>|[Conjunto de linhas MDSCHEMA_CUBES](../schema-rowsets/ole-db-olap/mdschema-cubes-rowset.md)|AdomdConnection.Cubes|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.DataSources>|[Conjunto de linhas DISCOVER_DATASOURCES](../schema-rowsets/xml/discover-datasources-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.DBConnections>|`DISCOVER_DB_CONNECTIONS`||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Dimensions>|[Conjunto de linhas MDSCHEMA_DIMENSIONS](../schema-rowsets/ole-db-olap/mdschema-dimensions-rowset.md)|AdomdConnection.Cubes[].Dimensions|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.DimensionStat>|`DISCOVER_DIMENSION_STAT`||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Enumerators>|[Conjunto de linhas DISCOVER_ENUMERATORS](../schema-rowsets/xml/discover-enumerators-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Functions>|[Conjunto de linhas MDSCHEMA_FUNCTIONS](../schema-rowsets/ole-db-olap/mdschema-functions-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Hierarchies>|[Conjunto de linhas MDSCHEMA_HIERARCHIES](../schema-rowsets/ole-db-olap/mdschema-hierarchies-rowset.md)|AdomdConnection.Cubes[].Dimensions[].Hierarchies|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.InputDataSources>|[Conjunto de linhas MDSCHEMA_INPUT_DATASOURCES](../schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Instances>|[Conjunto de linhas DISCOVER_INSTANCES](../schema-rowsets/ole-db-olap/discover-instances-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Jobs>|`DISCOVER_JOBS`||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Keywords>|[Conjunto de linhas DISCOVER_KEYWORDS &#40;OLE DB para OLAP&#41;](../schema-rowsets/ole-db-olap/discover-keywords-rowset-ole-db-for-olap.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Kpis>|[Conjunto de linhas MDSCHEMA_KPIS](../schema-rowsets/ole-db-olap/mdschema-kpis-rowset.md)|AdomdConnection.Cubes[].KPIs|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Levels>|[Conjunto de linhas MDSCHEMA_LEVELS](../schema-rowsets/ole-db-olap/mdschema-levels-rowset.md)|AdomdConnection.Cubes[].Dimensions[].Hierarchies[].Levels|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Literals>|[Conjunto de linhas DISCOVER_LITERALS](../schema-rowsets/xml/discover-literals-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Locations>|`DISCOVER_LOCATIONS`||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Locks>|`DISCOVER_LOCKS`||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MasterKey>|`DISCOVER_MASTER_KEY`||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MeasureGroupDimensions>|[Conjunto de linhas MDSCHEMA_MEASUREGROUP_DIMENSIONS](../schema-rowsets/ole-db-olap/mdschema-measuregroup-dimensions-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MeasureGroups>|[Conjunto de linhas MDSCHEMA_MEASURESGROUPS](../schema-rowsets/ole-db-olap/mdschema-measuregroups-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Measures>|[Conjunto de linhas MDSCHEMA_MEASURES](../schema-rowsets/ole-db-olap/mdschema-measures-rowset.md)|AdomdConnection.Cubes[].Measures|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MemberProperties>|[Conjunto de linhas MDSCHEMA_PROPERTIES](../schema-rowsets/ole-db-olap/mdschema-properties-rowset.md)|PropertyCollection disponível na maioria dos objetos ADOMD.NET.|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Members>|[Conjunto de linhas MDSCHEMA_MEMBERS](../schema-rowsets/ole-db-olap/mdschema-members-rowset.md)|AdomdConnection.Cubes[].Dimensions[].Hierarchies[].Levels[].GetMembers()|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MemoryGrant>|`DISCOVER_MEMORYGRANT`||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MemoryUsage>|`DISCOVER_MEMORYUSAGE`||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MiningColumns>|[Conjunto de linhas DMSCHEMA_MINING_COLUMNS](../schema-rowsets/data-mining/dmschema-mining-columns-rowset.md)|AdomdConnection.MiningModels[].MiningModelColumns|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MiningFunctions>|[Conjunto de linhas DMSCHEMA_MINING_FUNCTIONS](../schema-rowsets/data-mining/dmschema-mining-functions-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MiningModelContent>|[Conjunto de linhas DMSCHEMA_MINING_MODEL_CONTENT](../schema-rowsets/data-mining/dmschema-mining-model-content-rowset.md)|AdomdConnection.MiningModels[].MiningContentNodes|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MiningModelContentPmml>|[Conjunto de linhas DMSCHEMA_MINING_MODEL_CONTENT_PMML](../schema-rowsets/data-mining/dmschema-mining-model-content-pmml-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MiningModels>|[Conjunto de linhas DMSCHEMA_MINING_MODELS](../schema-rowsets/data-mining/dmschema-mining-models-rowset.md)|AdomdConnection.MiningModels|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MiningModelXml>|[Conjunto de linhas DMSCHEMA_MINING_MODEL_XML](../schema-rowsets/data-mining/dmschema-mining-model-xml-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MiningServiceParameters>|[Conjunto de linhas DMSCHEMA_MINING_SERVICE_PARAMETERS](../schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset.md)|AdomdConnection.MiningServices[].MiningServiceParameters|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MiningServices>|[Conjunto de linhas DMSCHEMA_MINING_SERVICES](../schema-rowsets/data-mining/dmschema-mining-services-rowset.md)|AdomdConnection.MiningServices|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MiningStructureColumns>|[Conjunto de linhas DMSCHEMA_MINING_STRUCTURE_COLUMNS](../schema-rowsets/data-mining/dmschema-mining-structure-columns-rowset.md)|AdomdConnection.MiningStructures[].MiningStructureColumns|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MiningStructures>|[Conjunto de linhas DMSCHEMA_MINING_STRUCTURES](../schema-rowsets/data-mining/dmschema-mining-structures-rowset.md)|AdomdConnection.MiningStructures|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.PartitionDimensionStat>|`DISCOVER_PARTITION_DIMENSION_STAT`||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.PartitionStat>|`DISCOVER_PARTITION_STAT`||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.PerformanceCounters>|`DISCOVER_PERFORMANCE_COUNTERS`||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.ProviderTypes>|[Conjunto de linhas DBSCHEMA_PROVIDER_TYPES](../schema-rowsets/ole-db/dbschema-provider-types-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.SchemaRowsets>|[Conjunto de linhas DISCOVER_SCHEMA_ROWSETS](../schema-rowsets/xml/discover-schema-rowsets-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Sessions>|`DISCOVER_SESSIONS`||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Sets>|[Conjunto de linhas MDSCHEMA_SETS](../schema-rowsets/ole-db-olap/mdschema-sets-rowset.md)|AdomdConnection.Cubes[].NamedSets|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Tables>|[Conjunto de linhas DBSCHEMA_TABLES](../schema-rowsets/ole-db/dbschema-tables-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.TablesInfo>|`DBSCHEMA_TABLES_INFO`||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.TraceColumns>|`DISCOVER_TRACE_COLUMNS`||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.TraceDefinitionProviderInfo>|`DISCOVER_TRACE_DEFINITION_PROVIDERINFO`||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.TraceEventCategories>|`DISCOVER_TRACE_EVENT_CATEGORIES`||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Traces>|`DISCOVER_TRACES`||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Transactions>|`DISCOVER_TRANSACTIONS`||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.XmlaProperties>|[Conjunto de linhas DISCOVER_PROPERTIES](../schema-rowsets/xml/discover-properties-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.XmlMetadata>|[Conjunto de linhas DISCOVER_XML_METADATA](../schema-rowsets/xml/discover-xml-metadata-rowset.md)||  
  
## <a name="see-also"></a>Consulte também  
 [Programação de cliente ADOMD.NET](adomd-net-client-programming.md)   
 [Programação de cliente ADOMD.NET](adomd-net-client-programming.md)   
 [Conjuntos de linhas de esquema do Analysis Services](../schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
