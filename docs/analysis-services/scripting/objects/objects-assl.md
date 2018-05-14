---
title: Objetos (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e2ff05366ae438da1badf0b55aa3bbaff4b32d43
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="objects-assl"></a>Objetos (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Esta seção de referência contém informações de sintaxe e uso de cada elemento que age como um objeto no esquema ASSL (Analysis Services Scripting Language).  
  
 Embora o esquema ASSL contenha somente elementos XML, do ponto de vista do desenvolvedor, os elementos descritos nessa seção correspondem a objetos, como **banco de dados**, **cubo**, e  **Dimensão** objetos na hierarquia de objetos contidos em uma instância de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 Os objetos nunca são elementos do nível folha no esquema ASSL, mas têm elementos filho e elementos que correspondem às propriedades de objeto.  
  
 Em alguns casos, um elemento do nível folha no esquema que pode parecer uma propriedade é classificado como um objeto porque o tipo de elemento é um tipo de objeto. Por exemplo, o **fonte** de um **dimensão** objeto é do tipo **DimensionBinding**.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Elemento|Description|  
|-------------|-----------------|  
|[Elemento de conta &#40;ASSL&#41;](../../../analysis-services/scripting/objects/account-element-assl.md)|Contém detalhes sobre um tipo de conta dentro de um [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.|  
|[Elemento Action &#40;ASSL&#41;](../../../analysis-services/scripting/objects/action-element-assl.md)|Contém informações sobre uma ação disponível em um elemento [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) ou um elemento [Perspective](../../../analysis-services/scripting/objects/perspective-element-assl.md) .|  
|[Elemento Aggregation &#40;ASSL&#41;](../../../analysis-services/scripting/objects/aggregation-element-assl.md)|Define uma única agregação para um [partição](../../../analysis-services/scripting/objects/partition-element-assl.md) elemento.|  
|[Elemento AggregationDesign &#40;ASSL&#41;](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)|Define um conjunto de definições de agregação que podem ser compartilhadas entre várias partições de um banco de dados.|  
|[Elemento AggregationInstance &#40;ASSL&#41;](../../../analysis-services/scripting/objects/aggregationinstance-element-assl.md)|Define uma instância de agregação para uma partição.|  
|[Elemento AlgorithmParameter &#40;ASSL&#41;](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)|Define um parâmetro para o algoritmo usado por um [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) elemento.|  
|[Elemento AllMemberTranslation &#40;ASSL&#41;](../../../analysis-services/scripting/objects/allmembertranslation-element-assl.md)|Contém uma tradução para a legenda do membro All de um [hierarquia](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) elemento.|  
|[Elemento Annotation &#40;ASSL&#41;](../../../analysis-services/scripting/objects/annotation-element-assl.md)|Contém elementos que são usados para estender o esquema ASSL.|  
|[Elemento assembly &#40;ASSL&#41;](../../../analysis-services/scripting/objects/assembly-element-assl.md)|Representa um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] assembly ou uma biblioteca de vínculo dinâmico (DLL) COM associado com um [servidor](../../../analysis-services/scripting/objects/server-element-assl.md) elemento ou um [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.|  
|[Atributo de elemento &#40;ASSL&#41;](../../../analysis-services/scripting/objects/attribute-element-assl.md)|Contém a descrição de um atributo.|  
|[Elemento AttributeAllMemberTranslation &#40;ASSL&#41;](../../../analysis-services/scripting/objects/attributeallmembertranslation-element-assl.md)|Contém uma tradução para a legenda do membro All de um [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md) elemento.|  
|[Elemento AttributePermission &#40;ASSL&#41;](../../../analysis-services/scripting/objects/attributepermission-element-assl.md)|Define as permissões que os membros de um [função](../../../analysis-services/scripting/objects/role-element-assl.md) elemento tem os atributos de uma dimensão individual de um [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento.|  
|[Elemento AttributeRelationship &#40;ASSL&#41;](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)|Fornece detalhes sobre a relação entre dois atributos.|  
|[Bloquear elemento &#40;ASSL&#41;](../../../analysis-services/scripting/objects/block-element-assl.md)|Contém todo ou parte do conteúdo binário de um [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md) elemento.|  
|[Elemento Calculation &#40;ASSL&#41;](../../../analysis-services/scripting/objects/calculation-element-assl.md)|Associa um cálculo com um [perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md) elemento.|  
|[Elemento CalculationProperty &#40;ASSL&#41;](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)|Contém uma coleção de propriedades de interface de usuário para um cálculo usado em uma [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md) elemento.|  
|[Elemento CaptionColumn &#40;ASSL&#41;](../../../analysis-services/scripting/objects/captioncolumn-element-assl.md)|Define a coluna que fornece a legenda do atributo.|  
|[Elemento CellPermission &#40;ASSL&#41;](../../../analysis-services/scripting/objects/cellpermission-element-assl.md)|Descreve as permissões que os membros de um [função](../../../analysis-services/scripting/objects/role-element-assl.md) elemento têm em células individuais de um [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento.|  
|[Elemento Column &#40;ASSL&#41;](../../../analysis-services/scripting/objects/column-element-assl.md)|Descreve uma coluna na coleção de colunas associada ao elemento pai.|  
|[Elemento de comando &#40;ASSL&#41;](../../../analysis-services/scripting/objects/command-element-assl.md)|Define um comando que está disponível para uso dentro do contexto do elemento pai da coleção Commands.|  
|[Elemento de cubo &#40;ASSL&#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)|Define um cubo normal, virtual ou vinculado em um [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.|  
|[Elemento CubePermission &#40;ASSL&#41;](../../../analysis-services/scripting/objects/cubepermission-element-assl.md)|Define as permissões dos membros de um determinado [função](../../../analysis-services/scripting/objects/role-element-assl.md) elemento em uma determinada [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento.|  
|[Elemento CustomRollupColumn &#40;ASSL&#41;](../../../analysis-services/scripting/objects/customrollupcolumn-element-assl.md)|Define os detalhes da coluna que fornece uma fórmula de acúmulo personalizada.|  
|[Elemento CustomRollupPropertiesColumn &#40;ASSL&#41;](../../../analysis-services/scripting/objects/customrolluppropertiescolumn-element-assl.md)|Define os detalhes de uma coluna que fornece as propriedades de uma fórmula de acúmulo personalizada.|  
|[Elemento de dados &#40;ASSL&#41;](../../../analysis-services/scripting/objects/data-element-assl.md)|Contém (na coleção de filhos **bloco** elementos) o conteúdo binário de um [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md) elemento.|  
|[Elemento de banco de dados &#40;ASSL&#41;](../../../analysis-services/scripting/objects/database-element-assl.md)|Define um banco de dados do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento DatabasePermission &#40;ASSL&#41;](../../../analysis-services/scripting/objects/databasepermission-element-assl.md)|Define as permissões padrão em uma [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento para um determinado [função](../../../analysis-services/scripting/objects/role-element-assl.md) elemento.|  
|[Elemento DataSource &#40;ASSL&#41;](../../../analysis-services/scripting/objects/datasource-element-assl.md)|Define uma fonte de dados em um [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.|  
|[Elemento DataSourcePermission &#40;ASSL&#41;](../../../analysis-services/scripting/objects/datasourcepermission-element-assl.md)|Define as permissões padrão em uma [DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md) tipo de dados para um determinado [função](../../../analysis-services/scripting/objects/role-element-assl.md) elemento.|  
|[Elemento DataSourceView &#40;ASSL&#41;](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)|Define uma exibição da fonte de dados usada por um [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.|  
|[Elemento de dimensão &#40;ASSL&#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)|Define uma dimensão.|  
|[Elemento DimensionPermission &#40;ASSL&#41;](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md)|Define as permissões que pertencem a um determinado [função](../../../analysis-services/scripting/objects/role-element-assl.md) elemento para uma dimensão de banco de dados específico ou a dimensão do cubo.|  
|[Elemento ErrorConfiguration &#40;ASSL&#41;](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)|Especifica configurações para manipular erros que podem ocorrer quando o elemento pai é processado.|  
|[Elemento Event &#40;ASSL&#41;](../../../analysis-services/scripting/objects/event-element-assl.md)|Define um evento a ser capturado como parte de um [rastreamento](../../../analysis-services/scripting/objects/trace-element-assl.md) elemento.|  
|[Elemento de arquivo &#40;ASSL&#41;](../../../analysis-services/scripting/objects/file-element-assl.md)|Define um dos arquivos que compõem um [ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md) elemento.|  
|[Elemento ForeignKeyColumn &#40;ASSL&#41;](../../../analysis-services/scripting/objects/foreignkeycolumn-element-assl.md)|Identifica a junção a uma tabela pai para uma fonte de dados relacional.|  
|[Elemento de grupo &#40;ASSL&#41;](../../../analysis-services/scripting/objects/group-element-assl.md)|Define um grupo de membros associado a um atributo.|  
|[Elemento Hierarchy &#40;ASSL&#41;](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)|Define uma hierarquia em uma dimensão.|  
|[Elemento IncrementalProcessingNotification &#40;ASSL&#41;](../../../analysis-services/scripting/objects/incrementalprocessingnotification-element-assl.md)|Contém informações para o [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) elemento sobre uma consulta a ser executada para determinar o andamento do processamento incremental.|  
|[Elemento KeyColumn &#40;ASSL&#41;](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)|Contém a definição de uma coluna, ou faz parte, a chave para um atributo.|  
|[Elemento KPI &#40;ASSL&#41;](../../../analysis-services/scripting/objects/kpi-element-assl.md)|Define um KPI (indicador chave de desempenho) em um elemento [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) ou em um elemento [Perspective](../../../analysis-services/scripting/objects/perspective-element-assl.md) .|  
|[Elemento de nível &#40;ASSL&#41;](../../../analysis-services/scripting/objects/level-element-assl.md)|Define um nível em uma [hierarquia](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) elemento.|  
|[Elemento MdxScript &#40;ASSL&#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)|Contém informações sobre um script MDX (Multidimensional Expressions) que está associado com um [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento.|  
|[Elemento de medidas &#40;ASSL&#41;](../../../analysis-services/scripting/objects/measure-element-assl.md)|Define uma medida.|  
|[Elemento MeasureGroup &#40;ASSL&#41;](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|Define um conjunto de medidas no mesmo nível de granularidade.|  
|[Elemento Member &#40;ASSL&#41;](../../../analysis-services/scripting/objects/member-element-assl.md)|Contém o nome de um membro de um elemento [Group](../../../analysis-services/scripting/objects/group-element-assl.md) ou de um elemento [Role](../../../analysis-services/scripting/objects/role-element-assl.md) .|  
|[Elemento MiningModel &#40;ASSL&#41;](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)|Define um único modelo de mineração de dados.|  
|[Elemento MiningModelPermission &#40;ASSL&#41;](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md)|Define os permissões que os membros de um [função](../../../analysis-services/scripting/objects/role-element-assl.md) elemento ter um indivíduo [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) elemento.|  
|[Elemento MiningStructure &#40;ASSL&#41;](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|Define a estrutura para um conjunto de modelos de mineração.|  
|[Elemento MiningStructurePermission &#40;ASSL&#41;](../../../analysis-services/scripting/objects/miningstructurepermission-element-assl.md)|Define as permissões que os membros de um [função](../../../analysis-services/scripting/objects/role-element-assl.md) elemento ter um indivíduo [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) elemento.|  
|[Elemento ModelingFlag &#40;ASSL&#41;](../../../analysis-services/scripting/objects/modelingflag-element-assl.md)|Contém um sinalizador de modelagem para uma coluna em uma estrutura ou modelo de mineração.|  
|[Elemento NameColumn &#40;ASSL&#41;](../../../analysis-services/scripting/objects/namecolumn-element-assl.md)|Identifica a coluna que fornece o nome do elemento pai.|  
|[Elemento NamingTemplateTranslation &#40;ASSL&#41;](../../../analysis-services/scripting/objects/namingtemplatetranslation-element-assl.md)|Fornece uma tradução localizada do **NamingTemplate** elemento para um pai [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md) tipo de dados.|  
|[Elemento de partição &#40;ASSL&#41;](../../../analysis-services/scripting/objects/partition-element-assl.md)|Define uma partição de um [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md) elemento ou uma associação de partição em uma limite de linha [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)elemento.|  
|[Elemento Perspective &#40;ASSL&#41;](../../../analysis-services/scripting/objects/perspective-element-assl.md)|Define os detalhes de uma perspectiva de um [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento.|  
|[Elemento ProactiveCaching &#40;ASSL&#41;](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|Define configurações de cache pró-ativo para o elemento pai.|  
|[Elemento QueryNotification &#40;ASSL&#41;](../../../analysis-services/scripting/objects/querynotification-element-assl.md)|Contém informações para o [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) elemento sobre uma consulta a ser executada para determinar se uma fonte de dados foi modificada.|  
|[Elemento ReportFormatParameter &#40;ASSL&#41;](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md)|Contém o nome e o valor de um parâmetro que especifica como uma [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] relatório é formatado no tempo de execução.|  
|[Elemento ReportParameter &#40;ASSL&#41;](../../../analysis-services/scripting/objects/reportparameter-element-assl.md)|Contém o nome e valor de um parâmetro que é transmitido para um relatório do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] no tempo de execução.|  
|[Elemento Role &#40;ASSL&#41;](../../../analysis-services/scripting/objects/role-element-assl.md)|Contém informações sobre uma função de segurança.|  
|[Elemento Server &#40;ASSL&#41;](../../../analysis-services/scripting/objects/server-element-assl.md)|Descreve uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento ServerProperty &#40;ASSL&#41;](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|Define uma propriedade de servidor associada com um [Server](../../../analysis-services/scripting/objects/server-element-assl.md) elemento.|  
|[Elemento SkippedLevelsColumn &#40;ASSL&#41;](../../../analysis-services/scripting/objects/skippedlevelscolumn-element-assl.md)|Fornece os detalhes de uma coluna que armazena o número de níveis ignorados (vazios) entre cada membro e seu pai.|  
|[Elemento SourceMeasureGroup &#40;ASSL&#41;](../../../analysis-services/scripting/objects/sourcemeasuregroup-element-assl.md)|Identifica o grupo de medidas que serve como a fonte de dados para uma coluna de estrutura de mineração.|  
|[Elemento TableNotification &#40;ASSL&#41;](../../../analysis-services/scripting/objects/tablenotification-element-assl.md)|Contém informações para o [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) elemento sobre uma tabela ou exibição da fonte de dados que foi modificada.|  
|[Elemento trace &#40;ASSL&#41;](../../../analysis-services/scripting/objects/trace-element-assl.md)|Define um rastreamento que pode ser consultado.|  
|[Elemento Translation &#40;ASSL&#41;](../../../analysis-services/scripting/objects/translation-element-assl.md)|Fornece uma tradução localizada para o pai da coleção [Translations](../../../analysis-services/scripting/collections/translations-element-assl.md) .|  
|[Elemento UnaryOperatorColumn &#40;ASSL&#41;](../../../analysis-services/scripting/objects/unaryoperatorcolumn-element-assl.md)|Define os detalhes de uma coluna que fornece um operador unário.|  
|[Elemento UnknownMemberTranslation &#40;ASSL&#41;](../../../analysis-services/scripting/objects/unknownmembertranslation-element-assl.md)|Contém uma tradução para a legenda do [UnknownMember](../../../analysis-services/scripting/properties/unknownmember-element-assl.md) elemento para uma [dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md) elemento.|  
|[Elemento ValueColumn &#40;ASSL&#41;](../../../analysis-services/scripting/objects/valuecolumn-element-assl.md)|Identifica a coluna que fornece o valor do elemento pai.|  
  
## <a name="see-also"></a>Consulte também  
 [Hierarquia de elementos XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
