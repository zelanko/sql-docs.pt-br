---
title: "Coleções (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- collections [Analysis Services Scripting Language]
- Analysis Services Scripting Language, collections
- ASSL, collections
ms.assetid: 072b8c6b-1550-4cab-ae64-ba0e3e60b059
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f9751d6b4052575c85abf41f745817def8f7ae75
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="collections-assl"></a>Coleções (ASSL)
  Esta seção de referência contém informações de sintaxe e uso de cada elemento que age como uma coleção no esquema ASSL (Analysis Services Scripting Language).  
  
 Embora o esquema ASSL contenha somente elementos XML, do ponto de vista do desenvolvedor, os elementos descritos nessa seção correspondem a coleções de objetos, como o **dimensões** e **cubos** coleções.  
  
 Coleções são principalmente as coleções de elementos de objeto, no qual um substantivo plural designa a coleção (para obter exemplos, **cubos**), e a coleção contém elementos designados pelo mesmo substantivo no singular (por exemplo,  **Cubo**).  
  
 Em alguns casos, o esquema não adere a esta regra geral. Por exemplo, o **ClassifiedColumns** coleção contém **ClassifiedColumnID** elementos.  
  
 Em outros casos, uma coleção contém elementos que correspondem a propriedades de objeto, não a objetos. Por exemplo, o **Aliases** coleção contém **Alias** propriedades, cada um deles é um valor de cadeia de caracteres simples.  
  
