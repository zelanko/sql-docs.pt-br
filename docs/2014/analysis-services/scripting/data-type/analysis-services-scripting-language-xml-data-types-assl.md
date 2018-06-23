---
title: Tipos de dados XML de linguagem script (ASSL) do Analysis Services | Microsoft Docs
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
api_name:
- Analysis Services Scripting Language XML Data Types
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ASSL, data types
- Analysis Services Scripting Language, data types
- data types [Analysis Services Scripting Language]
ms.assetid: 8e527916-932e-48ec-9010-f22cd4b721e2
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3420e553b1391fb9645f7e3bffa884e255a90897
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116045"
---
# <a name="analysis-services-scripting-language-xml-data-types-assl"></a>Tipos de dados XML de linguagem script (ASSL) do Analysis Services
  Esta seção de referência contém informações de sintaxe e uso de cada elemento que age como um tipo no esquema ASSL (Analysis Services Scripting Language).  
  
 Embora o esquema ASSL contenha somente elementos XML, do ponto de vista do desenvolvedor, os elementos descritos nessa seção correspondem aos tipos, como `Binding` e `Permission`, que são usados para definir os elementos filho e as propriedades de outros objetos.  
  
 Os elementos de tipo, como os elementos de objetos, nunca são elementos do nível folha no esquema ASSL, mas têm elementos filho e elementos que correspondem às propriedades de objeto.  
  
 No entanto um elemento de tipo nunca aparece como um elemento em um script que define ou descreve [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] objetos. Em vez disso, ele aparece como o tipo de outros elementos de objeto, normalmente designados com o atributo `type` do esquema da instância do esquema XML usando `xsi:type` ou `xs:type`. Por exemplo, `<Assembly xsi:type="ClrAssembly">...</Assembly>`.  
  
 Em alguns casos, um tipo é derivado de outro tipo. Por exemplo, o tipo `CubeBinding` é derivado do tipo pai `Binding`.  
  
