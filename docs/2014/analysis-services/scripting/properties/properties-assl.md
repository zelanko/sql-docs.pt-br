---
title: Propriedades (ASSL) | Microsoft Docs
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
- properties [Analysis Services Scripting Language]
- Analysis Services Scripting Language, properties
- ASSL, properties
ms.assetid: 9a38cdc9-a210-421a-90e9-6391876765fa
caps.latest.revision: 21
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8a000f4f4c9a73698f04a0bd88882db55b8661e1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37173497"
---
# <a name="properties-assl"></a>Properties (ASSL)
  Esta seção de referência contém informações de sintaxe e uso de cada elemento que age como uma propriedade de objeto no esquema ASSL (Analysis Services Scripting Language).  
  
 Embora o esquema ASSL contenha somente elementos XML, do ponto de vista do desenvolvedor, os elementos descritos nessa seção correspondem a propriedades que descrevem objetos.  
  
 As propriedades são elementos do nível folha no esquema ASSL e não têm elementos filho ou elementos que correspondem a propriedades próprias.  
  
 Em alguns casos, um elemento do nível folha no esquema que pode parecer uma propriedade é classificado como um objeto porque o tipo de elemento é um tipo de objeto. Por exemplo, a `Source` de um objeto `Dimension` é de tipo `DimensionBinding`.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Elemento|Description|  