|Elemento|Description|  
|-------------|-----------------|  
|[Elemento Accounts &#40; ASSL &#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)|Contém a coleção de tipos de conta que são definidos em um [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.|  
|[Elemento Actions &#40; ASSL &#41;](../../../analysis-services/scripting/collections/actions-element-assl.md)|Contém a coleção de ações para um [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) ou [perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md) elemento.|  
|[Elemento AggregationDesigns &#40; ASSL &#41;](../../../analysis-services/scripting/collections/aggregationdesigns-element-assl.md)|Contém a coleção de designs de agregação que pode ser compartilhada por várias partições em um banco de dados.|  
|[Elemento AggregationInstances &#40; ASSL &#41;](../../../analysis-services/scripting/collections/aggregationinstances-element-assl.md)|Contém a coleção de instâncias de agregação que são definidos em um [partição](../../../analysis-services/scripting/objects/partition-element-assl.md) elemento.|  
|[Elemento Aggregations &#40; ASSL &#41;](../../../analysis-services/scripting/collections/aggregations-element-assl.md)|Contém a coleção de agregações definida para um [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md) elemento.|  
|[Elemento AlgorithmParameters &#40; ASSL &#41;](../../../analysis-services/scripting/collections/algorithmparameters-element-assl.md)|Contém a coleção de parâmetros para o algoritmo usado por um [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) elemento.|  
|[Elemento aliases &#40; ASSL &#41;](../../../analysis-services/scripting/collections/aliases-element-assl.md)|Contém a coleção de [Alias](../../../analysis-services/scripting/properties/alias-element-assl.md) elementos associados a um [conta](../../../analysis-services/scripting/objects/account-element-assl.md) elemento|  
|[Elemento AllMemberTranslations &#40; ASSL &#41;](../../../analysis-services/scripting/collections/allmembertranslations-element-assl.md)|Contém a coleção de [tradução](../../../analysis-services/scripting/objects/translation-element-assl.md) elementos para a legenda do membro All de um [hierarquia](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) elemento.|  
|[Elemento Annotations &#40; ASSL &#41;](../../../analysis-services/scripting/collections/annotations-element-assl.md)|Contém a coleção de [anotação](../../../analysis-services/scripting/objects/annotation-element-assl.md) elementos associados ao elemento pai.|  
|[Elemento assemblies &#40; ASSL &#41;](../../../analysis-services/scripting/collections/assemblies-element-assl.md)|Contém a coleção de [Assembly](../../../analysis-services/scripting/objects/assembly-element-assl.md) elementos associados a um [servidor](../../../analysis-services/scripting/objects/server-element-assl.md) elemento ou um [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.|  
|[Elemento AttributeAllMemberTranslations &#40; ASSL &#41;](../../../analysis-services/scripting/collections/attributeallmembertranslations-element-assl.md)|Contém a coleção de traduções para a legenda do membro All da dimensão.|  
|[Elemento AttributePermissions &#40; ASSL &#41;](../../../analysis-services/scripting/collections/attributepermissions-element-assl.md)|Contém a coleção de permissões de atributo de um indivíduo [função](../../../analysis-services/scripting/objects/role-element-assl.md) elemento em uma dimensão específica de um [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento.|  
|[Elemento AttributeRelationships &#40; ASSL &#41;](../../../analysis-services/scripting/collections/attributerelationships-element-assl.md)|Contém a coleção de [AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md) elementos para o atributo.|  
|[Atributos de elemento &#40; ASSL &#41;](../../../analysis-services/scripting/collections/attributes-element-assl.md)|Contém a coleção de atributos para a dimensão associada.|  
|[Elemento Blocks &#40; ASSL &#41;](../../../analysis-services/scripting/collections/blocks-element-assl.md)|Contém a coleção de blocos de dados binários que representam o conteúdo binário de um [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md) elemento.|  
|[Elemento CalculationProperties &#40; ASSL &#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)|Contém a coleção de [CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md) elementos associados a um [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md) elemento.|  
|[Elemento calculations &#40; ASSL &#41;](../../../analysis-services/scripting/collections/calculations-element-assl.md)|Contém a coleção de [PerspectiveCalculation](../../../analysis-services/scripting/data-type/perspectivecalculation-data-type-assl.md) elementos associados a um [perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md) elemento.|  
|[Elemento CellPermissions &#40; ASSL &#41;](../../../analysis-services/scripting/collections/cellpermissions-element-assl.md)|Contém a coleção de permissões para células no associado [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento.|  
|[Elemento ClassifiedColumns &#40; ASSL &#41;](../../../analysis-services/scripting/collections/classifiedcolumns-element-assl.md)|Contém a coleção de colunas relacionadas classificadas pelo [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md) elemento.|  
|[Elemento de colunas &#40; ASSL &#41;](../../../analysis-services/scripting/collections/columns-element-assl.md)|Contém a coleção de colunas associada ao elemento pai.|  
|[Elemento Commands &#40; ASSL &#41;](../../../analysis-services/scripting/collections/commands-element-assl.md)|Contém a coleção de elementos [Command](../../../analysis-services/scripting/objects/command-element-assl.md) associados a um elemento [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md) .|  
|[Elemento CubePermissions &#40; ASSL &#41;](../../../analysis-services/scripting/collections/cubepermissions-element-assl.md)|Contém a coleção de permissões aplicáveis a um [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento.|  
|[Elemento Cubes &#40; ASSL &#41;](../../../analysis-services/scripting/collections/cubes-element-assl.md)|Contém a coleção de [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elementos associados a um [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.|  
|[Elemento DatabasePermissions &#40; ASSL &#41;](../../../analysis-services/scripting/collections/databasepermissions-element-assl.md)|Contém a coleção de [DatabasePermission](../../../analysis-services/scripting/objects/databasepermission-element-assl.md) elementos associados a um [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.|  
|[Elemento de bancos de dados &#40; ASSL &#41;](../../../analysis-services/scripting/collections/databases-element-assl.md)|Contém a coleção de [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elementos associados a um [Server](../../../analysis-services/scripting/objects/server-element-assl.md) elemento.|  
|[Elemento de fontes de dados &#40; ASSL &#41;](../../../analysis-services/scripting/collections/datasources-element-assl.md)|Contém a coleção de [DataSourcePermission](../../../analysis-services/scripting/objects/datasourcepermission-element-assl.md) elementos associados a um [DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md) tipo de dados.|  
|[Elemento DataSourcePermissions &#40; ASSL &#41;](../../../analysis-services/scripting/collections/datasourcepermissions-element-assl.md)|Contém a coleção de [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md) elementos associados a um [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.|  
|[Elemento DataSourceViews &#40; ASSL &#41;](../../../analysis-services/scripting/collections/datasourceviews-element-assl.md)|Contém a coleção de [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md) elementos associados a um [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.|  
|[Elemento DimensionPermissions &#40; ASSL &#41;](../../../analysis-services/scripting/collections/dimensionpermissions-element-assl.md)|Contém a coleção de permissões aplicáveis a um [dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md) elemento ou um [CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md) elemento.|  
|[Elemento Dimensions &#40; ASSL &#41;](../../../analysis-services/scripting/collections/dimensions-element-assl.md)|Contém a coleção de dimensões associada ao elemento pai.|  
|[Elemento de eventos &#40; ASSL &#41;](../../../analysis-services/scripting/collections/events-element-assl.md)|Define a coleção de elementos de eventos a serem capturados por um [rastreamento](../../../analysis-services/scripting/objects/trace-element-assl.md).|  
|[Elemento de arquivos &#40; ASSL &#41;](../../../analysis-services/scripting/collections/files-element-assl.md)|Contém a coleção de [arquivo](../../../analysis-services/scripting/objects/file-element-assl.md) elementos que compõem um [ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md) elemento.|  
|[Elemento ForeignKeyColumns &#40; ASSL &#41;](../../../analysis-services/scripting/collections/foreignkeycolumns-element-assl.md)|Contém a coleção das colunas que identificam a junção à tabela pai de uma fonte de dados relacional.|  
|[Elemento Groups &#40; ASSL &#41;](../../../analysis-services/scripting/collections/groups-element-assl.md)|Contém a coleção de grupos de membros ligados a um atributo.|  
|[Elemento hierarchies &#40; ASSL &#41;](../../../analysis-services/scripting/collections/hierarchies-element-assl.md)|Contém a coleção de [hierarquia](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) elementos associados ao elemento pai.|  
|[Elemento IncrementalProcessingNotifications &#40; ASSL &#41;](../../../analysis-services/scripting/collections/incrementalprocessingnotifications-element-assl.md)|Contém a coleção de [IncrementalProcessingNotification](../../../analysis-services/scripting/objects/incrementalprocessingnotification-element-assl.md) elementos que fornecem informações para o [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) elemento sobre consultas a serem executadas para determinar o andamento do processamento incremental.|  
|[Elemento KeyColumns &#40; ASSL &#41;](../../../analysis-services/scripting/collections/keycolumns-element-assl.md)|Contém a coleção de [KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md) definições de elemento para um objeto pai.|  
|[Elemento KPIs &#40; ASSL &#41;](../../../analysis-services/scripting/collections/kpis-element-assl.md)|Contém a coleção de [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md) elementos associados ao elemento pai.|  
|[Elemento Levels &#40; ASSL &#41;](../../../analysis-services/scripting/collections/levels-element-assl.md)|Contém a coleção de [nível](../../../analysis-services/scripting/objects/level-element-assl.md) elementos em uma [hierarquia](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) elemento.|  
|[Elemento MdxScripts &#40; ASSL &#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)|Contém a coleção de [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md) elementos associados a um [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento.|  
|[Elemento MeasureGroups &#40; ASSL &#41;](../../../analysis-services/scripting/collections/measuregroups-element-assl.md)|Contém a coleção de [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md) elementos associados ao elemento pai.|  
|[Elemento Measures &#40; ASSL &#41;](../../../analysis-services/scripting/collections/measures-element-assl.md)|Contém a coleção de [medidas](../../../analysis-services/scripting/objects/measure-element-assl.md) elementos associados ao elemento pai.|  
|[Elemento Members &#40; ASSL &#41;](../../../analysis-services/scripting/collections/members-element-assl.md)|Contém a coleção de elementos [Member](../../../analysis-services/scripting/objects/member-element-assl.md) do elemento pai.|  
|[Elemento MiningModelPermissions &#40; ASSL &#41;](../../../analysis-services/scripting/collections/miningmodelpermissions-element-assl.md)|Contém a coleção de permissões para um [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) elemento.|  
|[Elemento MiningModels &#40; ASSL &#41;](../../../analysis-services/scripting/collections/miningmodels-element-assl.md)|Contém a coleção de [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) elementos associados a um [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md).|  
|[Elemento MiningStructurePermissions &#40; ASSL &#41;](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md)|Contém a coleção de permissões em um [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) elemento.|  
|[Elemento MiningStructures &#40; ASSL &#41;](../../../analysis-services/scripting/collections/miningstructures-element-assl.md)|Contém a coleção de [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) elementos em uma [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.|  
|[Elemento ModelingFlags &#40; ASSL &#41;](../../../analysis-services/scripting/collections/modelingflags-element-assl.md)|Contém a coleção de [ModelingFlag](../../../analysis-services/scripting/objects/modelingflag-element-assl.md) elementos de uma coluna em uma [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) ou um [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md).|  
|[Elemento NamingTemplateTranslations &#40; ASSL &#41;](../../../analysis-services/scripting/collections/namingtemplatetranslations-element-assl.md)|Fornece uma coleção de traduções localizadas para o [NamingTemplate](../../../analysis-services/scripting/properties/namingtemplate-element-assl.md) elemento do pai [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md).|  
|[Elemento Partitions &#40; ASSL &#41;](../../../analysis-services/scripting/collections/partitions-element-assl.md)|Contém a coleção de [partição](../../../analysis-services/scripting/objects/partition-element-assl.md) elementos usados por um [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md) elemento ou a coleção de ligações de partição que compõem uma fora de linha [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)elemento.|  
|[Elemento Perspectives &#40; ASSL &#41;](../../../analysis-services/scripting/collections/perspectives-element-assl.md)|Contém a coleção de [perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md) elementos associados a um [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento.|  
|[Elemento QueryNotifications &#40; ASSL &#41;](../../../analysis-services/scripting/collections/querynotifications-element-assl.md)|Contém a coleção de [QueryNotification](../../../analysis-services/scripting/objects/querynotification-element-assl.md) elementos que fornecem informações para o [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) elemento sobre consultas a serem executadas para determinar se uma fonte de dados foi modificada.|  
|[Elemento ReportFormatParameters &#40; ASSL &#41;](../../../analysis-services/scripting/collections/reportformatparameters-element-assl.md)|Contém a coleção de elementos [ReportFormatParameter](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md) para um elemento [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md) .|  
|[Elemento ReportParameters &#40; ASSL &#41;](../../../analysis-services/scripting/collections/reportparameters-element-assl.md)|Contém a coleção de [ReportParameter](../../../analysis-services/scripting/objects/reportparameter-element-assl.md) elementos para um [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md) elemento.|  
|[Elemento roles &#40; ASSL &#41;](../../../analysis-services/scripting/collections/roles-element-assl.md)|Contém a coleção de elementos [Role](../../../analysis-services/scripting/objects/role-element-assl.md) definidos sob o elemento pai.|  
|[Elemento ServerProperties &#40; ASSL &#41;](../../../analysis-services/scripting/collections/serverproperties-element-assl.md)|Contém a coleção de [ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md) elementos associados a um [Server](../../../analysis-services/scripting/objects/server-element-assl.md) elemento.|  
|[Elemento TableNotifications &#40; ASSL &#41;](../../../analysis-services/scripting/collections/tablenotifications-element-assl.md)|Contém a coleção de [TableNotification](../../../analysis-services/scripting/objects/tablenotification-element-assl.md) elementos que fornecem informações para o [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) elemento sobre tabelas ou exibições em uma fonte de dados que foram modificadas.|  
|[Elemento de rastreamentos &#40; ASSL &#41;](../../../analysis-services/scripting/collections/traces-element-assl.md)|Contém a coleção de elementos [Trace](../../../analysis-services/scripting/objects/trace-element-assl.md) associados a um elemento [Server](../../../analysis-services/scripting/objects/server-element-assl.md) .|  
|[Elemento translations &#40; ASSL &#41;](../../../analysis-services/scripting/collections/translations-element-assl.md)|Contém a coleção de [tradução](../../../analysis-services/scripting/objects/translation-element-assl.md) elementos associados ao elemento pai.|  
|[Elemento UnknownMemberTranslations &#40; ASSL &#41;](../../../analysis-services/scripting/collections/unknownmembertranslations-element-assl.md)|Contém a coleção de traduções da legenda do [UnknownMember](../../../analysis-services/scripting/properties/unknownmember-element-assl.md) elemento de uma dimensão.|  
  
## <a name="see-also"></a>Consulte também  
 [Hierarquia de elementos XML de linguagem de script &#40; do Analysis Services ASSL &#41;](../../../analysis-services/scripting/analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  