|Elemento|Description|  
|-------------|-----------------|  
|[Tipo de dados de ação &#40;ASSL&#41;](action-data-type-assl.md)|Define um tipo de dados primitivo abstrato que representa uma ação em um [cubo](../objects/cube-element-assl.md) elemento ou um [perspectiva](../objects/perspective-element-assl.md) elemento.|  
|[Tipo de dados AggregationAttribute &#40;ASSL&#41;](aggregationattribute-data-type-assl.md)|Define um tipo de dados primitivo que representa a associação entre um [agregação](../objects/aggregation-element-assl.md) elemento e um atributo.|  
|[Tipo de dados AggregationDesignAttribute &#40;ASSL&#41;](aggregationdesignattribute-data-type-assl.md)|Define um tipo de dados primitivo que representa a associação entre um atributo e um [AggregationDesignDimension](dimension-data-type-assl.md) elemento.|  
|[Tipo de dados AggregationDesignDimension &#40;ASSL&#41;](dimension-data-type-assl.md)|Define um tipo de dados primitivo que representa a relação entre uma dimensão de cubo e um [AggregationDesign](../objects/aggregationdesign-element-assl.md) elemento.|  
|[Tipo de dados AggregationDimension &#40;ASSL&#41;](aggregationdimension-data-type-assl.md)|Define um tipo de dados primitivo que representa a relação entre uma dimensão e um [agregação](../objects/aggregation-element-assl.md) elemento.|  
|[Tipo de dados AggregationInstanceAttribute &#40;ASSL&#41;](aggregationinstanceattribute-data-type-assl.md)|Define um tipo de dados primitivos que representa informações sobre um atributo usado por uma instância de agregação.|  
|[Tipo de dados AggregationInstanceCubeDimension &#40;ASSL&#41;](cubedimension-data-type-assl.md)|Define um tipo de dados primitivos que representa informações sobre uma dimensão de cubo usada por uma instância de agregação.|  
|[Tipo de dados AggregationInstanceMeasure &#40;ASSL&#41;](aggregationinstancemeasure-data-type-assl.md)|Define um tipo de dados primitivo que representa informações sobre uma medida usada por uma instância de agregação.|  
|[Tipo de dados assembly &#40;ASSL&#41;](assembly-data-type-assl.md)|Define um tipo de dados primitivo abstrato que representa um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] assembly ou uma biblioteca de vínculo dinâmico (DLL) COM associado com um [servidor](../objects/server-element-assl.md) ou [banco de dados](../objects/database-element-assl.md) elemento.|  
|[Tipo de dados AttributeBinding &#40;ASSL&#41;](binding-data-type-assl.md)|Define um tipo de dados derivado que representa uma associação para um [atributo](../objects/attribute-element-assl.md) elemento.|  
|[Tipo de dados AttributeTranslation &#40;ASSL&#41;](translation-data-type-assl.md)|Define um tipo de dados derivado que representa uma tradução associada a um [atributo](../objects/attribute-element-assl.md) elemento|  
|[Tipo de dados de associação &#40;ASSL&#41;](binding-data-type-assl.md)|Define um tipo de dados primitivo abstrato que representa uma relação de dependência entre dois objetos na qual os dados ou os metadados de um objeto dependem dos dados ou metadados de um objeto associado.|  
|[Tipo de dados ClrAssembly &#40;ASSL&#41;](clrassembly-data-type-assl.md)|Define um tipo de dados derivado que representa um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] assembly associado com um [banco de dados](../objects/database-element-assl.md) ou [Server](../objects/server-element-assl.md) elemento|  
|[Tipo de dados ClrAssemblyFile &#40;ASSL&#41;](clrassemblyfile-data-type-assl.md)|Define um tipo de dados primitivo que representa um dos arquivos que compõem um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] assembly ([ClrAssembly](clrassembly-data-type-assl.md) elemento).|  
|[Tipo de dados ColumnBinding &#40;ASSL&#41;](columnbinding-data-type-assl.md)|Define um tipo de dados derivado que representa a associação de uma coluna em uma exibição da fonte de dados para um [DataItem](dataitem-data-type-assl.md) elemento.|  
|[Tipo de dados ComAssembly &#40;ASSL&#41;](comassembly-data-type-assl.md)|Define um tipo de dados derivado que representa uma biblioteca COM associada a um [servidor](../objects/server-element-assl.md) ou [banco de dados](../objects/database-element-assl.md) elemento.|  
|[Tipo de dados CubeAttribute &#40;ASSL&#41;](cubeattribute-data-type-assl.md)|Define um tipo de dados primitivo que representa um atributo associado a um [cubo](../objects/cube-element-assl.md) elemento.|  
|[Tipo de dados CubeAttributeBinding &#40;ASSL&#41;](cubebinding-data-type-out-of-line-assl.md)|Define um tipo de dados derivado que representa a associação de um atributo em uma dimensão de cubo a uma ação ou coluna de estrutura de mineração.|  
|[Tipo de dados CubeBinding &#40;fora de linha&#41; &#40;ASSL&#41;](cubebinding-data-type-out-of-line-assl.md)|Define um tipo de dados primitivo que representa a relação entre um [cubo](../objects/cube-element-assl.md) elemento e um [DataSource](../objects/datasource-element-assl.md) elemento.|  
|[Tipo de dados CubeDimension &#40;ASSL&#41;](cubedimension-data-type-assl.md)|Define um tipo de dados primitivo que representa a relação entre uma dimensão e um cubo.|  
|[Tipo de dados CubeDimensionBinding &#40;ASSL&#41;](dimensionbinding-data-type-assl.md)|Define um tipo de dados derivado que representa a associação de um [dimensão](../objects/dimension-element-assl.md), [medidas](../objects/measure-element-assl.md), ou [MiningModel](../objects/miningmodel-element-assl.md) elemento para uma dimensão de cubo.|  
|[Tipo de dados CubeDimensionPermission &#40;ASSL&#41;](permission-data-type-assl.md)|Define um tipo de dados primitivo que representa as permissões para uma única função em uma dimensão específica em um cubo.|  
|[Tipo de dados CubeHierarchy &#40;ASSL&#41;](hierarchy-data-type-assl.md)|Define um tipo de dados primitivo que representa informações sobre um [hierarquia](../objects/hierarchy-element-assl.md) elemento em um [cubo](../objects/cube-element-assl.md) elemento.|  
|[Tipo de dados DataBlock &#40;ASSL&#41;](datablock-data-type-assl.md)|Define um tipo de dados primitivo que representa uma coleção de blocos de dados usado para armazenar o conteúdo binário de um [ClrAssemblyFile](clrassemblyfile-data-type-assl.md) elemento.|  
|[Tipo de dados DataItem &#40;ASSL&#41;](dataitem-data-type-assl.md)|Define um tipo de dados primitivo que representa a característica relacionada a dados de um item de dados, como, por exemplo, uma coluna ou um atributo.|  
|[Tipo de dados DataMiningMeasureGroupDimension &#40;ASSL&#41;](measuregroupdimension-data-type-assl.md)|Define um tipo de dados derivado que representa a relação entre um grupo de medidas e uma dimensão de mineração de dados.|  
|[Tipo de dados da fonte de dados &#40;ASSL&#41;](datasource-data-type-assl.md)|Define um tipo de dados primitivo abstrato que representa uma fonte de dados em um [banco de dados](../objects/database-element-assl.md) elemento.|  
|[Tipo de dados DataSourceViewBinding &#40;ASSL&#41;](datasourceviewbinding-data-type-assl.md)|Define um tipo de dados derivado que representa uma associação entre uma exibição da fonte de dados e o elemento pai.|  
|[Tipo de dados DegenerateMeasureGroupDimension &#40;ASSL&#41;](degeneratemeasuregroupdimension-data-type-assl.md)|Define um tipo de dados derivado que representa a relação entre uma dimensão de degeneração (ou seja, uma dimensão de fatos) e um grupo de medidas.|  
|[Tipo de dados de dimensão &#40;ASSL&#41;](dimension-data-type-assl.md)|Define um tipo de dados primitivo que representa uma dimensão de banco de dados.|  
|[Tipo de dados DimensionAttribute &#40;ASSL&#41;](dimensionattribute-data-type-assl.md)|Define um tipo de dados primitivo que representa um atributo em uma dimensão.|  
|[Tipo de dados DimensionBinding &#40;ASSL&#41;](dimensionbinding-data-type-assl.md)|Define um tipo de dados derivado que representa a associação entre uma fonte de dados e um [dimensão](../objects/dimension-element-assl.md) elemento.|  
|[Tipo de dados DimensionPermission &#40;ASSL&#41;](permission-data-type-assl.md)|Define um tipo de dados derivado que representa as permissões atribuídas a uma dimensão de banco de dados.|  
|[Tipo de dados DrillThroughAction &#40;ASSL&#41;](drillthroughaction-data-type-assl.md)|Define um tipo de dados derivado que representa uma ação de extração de detalhes.|  
|[Tipo de dados DSVTableBinding &#40;ASSL&#41;](tablebinding-data-type-assl.md)|Define um tipo de dados derivado que representa a associação entre uma tabela e um [DataSourceView](../objects/datasourceview-element-assl.md) elemento.|  
|[Tipo de dados EventColumn &#40;ASSL&#41;](eventcolumn-data-type-assl.md)|Define um tipo de dados primitivo que representa uma coluna de informações a serem capturadas para um [evento](../objects/event-element-assl.md) elemento como parte de um [rastreamento](../objects/trace-element-assl.md) elemento.|  
|[Tipo de dados da hierarquia &#40;ASSL&#41;](hierarchy-data-type-assl.md)|Define um tipo de dados primitivo que representa uma hierarquia em uma dimensão.|  
|[Tipo de dados ImpersonationInfo &#40;ASSL&#41;](impersonationinfo-data-type-assl.md)|Define um tipo de dados primitivo que representa as informações usadas para representar um usuário.|  
|[Tipo de dados IncrementalProcessingNotification &#40;ASSL&#41;](incrementalprocessingnotification-data-type-assl.md)|Define um tipo de dados derivado que representa informações para o [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento sobre uma consulta a ser executada para determinar o andamento do processamento incremental.|  
|[Tipo de dados InheritedBinding &#40;ASSL&#41;](inheritedbinding-data-type-assl.md)|Define um tipo de dados derivado que indica que um [MeasureGroupAttribute](measuregroupattribute-data-type-assl.md) elemento herda suas associações do atributo.|  
|[Tipo de dados ManyToManyMeasureGroupDimension &#40;ASSL&#41;](manytomanymeasuregroupdimension-data-type-assl.md)|Define um tipo de dados derivado que representa a relação entre uma dimensão muitos para muitos e um grupo de medidas.|  
|[Tipo de dados MeasureBinding &#40;ASSL&#41;](measurebinding-data-type-assl.md)|Define um tipo de dados derivado que representa a associação de uma medida ao elemento pai.|  
|[Tipo de dados MeasureGroupAttribute &#40;ASSL&#41;](measuregroupattribute-data-type-assl.md)|Define um tipo de dados primitivo que representa a relação entre um atributo e um grupo de medidas.|  
|[Tipo de dados MeasureGroupBinding &#40;ASSL&#41;](measuregroupbinding-data-type-assl.md)|Define um tipo de dados derivado que representa uma associação a um [MeasureGroup](../objects/group-element-assl.md) elemento.|  
|[Tipo de dados MeasureGroupBinding &#40;fora de linha&#41; &#40;ASSL&#41;](measuregroupbinding-data-type-out-of-line-assl.md)|Define um tipo de dados primitivo que representa uma ligação a um grupo de medidas.|  
|[Tipo de dados MeasureGroupDimension &#40;ASSL&#41;](measuregroupdimension-data-type-assl.md)|Define um tipo de dados primitivo abstrato que representa a relação entre uma dimensão e um grupo de medidas.|  
|[Tipo de dados MeasureGroupDimensionBinding &#40;ASSL&#41;](measuregroupdimensionbinding-data-type-assl.md)|Define um tipo de dados derivado que representa uma associação entre uma dimensão e um grupo de medidas.|  
|[Tipo de dados MeasureGroupHierarchy &#40;ASSL&#41;](measuregrouphierarchy-data-type-assl.md)|Define um tipo de dados primitivo que representa as informações sobre uma hierarquia em um grupo de medidas.|  
|[Tipo de dados MiningModelColumn &#40;ASSL&#41;](miningmodelcolumn-data-type-assl.md)|Define um tipo de dados primitivo que representa informações sobre uma coluna em uma [MiningModel](../objects/miningmodel-element-assl.md) elemento.|  
|[Tipo de dados MiningModelingFlag &#40;ASSL&#41;](miningmodelingflag-data-type-assl.md)|Define um tipo de dados primitivo que representa os sinalizadores de modelagem disponíveis para um [ModelingFlag](../objects/modelingflag-element-assl.md) elemento.|  
|[Tipo de dados MiningStructureColumn &#40;ASSL&#41;](miningstructurecolumn-data-type-assl.md)|Define um tipo de dados primitivo abstrato que representa informações sobre uma coluna em uma [MiningStructure](../objects/miningstructure-element-assl.md) elemento.|  
|[Tipo de dados OlapDataSource &#40;ASSL&#41;](olapdatasource-data-type-assl.md)|Define um tipo de dados derivado que representa um multidimensionais [DataSource](../objects/datasource-element-assl.md) elemento.|  
|[Tipo de dados PartitionBinding &#40;ASSL&#41;](partitionbinding-data-type-assl.md)|Define um tipo de dados derivado que representa uma associação a um [partição](../objects/partition-element-assl.md) elemento.|  
|[Tipo de dados Permission &#40;ASSL&#41;](permission-data-type-assl.md)|Define um tipo de dados primitivo abstrato que representa as informações sobre uma permissão individual.|  
|[Tipo de dados PerspectiveAction &#40;ASSL&#41;](perspectiveaction-data-type-assl.md)|Define um tipo de dados primitivo que representa informações sobre uma ação em um [perspectiva](../objects/perspective-element-assl.md) elemento.|  
|[Tipo de dados PerspectiveAttribute &#40;ASSL&#41;](perspectiveattribute-data-type-assl.md)|Define um tipo de dados primitivo que representa informações sobre um atributo em uma [PerspectiveDimension](perspectivedimension-data-type-assl.md) elemento.|  
|[Tipo de dados PerspectiveCalculation &#40;ASSL&#41;](perspectivecalculation-data-type-assl.md)|Define um tipo de dados primitivo que representa a relação entre um cálculo e um [perspectiva](../objects/perspective-element-assl.md) elemento.|  
|[Tipo de dados PerspectiveDimension &#40;ASSL&#41;](perspectivedimension-data-type-assl.md)|Define um tipo de dados primitivo que representa as informações sobre uma dimensão em uma perspectiva.|  
|[Tipo de dados PerspectiveHierarchy &#40;ASSL&#41;](perspectivehierarchy-data-type-assl.md)|Define um tipo de dados primitivo que representa informações sobre uma hierarquia em uma [PerspectiveDimension](perspectivedimension-data-type-assl.md) elemento.|  
|[Tipo de dados PerspectiveKpi &#40;ASSL&#41;](perspectivekpi-data-type-assl.md)|Define um tipo de dados primitivo que representa informações sobre um indicador chave de desempenho (KPI) em um [perspectiva](../objects/perspective-element-assl.md) elemento.|  
|[Tipo de dados PerspectiveMeasure &#40;ASSL&#41;](perspectivemeasure-data-type-assl.md)|Define um tipo de dados primitivo que representa informações sobre uma medida em um [PerspectiveMeasureGroup](perspectivemeasuregroup-data-type-assl.md) elemento.|  
|[Tipo de dados PerspectiveMeasureGroup &#40;ASSL&#41;](perspectivemeasuregroup-data-type-assl.md)|Define um tipo de dados primitivo que representa informações sobre um grupo de medidas em um [perspectiva](../objects/perspective-element-assl.md) elemento.|  
|[Tipo de dados ProactiveCachingBinding &#40;ASSL&#41;](proactivecachingbinding-data-type-assl.md)|Define um tipo de dados derivado abstrato que representa informações para o [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento sobre as alterações de fonte de dados que requerem a recriação do cache ou sobre o status do processo de recriação.|  
|[Tipo de dados ProactiveCachingIncrementalProcessingBinding &#40;ASSL&#41;](proactivecachingincrementalprocessingbinding-data-type-assl.md)|Define um tipo de dados derivado que representa uma associação para o [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento sobre o status do processo de recriação do cache.|  
|[Tipo de dados ProactiveCachingInheritedBinding &#40;ASSL&#41;](proactivecachinginheritedbinding-data-type-assl.md)|Define um tipo de dados derivado que representa informações para o [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento sobre as alterações da fonte de dados em tabelas e exibições identificadas por meio de ligações de dados existentes que requerem a recriação do cache.|  
|[Tipo de dados ProactiveCachingObjectNotificationBinding &#40;ASSL&#41;](proactivecachingobjectnotificationbinding-data-type-assl.md)|Define um tipo de dados derivado abstrato que representa informações para o [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento sobre alterações de fonte de dados, em tabelas e exibições especificadas ou em tabelas e exibições identificadas por meio de ligações de dados existentes que requerem a recriação do cache.|  
|[Tipo de dados ProactiveCachingQueryBinding &#40;ASSL&#41;](querybinding-data-type-assl.md)|Define um tipo de dados derivado que representa informações para o [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento sobre as alterações da fonte de dados em tabelas e visualizações, identificadas por meio da execução de consultas especificadas que requerem a recriação do cache.|  
|[Tipo de dados ProactiveCachingTablesBinding &#40;ASSL&#41;](proactivecachingtablesbinding-data-type-assl.md)|Define um tipo de dados derivado que representa informações para o [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento sobre as alterações da fonte de dados em tabelas e exibições que requerem a recriação do cache especificadas.|  
|[Tipo de dados PushedDataSource &#40;ASSL&#41;](pusheddatasource-data-type-assl.md)|Define um tipo de dados primitivo que representa uma fonte de dados (como um [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] pacote) usado para "empurrar" dados em um [cubo](../objects/cube-element-assl.md) elemento.|  
|[Tipo de dados QueryBinding &#40;ASSL&#41;](querybinding-data-type-assl.md)|Define um tipo de dados derivado que representa a associação de um [DataSource](../objects/datasource-element-assl.md) elemento com um [QueryDefinition](../properties/querydefinition-element-assl.md) elemento.|  
|[Tipo de dados ReferenceMeasureGroupDimension &#40;ASSL&#41;](referencemeasuregroupdimension-data-type-assl.md)|Define um tipo de dados derivado que representa uma dimensão que está indiretamente relacionada à tabela de fatos por meio de uma dimensão intermediária. Por exemplo, um grupo de medidas Vendas pode fazer referência a uma dimensão Geografia, que está relacionada pela dimensão Cliente.|  
|[Tipo de dados RegularMeasureGroupDimension &#40;ASSL&#41;](regularmeasuregroupdimension-data-type-assl.md)|Define um tipo de dados derivado que representa uma relação regular entre uma dimensão e um grupo de medidas.|  
|[Tipo de dados RelationalDataSource &#40;ASSL&#41;](relationaldatasource-data-type-assl.md)|Define um tipo de dados derivado que representa um [DataSource](../objects/datasource-element-assl.md) elemento com base em uma fonte de dados relacional.|  
|[Tipo de dados ReportAction &#40;ASSL&#41;](reportaction-data-type-assl.md)|Define um tipo de dados derivado que representa uma ação que gera um relatório do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
|[Tipo de dados RowBinding &#40;ASSL&#41;](rowbinding-data-type-assl.md)|Define um tipo de dados derivado que representa uma associação com as linhas de uma tabela em uma [DataSourceView](../objects/datasourceview-element-assl.md) elemento.|  
|[Tipo de dados ScalarMiningStructureColumn &#40;ASSL&#41;](scalarminingstructurecolumn-data-type-assl.md)|Define um tipo de dados derivado que representa um [MiningStructureColumn](miningstructurecolumn-data-type-assl.md) elemento que contém valores escalares, em oposição às tabelas aninhadas associadas a [TableMiningStructureColumn](tableminingstructurecolumn-data-type-assl.md) elemento que contém tabelas aninhadas.|  
|[Tipo de dados StandardAction &#40;ASSL&#41;](standardaction-data-type-assl.md)|Define um tipo de dados derivado que representa qualquer [ação](../objects/action-element-assl.md) elemento diferente de um [DrillThroughAction](drillthroughaction-data-type-assl.md) elemento ou um [ReportAction](reportaction-data-type-assl.md) elemento.|  
|[Tipo de dados TableBinding &#40;ASSL&#41;](tablebinding-data-type-assl.md)|Define um tipo de dados derivado que representa uma associação a uma tabela.|  
|[Tipo de dados TableMiningStructureColumn &#40;ASSL&#41;](tableminingstructurecolumn-data-type-assl.md)|Define um tipo de dados derivado que representa um [MiningStructureColumn](miningstructurecolumn-data-type-assl.md) elemento que contém tabelas aninhadas, em oposição aos valores escalares associados a [ScalarMiningStructureColumn](scalarminingstructurecolumn-data-type-assl.md) elemento que contém valores escalares.|  
|[Tipo de dados TabularBinding &#40;ASSL&#41;](tabularbinding-data-type-assl.md)|Define um tipo de dados derivado abstrato que representa uma associação a um item tabular como uma dimensão de cubo ou tabela.|  
|[Tipo de dados TimeAttributeBinding &#40;ASSL&#41;](timebinding-data-type-assl.md)|Define um tipo de dados derivado que representa uma associação de “espaço reservado” para os itens de dados gerados em uma dimensão de tempo de servidor, como as colunas de chave de um atributo.|  
|[Tipo de dados TimeBinding &#40;ASSL&#41;](timebinding-data-type-assl.md)|Define um tipo de dados derivado que representa uma associação aos períodos de tempo.|  
|[Tipo de dados Translation &#40;ASSL&#41;](translation-data-type-assl.md)|Define um tipo de dados primitivo que representa uma tradução localizada.|  
|[Tipo de dados UserDefinedGroupBinding &#40;ASSL&#41;](userdefinedgroupbinding-data-type-assl.md)|Define um tipo de dados derivado que representa um agrupamento definido pelo usuário para um atributo.|  
  
## <a name="see-also"></a>Consulte também  
 [Hierarquia de elemento XML de linguagem script do Analysis Services &#40;ASSL&#41;](../analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  