|-------------|-----------------|  
|[Acessar o elemento &#40;ASSL&#41;](access-element-assl.md)|Indica o nível de acesso concedido a um [CellPermission](../objects/cellpermission-element-assl.md) elemento.|  
|[Elemento de conta &#40;ImpersonationInfo&#41; &#40;ASSL&#41;](account-element-impersonationinfo-assl.md)|Contém o nome da conta de usuário para o [ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md) tipo de dados.|  
|[Elemento AccountType &#40;ASSL&#41;](accounttype-element-assl.md)|Contém o nome de um tipo de conta definido em uma [banco de dados](../objects/database-element-assl.md) elemento.|  
|[Elemento ActionID &#40;ASSL&#41;](id-element-assl.md)|Contém o nome de um [ação](../objects/action-element-assl.md) elemento definido em um [cubo](../objects/cube-element-assl.md) elemento que está disponível em um [perspectiva](../objects/perspective-element-assl.md) elemento como um [PerspectiveAction](../data-type/action-data-type-assl.md) elemento.|  
|[Elemento Administer &#40;ASSL&#41;](administer-element-assl.md)|Indica se a permissão associada inclui o direito de administrar um elemento `Database`.|  
|[Elemento AggregateFunction &#40;ASSL&#41;](aggregatefunction-element-assl.md)|Define o tipo de função de agregação usado por um [medida](../objects/measure-element-assl.md) elemento.|  
|[Elemento AggregationDesignID &#40;ASSL&#41;](aggregationdesignid-element-assl.md)|Identifica o [AggregationDesign](../objects/aggregationdesign-element-assl.md) elemento associado a [partição](../objects/partition-element-assl.md) elemento.|  
|[Elemento AggregationFunction &#40;ASSL&#41;](aggregationfunction-element-assl.md)|Contém a função de agregação a ser usada para o tipo de conta.|  
|[Elemento AggregationID &#40;ASSL&#41;](aggregationid-element-assl.md)|Identifica a definição de agregação do elemento `AggregationDesign` usado para criar a instância de agregação.|  
|[Elemento AggregationInstanceSource &#40;ASSL&#41;](aggregationinstancesource-element-assl.md)|Identifica a fonte de dados para instâncias de agregação definidas pelo usuário associadas a um elemento `Partition`.|  
|[Elemento AggregationPrefix &#40;ASSL&#41;](aggregationprefix-element-assl.md)|Define o prefixo comum a ser usado para nomes de agregação no elemento pai associado.|  
|[Elemento AggregationStorage &#40;ASSL&#41;](aggregationstorage-element-assl.md)|Identifica o método de armazenamento para agregações.|  
|[Elemento AggregationType &#40;ASSL&#41;](aggregationtype-element-assl.md)|Define o tipo de agregação armazenado pelo elemento `Partition`.|  
|[Elemento AggregationUsage &#40;ASSL&#41;](aggregationusage-element-assl.md)|Controles como o Designer de agregação na [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] projeta agregações.|  
|[Elemento Algorithm &#40;ASSL&#41;](algorithm-element-assl.md)|Define o algoritmo usado por um [MiningModel](../objects/miningmodel-element-assl.md) elemento.|  
|[Elemento alias &#40;ASSL&#41;](alias-element-assl.md)|Define um alias para um [conta](../objects/account-element-assl.md) elemento.|  
|[Elemento AllMemberAggregationUsage &#40;ASSL&#41;](allmemberaggregationusage-element-assl.md)|Controla como o Designer de Agregação no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] projeta agregações.|  
|[Elemento AllMemberName &#40;ASSL&#41;](name-element-assl.md)|Contém a legenda no idioma padrão para todos os membros de um [hierarquia](../objects/hierarchy-element-assl.md) elemento.|  
|[Elemento AllowBrowsing &#40;ASSL&#41;](allowbrowsing-element-assl.md)|Define se os membros de um [função](../objects/role-element-assl.md) elemento têm permissão de navegação um `MiningModel` elemento.|  
|[Elemento AllowDrillThrough &#40;ASSL&#41;](allowdrillthrough-element-assl.md)|Determina se a extração de detalhes é permitida no elemento pai.|  
|[Elemento AllowDuplicateNames &#40;ASSL&#41;](allowduplicatenames-element-assl.md)|Determina se são permitidos nomes duplicados em um elemento `Hierarchy`.|  
|[Elemento AllowedSet &#40;ASSL&#41;](allowedset-element-assl.md)|Contém uma expressão de conjunto que define o conjunto de permissões permitidas para um elemento `Role` em um atributo.|  
|[Elemento de aplicativo &#40;ASSL&#41;](application-element-assl.md)|Identifica o aplicativo associado a um elemento `Action`.|  
|[Elemento AssociatedMeasureGroupID &#40;ASSL&#41;](measuregroupid-element-assl.md)|Contém o identificador (ID) da [MeasureGroup](../objects/group-element-assl.md) elemento associado a um [CalculationProperty](../objects/calculationproperty-element-assl.md) elemento ou uma [Kpi](../objects/kpi-element-assl.md) elemento.|  
|[Elemento AttributeAllMemberName &#40;ASSL&#41;](attributeallmembername-element-assl.md)|Contém a legenda, no idioma padrão, do membro All da dimensão.|  
|[Elemento AttributeHierarchyDisplayFolder &#40;ASSL&#41;](displayfolder-element-assl.md)|Identifica a pasta na qual deve ser exibida a hierarquia de atributo associada.|  
|[Elemento AttributeHierarchyEnabled &#40;ASSL&#41;](enabled-element-assl.md)|Determina se uma hierarquia de atributo está habilitada para o atributo.|  
|[Elemento AttributeHierarchyOptimizedState &#40;ASSL&#41;](state-element-assl.md)|Determina o nível de otimização aplicado à hierarquia de atributo.|  
|[Elemento AttributeHierarchyOrdered &#40;ASSL&#41;](attributehierarchyordered-element-assl.md)|Determina se a hierarquia de atributo associada está ordenada.|  
|[Elemento AttributeHierarchyVisible &#40;ASSL&#41;](visible-element-assl.md)|Determina se a hierarquia de atributo é visível a aplicativos cliente.|  
|[Elemento AttributeID &#40;ASSL&#41;](attributeid-element-assl.md)|Contém a ID do atributo associado ao elemento pai.|  
|[Auditar o elemento &#40;ASSL&#41;](audit-element-assl.md)|Especifica que um [rastreamento](../objects/trace-element-assl.md) elemento não pode descartar quaisquer eventos, mesmo se isso resulta em desempenho degradado no servidor.|  
|[Elemento AutoRestart &#40;ASSL&#41;](autorestart-element-assl.md)|Determina se um elemento `Trace` deve ser reiniciado automaticamente caso o serviço do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] pare e reinicie.|  
|[Elemento BackColor &#40;ASSL&#41;](backcolor-element-assl.md)|Descreve características de exibição relacionadas a cores do elemento pai.|  
|[Elemento CacheMode &#40;ASSL&#41;](cachemode-element-assl.md)|Determina o mecanismo de cache usado por treinar dados recuperados durante o processamento de uma estrutura de mineração.|  
|[Elemento CalculationReference &#40;ASSL&#41;](calculationreference-element-assl.md)|Contém o nome do conjunto nomeado ou da célula calculada mencionado pelo elemento `CalculationProperty`.|  
|[Elemento CalculationType &#40;ASSL&#41;](calculationtype-element-assl.md)|Descreve o tipo de cálculo definido no elemento `CalculationProperty` associado.|  
|[Elemento CalendarEndDate &#40;ASSL&#41;](calendarenddate-element-assl.md)|Define a data de término do período de calendário para um [TimeBinding](../data-type/binding-data-type-assl.md) elemento.|  
|[Elemento CalendarLanguage &#40;ASSL&#41;](language-element-assl.md)|Define a linguagem de calendário usada para o elemento `TimeBinding`.|  
|[Elemento CalendarStartDate &#40;ASSL&#41;](calendarstartdate-element-assl.md)|Define a data de início do período de calendário do elemento `TimeBinding`.|  
|[Elemento de legenda &#40;ASSL&#41;](caption-element-assl.md)|Contém a legenda do elemento pai associado.|  
|[Elemento CaptionIsMdx &#40;ASSL&#41;](captionismdx-element-assl.md)|Define se a legenda do elemento `Action` é uma linguagem MDX.|  
|[Elemento Cardinality &#40;ASSL&#41;](cardinality-element-assl.md)|Indica a cardinalidade da relação descrita por um [AttributeRelationship](../objects/attributerelationship-element-assl.md) ou [RegularMeasureGroupDimension](../data-type/dimension-data-type-assl.md).|  
|[Elemento CaseCubeDimensionID &#40;ASSL&#41;](dimensionid-element-assl.md)|Contém a ID da dimensão de cubo que relaciona a dimensão de mineração de dados ao grupo de medidas.|  
|[Elemento ClassifiedColumnID &#40;ASSL&#41;](classifiedcolumnid-element-assl.md)|Contém a ID de uma coluna relacionada classificada pelo [ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md) elemento.|  
|[Elemento de agrupamento &#40;ASSL&#41;](collation-element-assl.md)|Determina o agrupamento usado pelo elemento pai.|  
|[Elemento ColumnID &#40;ColumnBinding&#41; &#40;ASSL&#41;](columnid-element-columnbinding-assl.md)|Contém a ID da coluna na tabela à qual o item de dados está associado.|  
|[Elemento ColumnID &#40;EventColumn&#41; &#40;ASSL&#41;](columnid-element-eventcolumn-assl.md)|Contém a ID da coluna de informações a serem capturadas para um evento como parte de um elemento `Trace`.|  
|[Elemento de condição &#40;ASSL&#41;](condition-element-assl.md)|Contém uma linguagem MDX que determina se o elemento pai `Action` se aplica ao destino.|  
|[Elemento ConnectionString &#40;ASSL&#41;](connectionstring-element-assl.md)|Contém a cadeia de conexão criptografada para um [fonte de dados](../objects/datasource-element-assl.md) elemento.|  
|[Elemento ConnectionStringSecurity &#40;ASSL&#41;](connectionstringsecurity-element-assl.md)|Especifica se a senha do usuário é tirada da cadeia de conexão de fonte de dados para propósitos de segurança.|  
|[Elemento de conteúdo &#40;ASSL&#41;](content-element-assl.md)|Descreve o conteúdo da coluna na [MiningStructure](../objects/miningstructure-element-assl.md) elemento.|  
|[Elemento CreatedTimestamp &#40;ASSL&#41;](createdtimestamp-element-assl.md)|Contém o carimbo de data e hora de criação somente leitura do elemento pai.|  
|[Elemento CubeDimensionID &#40;ASSL&#41;](cubedimensionid-element-assl.md)|Identifica o [CubeDimension](../data-type/cubedimension-data-type-assl.md) associado ao elemento pai do elemento.|  
|[Elemento CubeID &#40;ASSL&#41;](cubeid-element-assl.md)|Identifica o `Cube` elemento associado a um [associação](../data-type/binding-data-type-assl.md) elemento.|  
|[Elemento CurrentStorageMode &#40;ASSL&#41;](storagemode-element-assl.md)|Determina o modo de armazenamento atual para o elemento pai.|  
|[Elemento CurrentTimeMember &#40;ASSL&#41;](../objects/member-element-assl.md)|Define o membro atual de uma dimensão de tempo associada a um elemento `Kpi`.|  
|[Elemento DataAggregation &#40;ASSL&#41;](../objects/aggregation-element-assl.md)|Determina se a instância pode agregar dados persistidos ou dados armazenados em cache para o elemento `MeasureGroup`.|  
|[Elemento DatabaseID &#40;ASSL&#41;](databaseid-element-assl.md)|Identifica o elemento `Database` associado a um elemento `Binding` fora de linha.|  
|[Elemento DataSize &#40;ASSL&#41;](datasize-element-assl.md)|Contém o tamanho em bytes de um [DataItem](../data-type/dataitem-data-type-assl.md) elemento.|  
|[Elemento DataSourceID &#40;ASSL&#41;](datasourceid-element-assl.md)|Identifica o elemento `DataSource` associado ao elemento pai.|  
|[Elemento DataSourceImpersonationInfo &#40;ASSL&#41;](impersonationinfo-element-assl.md)|Contém as informações usadas para determinar o comportamento de representação ao conectar à fonte de dados para um elemento `Database`.|  
|[Elemento DataSourceViewID &#40;ASSL&#41;](datasourceviewid-element-assl.md)|Identifica o [DataSourceView](../objects/datasourceview-element-assl.md) elemento associado a `Binding` elemento pai.|  
|[Elemento de tipo de dados &#40;ASSL&#41;](datatype-element-assl.md)|Define o tipo de dados do elemento associado.|  
|[Elemento DbSchemaName &#40;ASSL&#41;](dbschemaname-element-assl.md)|Contém o nome do esquema usado pelo elemento pai na tabela identificada pelo [DbTableName](dbtablename-element-assl.md) elemento.|  
|[Elemento DbTableName &#40;ASSL&#41;](dbtablename-element-assl.md)|Contém o nome da tabela à qual o elemento pai está associado.|  
|[Padrão do elemento &#40;ASSL&#41;](default-element-assl.md)|Determina se o elemento `DrillThroughAction` é a ação de extração de detalhes padrão.|  
|[Elemento DefaultMeasure &#40;ASSL&#41;](defaultmeasure-element-assl.md)|Contém uma expressão de linguagem MDX que define a medida padrão para um elemento `Cube` ou `Perspective`.|  
|[Elemento DefaultMember &#40;ASSL&#41;](defaultmember-element-assl.md)|Contém uma expressão MDX que identifica o membro padrão do elemento pai.|  
|[Elemento DefaultScript &#40;ASSL&#41;](defaultscript-element-assl.md)|Identifica o padrão [MdxScript](../objects/mdxscript-element-assl.md) elemento o [MdxScripts](../collections/mdxscripts-element-assl.md) coleção.|  
|[Elemento DefaultValue &#40;ASSL&#41;](value-element-assl.md)|Contém o valor padrão de somente leitura associado [ServerProperty](../objects/serverproperty-element-assl.md) elemento.|  
|[Elemento DeniedSet &#40;ASSL&#41;](deniedset-element-assl.md)|Contém uma expressão de conjunto que define a lista de permissões negadas no atributo associado.|  
|[Elemento DependsOnDimensionID &#40;ASSL&#41;](dependsondimensionid-element-assl.md)|Contém a ID de outra dimensão da qual a dimensão pai depende.|  
|[Elemento Description &#40;ASSL&#41;](description-element-assl.md)|Contém a descrição do elemento pai.|  
|[Elemento DimensionID &#40;ASSL&#41;](dimensionid-element-assl.md)|Contém a ID da dimensão.|  
|[Elemento DiscretizationBucketCount &#40;ASSL&#41;](discretizationbucketcount-element-assl.md)|Contém o número de recipientes nos quais são diferenciados.|  
|[Elemento DiscretizationMethod &#40;ASSL&#41;](discretizationmethod-element-assl.md)|Define o método a ser usado para diferenciação.|  
|[Elemento DisplayFlag &#40;ASSL&#41;](displayflag-element-assl.md)|Contém uma dica somente leitura que indica se os componentes de interface de usuário devem exibir o elemento `ServerProperty` associado.|  
|[Elemento DisplayFolder &#40;ASSL&#41;](displayfolder-element-assl.md)|Especifica a pasta na qual listar o elemento pai. Os aplicativos [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para desenvolvedores e administradores podem oferecer suporte ao uso de pastas de exibição para categorizar vários elementos visualmente.|  
|[Elemento Distribution &#40;ASSL&#41;](distribution-element-assl.md)|Contém um valor específico do provedor que descreve como os valores escalares são distribuídos dentro de uma coluna de um elemento `MiningStructure`.|  
|[Elemento Edition &#40;ASSL&#41;](edition-element-assl.md)|Contém a edição somente leitura da instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] representado pelo [Server](../objects/server-element-assl.md) elemento.|  
|[Habilitado o elemento &#40;ASSL&#41;](enabled-element-assl.md)|Indica se o elemento pai está habilitado.|  
|[Elemento EndOfData &#40;ASSL&#41;](../objects/data-element-assl.md)|Indica o final dos dados recebidos de um [PushedDataSource](../data-type/datasource-data-type-assl.md) elemento.|  
|[Elemento EstimatedCount &#40;ASSL&#41;](estimatedcount-element-assl.md)|Contém o número estimado de membros para um atributo.|  
|[Elemento EstimatedPerformanceGain &#40;ASSL&#41;](estimatedperformancegain-element-assl.md)|Contém a porcentagem somente leitura de ganho de desempenho estimado para a partição.|  
|[Elemento EstimatedRows &#40;ASSL&#41;](estimatedrows-element-assl.md)|Contém o número estimado de linhas representadas pelo elemento pai.|  
|[Elemento EstimatedSize &#40;ASSL&#41;](estimatedsize-element-assl.md)|Contém o tamanho estimado somente leitura, em bytes, do elemento pai.|  
|[Elemento EventID &#40;ASSL&#41;](eventid-element-assl.md)|Identifica exclusivamente um [evento](../objects/event-element-assl.md) elemento que deve ser capturado como parte de um `Trace` elemento.|  
|[Elemento de expressão &#40;ASSL&#41;](expression-element-assl.md)|Contém uma expressão MDX que define o conteúdo do elemento pai.|  
|[Elemento Filter &#40;associação&#41; &#40;ASSL&#41;](filter-element-binding-assl.md)|Contém uma expressão MDX que filtra o conteúdo do elemento pai.|  
|[Elemento Filter &#40;rastreamento&#41; &#40;ASSL&#41;](filter-element-trace-assl.md)|Contém um fragmento de documento XML que descreve o filtro `Trace`.|  
|[Elemento FirstDayOfWeek &#40;ASSL&#41;](firstdayofweek-element-assl.md)|Define o primeiro dia da semana para um elemento `TimeBinding`.|  
|[Elemento FiscalFirstDayOfMonth &#40;ASSL&#41;](fiscalfirstdayofmonth-element-assl.md)|Define o primeiro dia do mês fiscal para um elemento `TimeBinding`.|  
|[Elemento FiscalFirstMonth &#40;ASSL&#41;](fiscalfirstmonth-element-assl.md)|Define o primeiro mês do período fiscal para um elemento `TimeBinding`.|  
|[Elemento FiscalYearName &#40;ASSL&#41;](fiscalyearname-element-assl.md)|Define a convenção de nomenclatura para o nome do ano fiscal para um elemento `TimeBinding`.|  
|[Elemento FontFlags &#40;ASSL&#41;](fontflags-element-assl.md)|Descreve características de exibição relacionadas à fonte do elemento pai `CalculationProperty` ou `Measure`.|  
|[Elemento FontName &#40;ASSL&#41;](fontname-element-assl.md)|Descreve características de exibição relacionadas à fonte do elemento pai `CalculationProperty` ou `Measure`.|  
|[Elemento FontSize &#40;ASSL&#41;](fontsize-element-assl.md)|Descreve características de exibição relacionadas à fonte do elemento pai `CalculationProperty` ou `Measure`.|  
|[Elemento ForceRebuildInterval &#40;ASSL&#41;](forcerebuildinterval-element-assl.md)|Determina a quantidade de tempo, começando quando uma imagem nova MOLAP (OLAP multidimensional) se torna disponível, depois da qual a imagem MOLAP começa incondicionalmente.|  
|[Elemento ForeColor &#40;ASSL&#41;](forecolor-element-assl.md)|Descreve características de exibição relacionadas à cor do elemento pai `CalculationProperty` ou `Measure`.|  
|[Formatar o elemento &#40;ASSL&#41;](format-element-assl.md)|Contém o formato obrigatório do elemento `DataItem`.|  
|[Elemento FormatString &#40;ASSL&#41;](formatstring-element-assl.md)|Descreve o formato de exibição para um elemento `CalculationProperty` ou um elemento `Measure`.|  
|[Elemento Goal &#40;ASSL&#41;](goal-element-assl.md)|Identifica a meta desejada em um elemento `Kpi`.|  
|[Elemento GranularityAttributeID &#40;ASSL&#41;](granularityattributeid-element-assl.md)|Contém a ID do atributo associado ao pai [MeasureGroupAttributeBinding](../data-type/measuregroupattributebinding-data-type-out-of-line-assl.md) tipo de dados.|  
|[Elemento HideMemberIf &#40;ASSL&#41;](hidememberif-element-assl.md)|Indica se, e quando, um membro em um nível ficará oculto pelos aplicativos cliente.|  
|[Elemento HierarchyID &#40;ASSL&#41;](hierarchyid-element-assl.md)|Contém a ID para um [CubeHierarchy](../data-type/hierarchy-data-type-assl.md), [MeasureGroupHierarchy](../data-type/measuregrouphierarchy-data-type-assl.md), ou [PerspectiveHierarchy](../data-type/perspectivehierarchy-data-type-assl.md) elemento.|  
|[Elemento HierarchyUniqueNameStyle &#40;ASSL&#41;](hierarchyuniquenamestyle-element-assl.md)|Determina como nomes exclusivos são gerados para hierarquias que estão contidas em `CubeDimension`.|  
|[ID do elemento &#40;ASSL&#41;](id-element-assl.md)|Contém a ID exclusiva do elemento pai.|  
|[Elemento IgnoreUnrelatedDimensions &#40;ASSL&#41;](../collections/dimensions-element-assl.md)|Determina se as dimensão não relacionadas são forçadas para seu nível superior quando os membros das dimensões que não estão relacionados ao grupo de medidas são incluídos em uma consulta.|  
|[Elemento ImpersonationInfo &#40;ASSL&#41;](impersonationinfo-element-assl.md)|Contém as informações usadas para determinar o comportamento de personificação ao acessar ou executar um assembly.|  
|[Elemento ImpersonationInfoSecurity &#40;ASSL&#41;](impersonationinfosecurity-element-assl.md)|Contém um valor somente leitura que indica se alguma alteração foi feita nas credenciais de segurança fornecidas no tipo de dados `ImpersonationInfo`.|  
|[Elemento ImpersonationMode &#40;ASSL&#41;](impersonationmode-element-assl.md)|Contém um valor que indica o método de representação para elementos que são derivados do tipo de dados `ImpersonationInfo`.|  
|[Elemento InstanceSelection &#40;ASSL&#41;](instanceselection-element-assl.md)|Fornece uma dica para aplicativos cliente para sugerir como uma lista de itens deve ser exibida, com base no número esperado de itens na lista.|  
|[Elemento IntermediateCubeDimensionID &#40;ASSL&#41;](intermediatecubedimensionid-element-assl.md)|Contém a ID da dimensão que relaciona uma dimensão de referência a um grupo de medidas.|  
|[Elemento IntermediateGranularityAttributeID &#40;ASSL&#41;](intermediategranularityattributeid-element-assl.md)|Contém a ID do atributo de granularidade das dimensões de cubo intermediárias usadas para relacionar uma dimensão de referência com uma dimensão intermediária.|  
|[Elemento InvalidXmlCharacters &#40;ASSL&#41;](invalidxmlcharacters-element-assl.md)|Especifica o método de manipulação de caracteres XML nos dados de origem que não são válidos.|  
|[Elemento Invocation &#40;ASSL&#41;](invocation-element-assl.md)|Especifica como uma `Action` deve ser chamada.|  
|[Elemento IsAggregatable &#40;ASSL&#41;](isaggregatable-element-assl.md)|Especifica se os valores de [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md) elemento pode ser agregado.|  
|[Elemento IsKey &#40;ASSL&#41;](iskey-element-assl.md)|Indica se a coluna fornece a chave para o elemento `MiningStructure`.|  
|[Elemento Isolation &#40;ASSL&#41;](isolation-element-assl.md)|Indica o nível de isolamento para um elemento que é derivado de [fonte de dados](../data-type/datasource-data-type-assl.md) tipo de dados.|  
|[Elemento KeyDuplicate &#40;ASSL&#41;](keyduplicate-element-assl.md)|Determina como o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] manipula um erro de chave duplicada, caso seja encontrado algum durante o processamento.|  
|[Elemento KeyErrorAction &#40;ASSL&#41;](keyerroraction-element-assl.md)|Especifica a ação do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] a ser executada quando ocorre um erro em uma chave.|  
|[Elemento KeyErrorLimit &#40;ASSL&#41;](keyerrorlimit-element-assl.md)|Contém o número de erros aceitáveis durante o processamento.|  
|[Elemento KeyErrorLimitAction &#40;ASSL&#41;](keyerrorlimitaction-element-assl.md)|Especifica a ação que [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] toma quando a contagem de erros de chave especificada na [KeyErrorLimit](keyerrorlimit-element-assl.md) elemento for atingido.|  
|[Elemento KeyErrorLogFile &#40;ASSL&#41;](../objects/file-element-assl.md)|Contém o nome do arquivo para registrar erros de processamento.|  
|[Elemento KeyNotFound &#40;ASSL&#41;](keynotfound-element-assl.md)|Especifica como o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] responde quando encontra um erro de integridade referencial.|  
|[Elemento KeyUniquenessGuarantee &#40;ASSL&#41;](keyuniquenessguarantee-element-assl.md)|Indica se a relação entre a chave de atributo e seu nome, e a relação com os atributos relacionados, é válida.|  
|[Elemento KpiID &#40;ASSL&#41;](kpiid-element-assl.md)|Contém uma ID que associa um elemento `Kpi` a um elemento `Perspective`.|  
|[Elemento de linguagem &#40;ASSL&#41;](language-element-assl.md)|Contém o identificador de idioma do elemento pai.|  
|[Elemento LastProcessed &#40;ASSL&#41;](lastprocessed-element-assl.md)|Contém o carimbo de data e hora somente leitura que indica quando o banco de dados que contém o elemento pai foi processado por último.|  
|[Elemento LastSchemaUpdate &#40;ASSL&#41;](lastschemaupdate-element-assl.md)|Contém o carimbo de data e hora de atualização de metadados somente leitura do elemento pai.|  
|[Elemento LastUpdate &#40;ASSL&#41;](lastupdate-element-assl.md)|Contém um carimbo de data e hora somente leitura que indica a última vez em que o elemento `Database` associado ou qualquer objeto principal contido no banco de dados foi alterado.|  
|[Elemento Latency &#40;ASSL&#41;](latency-element-assl.md)|Define o "período de avaliação" entre a primeira notificação e o momento em que as imagens MOLAP são destruídas.|  
|[Elemento LogFileAppend &#40;ASSL&#41;](logfileappend-element-assl.md)|Determina se o elemento `Trace` anexa sua saída de log ao arquivo de log existente ou a substitui.|  
|[Elemento LogFileName &#40;ASSL&#41;](logfilename-element-assl.md)|Contém o nome do arquivo de log do elemento `Trace`.|  
|[Elemento LogFileRollover &#40;ASSL&#41;](logfilerollover-element-assl.md)|Especifica se o registro de `Trace` saída deve captar um novo arquivo ou deve parar quando o arquivo de log máximo tamanho especificado em [LogFileSize](logfilesize-element-assl.md) for atingido.|  
|[Elemento LogFileSize &#40;ASSL&#41;](logfilesize-element-assl.md)|Especifica o tamanho máximo de arquivo de log em megabytes.|  
|[Elemento ManagedProvider &#40;ASSL&#41;](managedprovider-element-assl.md)|Contém o nome do provedor gerenciado usado por um elemento derivado do tipo de dados `DataSource`.|  
|[Elemento ManufacturingExtraMonthQuarter &#40;ASSL&#41;](manufacturingextramonthquarter-element-assl.md)|Define o mês do período de fabricação para o qual um mês extra é atribuído para um elemento `TimeBinding`.|  
|[Elemento ManufacturingFirstMonth &#40;ASSL&#41;](manufacturingfirstmonth-element-assl.md)|Define o primeiro mês de fabricação para um elemento `TimeBinding`.|  
|[Elemento ManufacturingFirstWeekOfMonth &#40;ASSL&#41;](manufacturingfirstweekofmonth-element-assl.md)|Define a primeira semana do mês de fabricação para um elemento `TimeBinding`.|  
|[Elemento MasterDatasourceID &#40;ASSL&#41;](masterdatasourceid-element-assl.md)|Contém a ID da fonte de dados mestre para um elemento `Database`.|  
|[Elemento Materialization &#40;ASSL&#41;](materialization-element-assl.md)|Indica o tipo de relação entre o grupo de medidas e a dimensão de referência.|  
|[Elemento MaxActiveConnections &#40;ASSL&#41;](maxactiveconnections-element-assl.md)|Contém o número máximo de conexões simultâneas permitido por um elemento derivado do tipo de dados `DataSource`.|  
|[Elemento MdxMissingMemberMode &#40;ASSL&#41;](mdxmissingmembermode-element-assl.md)|Determina como são manipulados membros ausentes para linguagens MDX.|  
|[Elemento MeasureExpression &#40;ASSL&#41;](measureexpression-element-assl.md)|Contém a linguagem MDX que define uma medida.|  
|[Elemento MeasureGroupID &#40;ASSL&#41;](measuregroupid-element-assl.md)|Associa um `MeasureGroup` ao elemento pai, associação ou associação fora de linha.|  
|[Elemento MeasureID &#40;ASSL&#41;](measureid-element-assl.md)|Associa um elemento `Measure` com o elemento pai.|  
|[Elemento Measurequalification &#40;ASSL&#41;](measurequalificaton-element-assl.md)|Determina se um prefixo é aplicado em medidas no `MeasureGroup`.|  
|[Elemento MemberNamesUnique &#40;ASSL&#41;](membernamesunique-element-assl.md)|Determina se os nomes de membros no elemento pai devem ser exclusivos.|  
|[Elemento MemberUniqueNameStyle &#40;ASSL&#41;](memberuniquenamestyle-element-assl.md)|Determina como são gerados nomes exclusivos para membros de hierarquias contidas no elemento `CubeDimension`.|  
|[Elemento MembersWithData &#40;ASSL&#41;](memberswithdata-element-assl.md)|Determina se devem ou não exibir membros de dados para membros não folha no atributo pai.|  
|[Elemento MembersWithDataCaption &#40;ASSL&#41;](memberswithdatacaption-element-assl.md)|Fornece uma cadeia de caracteres de modelo usada para criar legendas para os membros de dados gerados pelo sistema.|  
|[Elemento MimeType &#40;ASSL&#41;](mimetype-element-assl.md)|Contém o tipo MIME (Multipurpose Internet Mail Extensions), se aplicável, dos dados representados pelo elemento pai `DataItem`.|  
|[Elemento MiningModelID &#40;ASSL&#41;](miningmodelid-element-assl.md)|Associa um modelo de mineração com uma dimensão de mineração de dados.|  
|[Nomeie o elemento &#40;ASSL&#41;](name-element-assl.md)|Contém o nome do elemento pai.|  
|[Elemento NamingTemplate &#40;ASSL&#41;](namingtemplate-element-assl.md)|Define como os níveis construídos a partir do elemento pai `DimensionAttribute` são nomeados em uma hierarquia pai-filho.|  
|[Elemento NonEmptyBehavior &#40;ASSL&#41;](nonemptybehavior-element-assl.md)|Determina o comportamento não vazio associado ao pai do elemento `CalculationProperty`.|  
|[Elemento NotificationTechnique &#40;ASSL&#41;](notificationtechnique-element-assl.md)|Especifica se [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou um aplicativo cliente externo processa as notificações.|  
|[Elemento NullKeyConvertedToUnknown &#40;ASSL&#41;](nullkeyconvertedtounknown-element-assl.md)|Especifica a ação a ser tomada quando um erro de conversão nulo é encontrado.|  
|[Elemento NullKeyNotAllowed &#40;ASSL&#41;](nullkeynotallowed-element-assl.md)|Determina como o mecanismo de processamento do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] manipula um erro de chave nula encontrado durante o processamento.|  
|[Elemento NullProcessing &#40;ASSL&#41;](nullprocessing-element-assl.md)|Define como valores nulos são processados.|  
|[Elemento OnlineMode &#40;ASSL&#41;](onlinemode-element-assl.md)|Especifica se o banco de dados volta a ficar online imediatamente quando a recriação do cache é iniciada ou somente quando a recriação do cache é concluída.|  
|[Elemento OptimizedState &#40;ASSL&#41;](state-element-assl.md)|Determina o nível de otimização aplicado à hierarquia.|  
|[Elemento optionality &#40;ASSL&#41;](optionality-element-assl.md)|Indica as opções dos membros para um elemento `AttributeRelationship`.|  
|[Elemento OrderBy &#40;ASSL&#41;](orderby-element-assl.md)|Descreve como ordenar os membros contidos no atributo.|  
|[Elemento OrderByAttributeID &#40;ASSL&#41;](orderbyattributeid-element-assl.md)|Identifica outro atributo pelo qual ordenar os membros de [dimensão](../data-type/dimensionattribute-data-type-assl.md) atributo.|  
|[Elemento ordinal &#40;ASSL&#41;](ordinal-element-assl.md)|Indica o número ordinal a ser associado às coleções como chaves e traduções.|  
|[Elemento OverrideBehavior &#40;ASSL&#41;](overridebehavior-element-assl.md)|Indica o comportamento substituto da relação descrita por um elemento `AttributeRelationship`.|  
|[Elemento PartitionID &#40;ASSL&#41;](partitionid-element-assl.md)|Associa um elemento `Partition` ao elemento pai, associação ou associação fora de linha.|  
|[Elemento Password &#40;ASSL&#41;](password-element-assl.md)|Contém a senha da conta de usuário para o elemento `ImpersonationInfo`.|  
|[Elemento de caminho &#40;ASSL&#41;](path-element-assl.md)|Contém o caminho, conforme fornecido por uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], de um relatório usado pelo [ReportAction](../data-type/reportaction-data-type-assl.md) elemento.|  
|[Elemento PendingValue &#40;ASSL&#41;](pendingvalue-element-assl.md)|Contém o valor pendente somente leitura do elemento `ServerProperty` associado.|  
|[Elemento PermissionSet &#40;ASSL&#41;](permissionset-element-assl.md)|Identifica o conjunto de permissões associado com um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] assembly do .NET Framework.|  
|[Elemento Persistence &#40;ASSL&#41;](persistence-element-assl.md)|Determina quais partes dos dados de origem ligados são dinâmicos e são verificados quanto à atualizações usando a frequência especificada pelo [RefreshPolicy](refreshpolicy-element-assl.md) elemento.|  
|[Processar o elemento &#40;ASSL&#41;](process-element-assl.md)|Determina se um usuário pode processar o proprietário do elemento pai.|  
|[Elemento ProcessingMode &#40;ASSL&#41;](processingmode-element-assl.md)|Indica se a instância deve fazer indexação e agregação durante ou após o processamento.|  
|[Elemento ProcessingPriority &#40;ASSL&#41;](processingpriority-element-assl.md)|Determina a prioridade de processamento do objeto pai durante as operações em segundo plano, como agregações lentas, indexação ou cluster.|  
|[Elemento ProcessingQuery &#40;ASSL&#41;](query-element-assl.md)|Contém o texto parametrizado da consulta a ser executado para notificação do status de processamento incremental.|  
|[Elemento ProductName &#40;ASSL&#41;](productname-element-assl.md)|Contém o nome de produto somente leitura da instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] associada a um elemento `Server`.|  
|[Elemento de consulta &#40;ASSL&#41;](query-element-assl.md)|Contém o texto da consulta a ser executado para a notificação.|  
|[Elemento QueryDefinition &#40;ASSL&#41;](querydefinition-element-assl.md)|Contém uma expressão opaca para uma consulta associada a um `DataSource` elemento em um [QueryBinding](../data-type/querybinding-data-type-assl.md) elemento.|  
|[Ler o elemento &#40;ASSL&#41;](read-element-assl.md)|Determina se os dados ou metadados podem ser lidos para um determinado [CubeDimensionPermission](../data-type/permission-data-type-assl.md) ou [permissão](../data-type/permission-data-type-assl.md) elemento.|  
|[Elemento ReadDefinition &#40;ASSL&#41;](readdefinition-element-assl.md)|Determina se os membros podem ler a definição do banco de dados ou a definição de objetos no banco de dados.|  
|[Elemento ReadSourceData &#40;ASSL&#41;](readsourcedata-element-assl.md)|Determina como nomes exclusivos são gerados para hierarquias que estão contidas em `CubePermission`.|  
|[Elemento RefreshInterval &#40;ASSL&#41;](refreshinterval-element-assl.md)|Especifica o intervalo no qual os dados ligados associados ao elemento pai são atualizados.|  
|[Elemento RefreshPolicy &#40;ASSL&#41;](refreshpolicy-element-assl.md)|Determina a frequência com que a parte dinâmica do grupo de medidas ou dimensões (conforme especificado pela [persistência](persistence-element-assl.md) elemento) é verificada quanto a alterações.|  
|[Elemento RelationshipType &#40;ASSL&#41;](relationshiptype-element-assl.md)|Indica se as relações de membro para um elemento `AttributeRelationship` podem ser alteradas.|  
|[Elemento RemoteDatasourceID &#40;ASSL&#41;](remotedatasourceid-element-assl.md)|Especifica a ID da fonte de dados OLAP que aponta para a instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que armazena a partição remota.|  
|[Elemento ReportingFirstMonth &#40;ASSL&#41;](reportingfirstmonth-element-assl.md)|Define o primeiro mês de relatório do elemento `TimeBinding`.|  
|[Elemento ReportingFirstWeekOfMonth &#40;ASSL&#41;](reportingfirstweekofmonth-element-assl.md)|Define a primeira semana do mês de relatório do elemento `TimeBinding`.|  
|[Elemento ReportingWeekToMonthPattern &#40;ASSL&#41;](reportingweektomonthpattern-element-assl.md)|Define o padrão de relatório mensal, semana a semana, para o elemento `TimeBinding`.|  
|[Elemento ReportServer &#40;ASSL&#41;](reportserver-element-assl.md)|Contém o nome da instância do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] usada por `ReportAction`.|  
|[Elemento RequiresRestart &#40;ASSL&#41;](requiresrestart-element-assl.md)|Contém um valor somente leitura associado a um elemento `ServerProperty` que determina se a alteração do valor da propriedade de servidor requer a instância seja reiniciada para validar a alteração.|  
|[Elemento RoleID &#40;ASSL&#41;](roleid-element-assl.md)|Identifica a função para a qual permissões estão estando definidas.|  
|[Elemento raiz &#40;ASSL&#41;](root-element-assl.md)|Contém os dados (conjunto de linhas) para uma fonte de dados.|  
|[Elemento RootMemberIf &#40;ASSL&#41;](rootmemberif-element-assl.md)|Determina como são identificados os membros raiz ou membros de um atributo pai.|  
|[Elemento de esquema &#40;ASSL&#41;](schema-element-assl.md)|Contém o esquema da exibição da fonte de dados.|  
|[Elemento ScriptCacheProcessingMode &#40;ASSL&#41;](scriptcacheprocessingmode-element-assl.md)|Indica se o servidor deve criar o cache de scripts durante ou após o processamento.|  
|[Elemento SilenceInterval &#40;ASSL&#41;](silenceinterval-element-assl.md)|Define a quantidade mínima de tempo durante o qual a instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] é pausada antes de iniciar o processo de imagens MOLAP.|  
|[Elemento SilenceOverrideInterval &#40;ASSL&#41;](silenceoverrideinterval-element-assl.md)|Define o período de tempo que deve decorrer após o recebimento da notificação inicial, antes da geração de imagens MOLAP começar incondicionalmente.|  
|[Fatiar o elemento &#40;ASSL&#41;](slice-element-assl.md)|Contém uma expressão MDX que define a fatia contida em uma partição.|  
|[Elemento SolveOrder &#40;ASSL&#41;](solveorder-element-assl.md)|Indica a ordem de resolução na qual o elemento `CalculationProperty` é aplicado a um membro calculado ou definição de célula calculada.|  
|[Elemento Source &#40;associação&#41; &#40;ASSL&#41;](source-element-binding-assl.md)|Identifica a fonte de dados à qual o elemento pai está associado.|  
|[Elemento Source &#40;ComAssembly&#41; &#40;ASSL&#41;](source-element-comassembly-assl.md)|Contém o nome de arquivo ou identificador programático (ProgID) para um componente COM (Component Object Model).|  
|[Elemento Source &#40;medida&#41; &#40;ASSL&#41;](source-element-measure-assl.md)|Contém os detalhes da fonte que contém o valor do elemento `Measure`.|  
|[Elemento SourceAttributeID &#40;ASSL&#41;](sourceattributeid-element-assl.md)|Contém a ID do atributo de origem no qual o [nível](../objects/level-element-assl.md) baseia-se elemento.|  
|[Elemento SourceColumnID &#40;ASSL&#41;](sourcecolumnid-element-assl.md)|Contém a ID da coluna de estrutura de mineração de origem no elemento ancestral `MiningStructure`.|  
|[Estado do elemento &#40;ASSL&#41;](state-element-assl.md)|Contém um valor somente leitura que descreve o estado de processamento atual do elemento pai.|  
|[Elemento status &#40;ASSL&#41;](status-element-assl.md)|Contém uma linguagem MDX que retorna um indicador de status para um elemento `Kpi`.|  
|[Elemento StatusGraphic &#40;ASSL&#41;](statusgraphic-element-assl.md)|Contém a representação gráfica recomendada do status do elemento `Kpi`.|  
|[Elemento StopTime &#40;ASSL&#41;](stoptime-element-assl.md)|Especifica a data e a hora em que um elemento `Trace` deve parar.|  
|[Elemento StorageLocation &#40;ASSL&#41;](storagelocation-element-assl.md)|Contém o local de armazenamento do sistema de arquivos de conteúdos do elemento pai.|  
|[Elemento StorageMode &#40;ASSL&#41;](storagemode-element-assl.md)|Determina o modo de armazenamento para o elemento pai.|  
|[Elemento TableID &#40;ASSL&#41;](tableid-element-assl.md)|Contém a ID da tabela (do elemento `DataSourceView`) associada ao elemento pai.|  
|[Elemento de destino &#40;ASSL&#41;](target-element-assl.md)|Identifica o destino do elemento `Action`.|  
|[Elemento TargetType &#40;ASSL&#41;](targettype-element-assl.md)|Identifica o tipo de item do item identificado na [destino](target-element-assl.md) elemento.|  
|[Elemento de texto &#40;ASSL&#41;](text-element-assl.md)|Contém o texto de um [comando](../objects/command-element-assl.md) elemento.|  
|[Elemento timeout &#40;ASSL&#41;](timeout-element-assl.md)|Especifica a hora, em segundos, depois da qual a tentativa de recuperar dados relata um tempo limite.|  
|[Elemento de tendência &#40;ASSL&#41;](trend-element-assl.md)|Contém uma linguagem MDX que retorna um indicador de tendência para um elemento `Kpi`.|  
|[Elemento TrendGraphic &#40;ASSL&#41;](trendgraphic-element-assl.md)|Contém a representação gráfica recomendada da tendência do elemento `Kpi`.|  
|[Elemento Trimming &#40;ASSL&#41;](trimming-element-assl.md)|Especifica como os dados da fonte de dados são cortados.|  
|[Elemento de tipo &#40;ação&#41; &#40;ASSL&#41;](type-element-action-assl.md)|Contém o tipo de elemento `Action`.|  
|[Elemento de tipo &#40;associação&#41; &#40;ASSL&#41;](type-element-binding-assl.md)|Contém o tipo de ligação do atributo.|  
|[Elemento de tipo &#40;ClrAssemblyFile&#41; &#40;ASSL&#41;](type-element-clrassemblyfile-assl.md)|Especifica o tipo de arquivo de um dos arquivos que pertencem a um assembly do .NET Framework.|  
|[Elemento de tipo &#40;dimensão&#41; &#40;ASSL&#41;](type-element-dimension-assl.md)|Fornece informações sobre o conteúdo da dimensão.|  
|[Elemento de tipo &#40;DimensionAttribute&#41; &#40;ASSL&#41;](type-element-dimensionattribute-assl.md)|Contém o tipo do atributo.|  
|[Elemento de tipo &#40;MeasureGroup&#41; &#40;ASSL&#41;](type-element-measuregroup-assl.md)|Especifica o tipo do `MeasureGroup`.|  
|[Elemento de tipo &#40;MeasureGroupAttribute&#41; &#40;ASSL&#41;](type-element-measuregroupattribute-assl.md)|Contém o tipo de um [MeasureGroupAttribute](../data-type/measuregroupattribute-data-type-assl.md) elemento.|  
|[Elemento de tipo &#40;MiningStructureColumn&#41; &#40;ASSL&#41;](type-element-miningstructurecolumn-assl.md)|Contém o tipo dos [MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md) elemento.|  
|[Elemento de tipo &#40;partição&#41; &#40;ASSL&#41;](type-element-partition-assl.md)|Contém o tipo de elemento `Partition`.|  
|[Elemento de tipo &#40;PerspectiveCalculation&#41; &#40;ASSL&#41;](type-element-perspectivecalculation-assl.md)|Indica o tipo dos [PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md) elemento.|  
|[Elemento UnknownMember &#40;ASSL&#41;](unknownmember-element-assl.md)|Indica se o membro desconhecido é visível.|  
|[Elemento UnknownMemberName &#40;ASSL&#41;](unknownmembername-element-assl.md)|Contém a legenda, no idioma padrão da dimensão, para o membro desconhecido da dimensão.|  
|[Elemento Usage &#40;DimensionAttribute&#41; &#40;ASSL&#41;](usage-element-dimensionattribute-assl.md)|Descreve como um atributo é usado.|  
|[Elemento Usage &#40;MiningModelColumn&#41; &#40;ASSL&#41;](usage-element-miningmodelcolumn-assl.md)|Descreve como a coluna associada no pai `MiningStructure` é usada.|  
|[Valor do elemento &#40;ASSL&#41;](value-element-assl.md)|Contém o valor do elemento pai.|  
|[Elemento Version &#40;ASSL&#41;](version-element-assl.md)|Contém o número de versão somente leitura da instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] representada pelo elemento `Server`.|  
|[Elemento Visibility &#40;ASSL&#41;](visibility-element-assl.md)|Define a visibilidade de um [anotação](../objects/annotation-element-assl.md) elemento.|  
|[Elemento Visible &#40;ASSL&#41;](visible-element-assl.md)|Determina a visibilidade do elemento pai.|  
|[Elemento VisualTotals &#40;ASSL&#41;](visualtotals-element-assl.md)|Contém uma linguagem MDX que determina se os totais visuais são exibidos para membros deste atributo.|  
|[Gravar o elemento &#40;ASSL&#41;](write-element-assl.md)|Determina se dados ou metadados podem ser gravados para um determinado elemento `CubeDimensionPermission` ou `Permission`.|  
|[Elemento WriteEnabled &#40;ASSL&#41;](writeenabled-element-assl.md)|Indica se write-backs de dimensão estão disponíveis (sujeito a permissões de segurança).|  
  
## <a name="see-also"></a>Consulte também  
 [Hierarquia Analysis Services Scripting Language XML elemento &#40;ASSL&#41;](../analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
