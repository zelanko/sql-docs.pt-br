---
title: Coleções (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- collections [Analysis Services Scripting Language]
- Analysis Services Scripting Language, collections
- ASSL, collections
ms.assetid: 072b8c6b-1550-4cab-ae64-ba0e3e60b059
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a56b577f39c2b2f4ef7a4033203fcda9706d1370
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37300986"
---
# <a name="collections-assl"></a>Coleções (ASSL)
  Esta seção de referência contém informações de sintaxe e uso de cada elemento que age como uma coleção no esquema ASSL (Analysis Services Scripting Language).  
  
 Embora o esquema ASSL contenha somente elementos XML, do ponto de vista do desenvolvedor, os elementos descritos nessa seção correspondem a coleções de objetos, como as coleções `Dimensions` e `Cubes`.  
  
 As coleções são, na maioria das vezes, coleções de elementos de objeto, nas quais um substantivo plural designa a coleção (por exemplo, `Cubes`); a coleção contém elementos designados pelo mesmo substantivo no singular (por exemplo, `Cube`).  
  
 Em alguns casos, o esquema não adere a esta regra geral. Por exemplo, a coleção `ClassifiedColumns` contém elementos `ClassifiedColumnID`.  
  
 Em outros casos, uma coleção contém elementos que correspondem a propriedades de objeto, não a objetos. Por exemplo, a coleção `Aliases` contém propriedades `Alias`, cada uma delas sendo um valor de cadeia de caracteres simples.  
  
|Elemento|Description|  
|-------------|-----------------|  
|[Contas de elemento &#40;ASSL&#41;](accounts-element-assl.md)|Contém a coleção de tipos de conta definidos em uma [banco de dados](../objects/database-element-assl.md) elemento.|  
|[Elemento Actions &#40;ASSL&#41;](actions-element-assl.md)|Contém a coleção de ações para um [cubo](../objects/cube-element-assl.md) ou [perspectiva](../objects/perspective-element-assl.md) elemento.|  
|[Elemento AggregationDesigns &#40;ASSL&#41;](aggregationdesigns-element-assl.md)|Contém a coleção de designs de agregação que pode ser compartilhada por várias partições em um banco de dados.|  
|[Elemento AggregationInstances &#40;ASSL&#41;](aggregationinstances-element-assl.md)|Contém a coleção de instâncias de agregação que são definidos em uma [partição](../objects/partition-element-assl.md) elemento.|  
|[Elemento Aggregations &#40;ASSL&#41;](aggregations-element-assl.md)|Contém a coleção de agregações definida para um [AggregationDesign](../objects/aggregationdesign-element-assl.md) elemento.|  
|[Elemento AlgorithmParameters &#40;ASSL&#41;](algorithmparameters-element-assl.md)|Contém a coleção de parâmetros para o algoritmo usado por um [MiningModel](../objects/miningmodel-element-assl.md) elemento.|  
|[Elemento aliases &#40;ASSL&#41;](aliases-element-assl.md)|Contém a coleção de [Alias](../properties/alias-element-assl.md) elementos associados a um [conta](../objects/account-element-assl.md) elemento|  
|[Elemento AllMemberTranslations &#40;ASSL&#41;](translations-element-assl.md)|Contém a coleção de [tradução](../objects/translation-element-assl.md) elementos para a legenda do membro All de um [hierarquia](../objects/hierarchy-element-assl.md) elemento.|  
|[Elemento Annotations &#40;ASSL&#41;](annotations-element-assl.md)|Contém a coleção de [anotação](../objects/annotation-element-assl.md) elementos associados ao elemento pai.|  
|[Elemento assemblies &#40;ASSL&#41;](assemblies-element-assl.md)|Contém a coleção de [Assembly](../objects/assembly-element-assl.md) elementos associados a um [Server](../objects/server-element-assl.md) elemento ou uma [banco de dados](../objects/database-element-assl.md) elemento.|  
|[Elemento AttributeAllMemberTranslations &#40;ASSL&#41;](attributeallmembertranslations-element-assl.md)|Contém a coleção de traduções para a legenda do membro All da dimensão.|  
|[Elemento AttributePermissions &#40;ASSL&#41;](attributepermissions-element-assl.md)|Contém a coleção de permissões de atributo de um indivíduo [função](../objects/role-element-assl.md) elemento em uma dimensão específica de um [cubo](../objects/cube-element-assl.md) elemento.|  
|[Elemento AttributeRelationships &#40;ASSL&#41;](relationships-element-assl.md)|Contém a coleção de [AttributeRelationship](../objects/attributerelationship-element-assl.md) elementos para o atributo.|  
|[Atributos do elemento &#40;ASSL&#41;](attributes-element-assl.md)|Contém a coleção de atributos para a dimensão associada.|  
|[Bloqueia o elemento &#40;ASSL&#41;](blocks-element-assl.md)|Contém a coleção de blocos de dados binários que representam o conteúdo binário de um [ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md) elemento.|  
|[Elemento CalculationProperties &#40;ASSL&#41;](calculationproperties-element-assl.md)|Contém a coleção de [CalculationProperty](../objects/calculationproperty-element-assl.md) elementos associados a um [MdxScript](../objects/mdxscript-element-assl.md) elemento.|  
|[Elemento calculations &#40;ASSL&#41;](calculations-element-assl.md)|Contém a coleção de [PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md) elementos associados a um [perspectiva](../objects/perspective-element-assl.md) elemento.|  
|[Elemento CellPermissions &#40;ASSL&#41;](cellpermissions-element-assl.md)|Contém a coleção de permissões para células no associado [cubo](../objects/cube-element-assl.md) elemento.|  
|[Elemento ClassifiedColumns &#40;ASSL&#41;](columns-element-assl.md)|Contém a coleção de colunas relacionadas classificadas pelo [ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md) elemento.|  
|[Elemento Columns &#40;ASSL&#41;](columns-element-assl.md)|Contém a coleção de colunas associada ao elemento pai.|  
|[Comandos do elemento &#40;ASSL&#41;](commands-element-assl.md)|Contém a coleção de elementos [Command](../objects/command-element-assl.md) associados a um elemento [MdxScript](../objects/mdxscript-element-assl.md) .|  
|[Elemento CubePermissions &#40;ASSL&#41;](cubepermissions-element-assl.md)|Contém a coleção de permissões aplicáveis a um [cubo](../objects/cube-element-assl.md) elemento.|  
|[Cubos do elemento &#40;ASSL&#41;](cubes-element-assl.md)|Contém a coleção de [cubo](../objects/cube-element-assl.md) elementos associados a um [banco de dados](../objects/database-element-assl.md) elemento.|  
|[Elemento DatabasePermissions &#40;ASSL&#41;](databasepermissions-element-assl.md)|Contém a coleção de [DatabasePermission](../objects/databasepermission-element-assl.md) elementos associados a um [banco de dados](../objects/database-element-assl.md) elemento.|  
|[Bancos de dados do elemento &#40;ASSL&#41;](databases-element-assl.md)|Contém a coleção de [banco de dados](../objects/database-element-assl.md) elementos associados a um [Server](../objects/server-element-assl.md) elemento.|  
|[Elemento DataSources &#40;ASSL&#41;](datasources-element-assl.md)|Contém a coleção de [DataSourcePermission](../objects/datasourcepermission-element-assl.md) elementos associados a um [DataSource](../data-type/datasource-data-type-assl.md) tipo de dados.|  
|[Elemento DataSourcePermissions &#40;ASSL&#41;](datasourcepermissions-element-assl.md)|Contém a coleção de [fonte de dados](../objects/datasource-element-assl.md) elementos associados a um [banco de dados](../objects/database-element-assl.md) elemento.|  
|[Elemento DataSourceViews &#40;ASSL&#41;](datasourceviews-element-assl.md)|Contém a coleção de [DataSourceView](../objects/datasourceview-element-assl.md) elementos associados a um [banco de dados](../objects/database-element-assl.md) elemento.|  
|[Elemento DimensionPermissions &#40;ASSL&#41;](dimensionpermissions-element-assl.md)|Contém a coleção de permissões aplicáveis a um [dimensão](../objects/dimension-element-assl.md) elemento ou um [CubePermission](../objects/cubepermission-element-assl.md) elemento.|  
|[Dimensões do elemento &#40;ASSL&#41;](dimensions-element-assl.md)|Contém a coleção de dimensões associada ao elemento pai.|  
|[Elemento Events &#40;ASSL&#41;](events-element-assl.md)|Define a coleção de elementos de eventos a serem capturados por um [rastreamento](../objects/trace-element-assl.md).|  
|[Arquivos de elemento &#40;ASSL&#41;](files-element-assl.md)|Contém a coleção de [arquivo](../objects/file-element-assl.md) elementos que compõem um [ClrAssembly](../data-type/assembly-data-type-assl.md) elemento.|  
|[Elemento ForeignKeyColumns &#40;ASSL&#41;](keycolumns-element-assl.md)|Contém a coleção das colunas que identificam a junção à tabela pai de uma fonte de dados relacional.|  
|[Elemento Groups &#40;ASSL&#41;](groups-element-assl.md)|Contém a coleção de grupos de membros ligados a um atributo.|  
|[Elemento hierarchies &#40;ASSL&#41;](hierarchies-element-assl.md)|Contém a coleção de [hierarquia](../objects/hierarchy-element-assl.md) elementos associados ao elemento pai.|  
|[Elemento IncrementalProcessingNotifications &#40;ASSL&#41;](incrementalprocessingnotifications-element-assl.md)|Contém a coleção de [IncrementalProcessingNotification](../objects/incrementalprocessingnotification-element-assl.md) elementos que fornecem informações para o [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento sobre consultas a serem executadas para determinar o andamento do processamento incremental.|  
|[Elemento KeyColumns &#40;ASSL&#41;](keycolumns-element-assl.md)|Contém a coleção de [KeyColumn](../objects/column-element-assl.md) definições de elemento para um objeto pai.|  
|[Elemento KPIs &#40;ASSL&#41;](kpis-element-assl.md)|Contém a coleção de [Kpi](../objects/kpi-element-assl.md) elementos associados ao elemento pai.|  
|[Os níveis de elemento &#40;ASSL&#41;](levels-element-assl.md)|Contém a coleção de [nível](../objects/level-element-assl.md) elementos em um [hierarquia](../objects/hierarchy-element-assl.md) elemento.|  
|[Elemento MdxScripts &#40;ASSL&#41;](mdxscripts-element-assl.md)|Contém a coleção de [MdxScript](../objects/mdxscript-element-assl.md) elementos associados a um [cubo](../objects/cube-element-assl.md) elemento.|  
|[Elemento MeasureGroups &#40;ASSL&#41;](measuregroups-element-assl.md)|Contém a coleção de [MeasureGroup](../objects/group-element-assl.md) elementos associados ao elemento pai.|  
|[Mede o elemento &#40;ASSL&#41;](measures-element-assl.md)|Contém a coleção de [medida](../objects/measure-element-assl.md) elementos associados ao elemento pai.|  
|[Elemento Members &#40;ASSL&#41;](members-element-assl.md)|Contém a coleção de elementos [Member](../objects/member-element-assl.md) do elemento pai.|  
|[Elemento MiningModelPermissions &#40;ASSL&#41;](miningmodelpermissions-element-assl.md)|Contém a coleção de permissões para um [MiningModel](../objects/miningmodel-element-assl.md) elemento.|  
|[Elemento MiningModels &#40;ASSL&#41;](miningmodels-element-assl.md)|Contém a coleção de [MiningModel](../objects/miningmodel-element-assl.md) elementos associados a um [MiningStructure](../objects/miningstructure-element-assl.md).|  
|[Elemento MiningStructurePermissions &#40;ASSL&#41;](miningstructurepermissions-element-assl.md)|Contém a coleção de permissões em um [MiningStructure](../objects/miningstructure-element-assl.md) elemento.|  
|[Elemento MiningStructures &#40;ASSL&#41;](miningstructures-element-assl.md)|Contém a coleção de [MiningStructure](../objects/miningstructure-element-assl.md) elementos em um [banco de dados](../objects/database-element-assl.md) elemento.|  
|[Elemento ModelingFlags &#40;ASSL&#41;](modelingflags-element-assl.md)|Contém a coleção de [ModelingFlag](../objects/modelingflag-element-assl.md) elementos para uma coluna em uma [MiningStructure](../objects/miningstructure-element-assl.md) ou uma [MiningModel](../objects/miningmodel-element-assl.md).|  
|[Elemento NamingTemplateTranslations &#40;ASSL&#41;](namingtemplatetranslations-element-assl.md)|Fornece uma coleção de traduções localizadas para o [NamingTemplate](../properties/namingtemplate-element-assl.md) elemento pai [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md).|  
|[Particiona o elemento &#40;ASSL&#41;](partitions-element-assl.md)|Contém a coleção de [partição](../objects/partition-element-assl.md) elementos usados por um [MeasureGroup](../objects/group-element-assl.md) elemento ou a coleção de ligações de partição que compõem uma fora de linha [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-out-of-line-assl.md)elemento.|  
|[Elemento Perspectives &#40;ASSL&#41;](perspectives-element-assl.md)|Contém a coleção de [perspectiva](../objects/perspective-element-assl.md) elementos associados a um [cubo](../objects/cube-element-assl.md) elemento.|  
|[Elemento QueryNotifications &#40;ASSL&#41;](querynotifications-element-assl.md)|Contém a coleção de [QueryNotification](../objects/querynotification-element-assl.md) elementos que fornecem informações para o [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento sobre consultas a ser executada para determinar se uma fonte de dados foi modificada.|  
|[Elemento ReportFormatParameters &#40;ASSL&#41;](reportformatparameters-element-assl.md)|Contém a coleção de elementos [ReportFormatParameter](../objects/reportformatparameter-element-asl.md) para um elemento [ReportAction](../data-type/action-data-type-assl.md) .|  
|[Elemento ReportParameters &#40;ASSL&#41;](reportparameters-element-assl.md)|Contém a coleção de [ReportParameter](../objects/reportparameter-element-assl.md) elementos para um [ReportAction](../data-type/action-data-type-assl.md) elemento.|  
|[Elemento roles &#40;ASSL&#41;](roles-element-assl.md)|Contém a coleção de elementos [Role](../objects/role-element-assl.md) definidos sob o elemento pai.|  
|[Elemento ServerProperties &#40;ASSL&#41;](serverproperties-element-assl.md)|Contém a coleção de [ServerProperty](../objects/serverproperty-element-assl.md) elementos associados a um [Server](../objects/server-element-assl.md) elemento.|  
|[Elemento TableNotifications &#40;ASSL&#41;](tablenotifications-element-assl.md)|Contém a coleção de [TableNotification](../objects/tablenotification-element-assl.md) elementos que fornecem informações para o [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento sobre tabelas ou exibições em uma fonte de dados que foram modificadas.|  
|[Rastreia o elemento &#40;ASSL&#41;](traces-element-assl.md)|Contém a coleção de elementos [Trace](../objects/trace-element-assl.md) associados a um elemento [Server](../objects/server-element-assl.md) .|  
|[Elemento translations &#40;ASSL&#41;](translations-element-assl.md)|Contém a coleção de [tradução](../objects/translation-element-assl.md) elementos associados ao elemento pai.|  
|[Elemento UnknownMemberTranslations &#40;ASSL&#41;](unknownmembertranslations-element-assl.md)|Contém a coleção de traduções para a legenda do [UnknownMember](../properties/unknownmember-element-assl.md) elemento de uma dimensão.|  
  
## <a name="see-also"></a>Consulte também  
 [Hierarquia Analysis Services Scripting Language XML elemento &#40;ASSL&#41;](../analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
