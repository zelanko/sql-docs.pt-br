---
title: Objetos (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- ASSL, objects
- objects [Analysis Services Scripting Language]
- Analysis Services Scripting Language, objects
ms.assetid: 0f672b93-c317-47e5-b44d-ecea9b587c98
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 302ad689a3e54a7a9937929b9c20f975fc3cd98f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079606"
---
# <a name="objects-assl"></a>Objetos (ASSL)
  Esta seção de referência contém informações de sintaxe e uso de cada elemento que age como um objeto no esquema ASSL (Analysis Services Scripting Language).  
  
 Embora o esquema ASSL contenha somente elementos XML, do ponto de vista do desenvolvedor, os elementos descritos nessa seção correspondem a objetos, como `Database`, `Cube`, e `Dimension` objetos na hierarquia de objetos contidos por um instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 Os objetos nunca são elementos do nível folha no esquema ASSL, mas têm elementos filho e elementos que correspondem às propriedades de objeto.  
  
 Em alguns casos, um elemento do nível folha no esquema que pode parecer uma propriedade é classificado como um objeto porque o tipo de elemento é um tipo de objeto. Por exemplo, a `Source` de um objeto `Dimension` é de tipo `DimensionBinding`.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Elemento|Description|  
|-------------|-----------------|  
|[Elemento de conta &#40;ASSL&#41;](account-element-assl.md)|Contém detalhes sobre um tipo de conta dentro de um [banco de dados](database-element-assl.md) elemento.|  
|[Elemento Action &#40;ASSL&#41;](action-element-assl.md)|Contém informações sobre uma ação disponível em um [cubo](cube-element-assl.md) elemento ou um [perspectiva](perspective-element-assl.md) elemento.|  
|[Elemento Aggregation &#40;ASSL&#41;](aggregation-element-assl.md)|Define uma única agregação para um [partição](partition-element-assl.md) elemento.|  
|[Elemento AggregationDesign &#40;ASSL&#41;](aggregationdesign-element-assl.md)|Define um conjunto de definições de agregação que podem ser compartilhadas entre várias partições de um banco de dados.|  
|[Elemento AggregationInstance &#40;ASSL&#41;](aggregationinstance-element-assl.md)|Define uma instância de agregação para uma partição.|  
|[Elemento AlgorithmParameter &#40;ASSL&#41;](algorithmparameter-element-assl.md)|Define um parâmetro para o algoritmo usado por um [MiningModel](miningmodel-element-assl.md) elemento.|  
|[Elemento AllMemberTranslation &#40;ASSL&#41;](translation-element-assl.md)|Contém uma tradução para a legenda do membro All de um [hierarquia](hierarchy-element-assl.md) elemento.|  
|[Elemento Annotation &#40;ASSL&#41;](annotation-element-assl.md)|Contém elementos que são usados para estender o esquema ASSL.|  
|[Elemento assembly &#40;ASSL&#41;](assembly-element-assl.md)|Representa uma [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] assembly ou uma biblioteca de vínculo dinâmico (DLL) COM associado com um [Server](server-element-assl.md) elemento ou uma [banco de dados](database-element-assl.md) elemento.|  
|[Atributo do elemento &#40;ASSL&#41;](attribute-element-assl.md)|Contém a descrição de um atributo.|  
|[Elemento AttributeAllMemberTranslation &#40;ASSL&#41;](attributeallmembertranslation-element-assl.md)|Contém uma tradução para a legenda do membro All de um [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md) elemento.|  
|[Elemento AttributePermission &#40;ASSL&#41;](attributepermission-element-assl.md)|Define as permissões que os membros de um [função](role-element-assl.md) elemento têm nos atributos de uma dimensão individual em um [cubo](cube-element-assl.md) elemento.|  
|[Elemento AttributeRelationship &#40;ASSL&#41;](attributerelationship-element-assl.md)|Fornece detalhes sobre a relação entre dois atributos.|  
|[Bloquear o elemento &#40;ASSL&#41;](block-element-assl.md)|Contém todo ou parte do conteúdo binário de um [ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md) elemento.|  
|[Elemento Calculation &#40;ASSL&#41;](calculation-element-assl.md)|Associa a um cálculo com um [perspectiva](perspective-element-assl.md) elemento.|  
|[Elemento CalculationProperty &#40;ASSL&#41;](calculationproperty-element-assl.md)|Contém uma coleção de propriedades de interface do usuário para um cálculo usado em uma [MdxScript](mdxscript-element-assl.md) elemento.|  
|[Elemento CaptionColumn &#40;ASSL&#41;](column-element-assl.md)|Define a coluna que fornece a legenda do atributo.|  
|[Elemento CellPermission &#40;ASSL&#41;](cellpermission-element-assl.md)|Descreve as permissões que os membros de um [função](role-element-assl.md) elemento têm em células individuais de uma [cubo](cube-element-assl.md) elemento.|  
|[Elemento Column &#40;ASSL&#41;](column-element-assl.md)|Descreve uma coluna na coleção de colunas associada ao elemento pai.|  
|[Elemento de comando &#40;ASSL&#41;](command-element-assl.md)|Define um comando que está disponível para uso dentro do contexto do elemento pai da coleção Commands.|  
|[Elemento de cubo &#40;ASSL&#41;](cube-element-assl.md)|Define um cubo normal, virtual ou vinculado em uma [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] [banco de dados](database-element-assl.md) elemento.|  
|[Elemento CubePermission &#40;ASSL&#41;](cubepermission-element-assl.md)|Define as permissões dos membros de um determinado [função](role-element-assl.md) elemento em um determinado [cubo](cube-element-assl.md) elemento.|  
|[Elemento CustomRollupColumn &#40;ASSL&#41;](customrollupcolumn-element-assl.md)|Define os detalhes da coluna que fornece uma fórmula de acúmulo personalizada.|  
|[Elemento CustomRollupPropertiesColumn &#40;ASSL&#41;](customrolluppropertiescolumn-element-assl.md)|Define os detalhes de uma coluna que fornece as propriedades de uma fórmula de acúmulo personalizada.|  
|[Elemento de dados &#40;ASSL&#41;](data-element-assl.md)|Contém (na coleção de filhos `Block` elementos) o conteúdo binário de um [ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md) elemento.|  
|[Elemento de banco de dados &#40;ASSL&#41;](database-element-assl.md)|Define um banco de dados do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento DatabasePermission &#40;ASSL&#41;](databasepermission-element-assl.md)|Define as permissões padrão em uma [banco de dados](database-element-assl.md) elemento para um determinado [função](role-element-assl.md) elemento.|  
|[Elemento de fonte de dados &#40;ASSL&#41;](datasource-element-assl.md)|Define uma fonte de dados em um [banco de dados](database-element-assl.md) elemento.|  
|[Elemento DataSourcePermission &#40;ASSL&#41;](datasourcepermission-element-assl.md)|Define as permissões padrão em uma [fonte de dados](../data-type/datasource-data-type-assl.md) tipo de dados para um determinado [função](role-element-assl.md) elemento.|  
|[Elemento DataSourceView &#40;ASSL&#41;](datasourceview-element-assl.md)|Define uma exibição da fonte de dados usada por um [banco de dados](database-element-assl.md) elemento.|  
|[Elemento de dimensão &#40;ASSL&#41;](dimension-element-assl.md)|Define uma dimensão.|  
|[Elemento DimensionPermission &#40;ASSL&#41;](dimensionpermission-element-assl.md)|Define as permissões que pertencem a um determinado [função](role-element-assl.md) elemento para uma dimensão de banco de dados específico ou a dimensão do cubo.|  
|[Elemento ErrorConfiguration &#40;ASSL&#41;](errorconfiguration-element-assl.md)|Especifica configurações para manipular erros que podem ocorrer quando o elemento pai é processado.|  
|[Elemento Event &#40;ASSL&#41;](event-element-assl.md)|Define um evento a ser capturado como parte de um [rastreamento](trace-element-assl.md) elemento.|  
|[Elemento de arquivo &#40;ASSL&#41;](file-element-assl.md)|Define um dos arquivos que compõem uma [ClrAssembly](../data-type/assembly-data-type-assl.md) elemento.|  
|[Elemento ForeignKeyColumn &#40;ASSL&#41;](keycolumn-element-assl.md)|Identifica a junção a uma tabela pai para uma fonte de dados relacional.|  
|[Elemento de grupo &#40;ASSL&#41;](group-element-assl.md)|Define um grupo de membros associado a um atributo.|  
|[Elemento Hierarchy &#40;ASSL&#41;](hierarchy-element-assl.md)|Define uma hierarquia em uma dimensão.|  
|[Elemento IncrementalProcessingNotification &#40;ASSL&#41;](incrementalprocessingnotification-element-assl.md)|Contém informações para o [ProactiveCaching](proactivecaching-element-assl.md) elemento sobre uma consulta a ser executada para determinar o andamento do processamento incremental.|  
|[Elemento KeyColumn &#40;ASSL&#41;](keycolumn-element-assl.md)|Contém a definição de uma coluna que é ou faz parte, a chave para um atributo.|  
|[Elemento KPI &#40;ASSL&#41;](kpi-element-assl.md)|Define um indicador chave de desempenho (KPI) em um [cubo](cube-element-assl.md) elemento ou um [perspectiva](perspective-element-assl.md) elemento.|  
|[Elemento de nível &#40;ASSL&#41;](level-element-assl.md)|Define um nível em uma [hierarquia](hierarchy-element-assl.md) elemento.|  
|[Elemento MdxScript &#40;ASSL&#41;](mdxscript-element-assl.md)|Contém informações sobre um script MDX (Multidimensional Expressions) que está associado com um [cubo](cube-element-assl.md) elemento.|  
|[Medir o elemento &#40;ASSL&#41;](measure-element-assl.md)|Define uma medida.|  
|[Elemento MeasureGroup &#40;ASSL&#41;](measuregroup-element-assl.md)|Define um conjunto de medidas no mesmo nível de granularidade.|  
|[Elemento Member &#40;ASSL&#41;](member-element-assl.md)|Contém o nome de um membro de um elemento [Group](group-element-assl.md) ou de um elemento [Role](role-element-assl.md) .|  
|[Elemento MiningModel &#40;ASSL&#41;](miningmodel-element-assl.md)|Define um único modelo de mineração de dados.|  
|[Elemento MiningModelPermission &#40;ASSL&#41;](miningmodelpermission-element-assl.md)|Define os permissões que os membros de um [função](role-element-assl.md) elemento ter em um indivíduo [MiningModel](miningmodel-element-assl.md) elemento.|  
|[Elemento MiningStructure &#40;ASSL&#41;](miningstructure-element-assl.md)|Define a estrutura para um conjunto de modelos de mineração.|  
|[Elemento MiningStructurePermission &#40;ASSL&#41;](miningstructurepermission-element-assl.md)|Define as permissões que os membros de um [função](role-element-assl.md) elemento ter em um indivíduo [MiningStructure](miningstructure-element-assl.md) elemento.|  
|[Elemento ModelingFlag &#40;ASSL&#41;](modelingflag-element-assl.md)|Contém um sinalizador de modelagem para uma coluna em uma estrutura ou modelo de mineração.|  
|[Elemento NameColumn &#40;ASSL&#41;](namecolumn-element-assl.md)|Identifica a coluna que fornece o nome do elemento pai.|  
|[Elemento NamingTemplateTranslation &#40;ASSL&#41;](namingtemplatetranslation-element-assl.md)|Fornece uma tradução localizada do `NamingTemplate` elemento para um pai [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md) tipo de dados.|  
|[Elemento de partição &#40;ASSL&#41;](partition-element-assl.md)|Define uma partição de um [MeasureGroup](measuregroup-element-assl.md) elemento ou uma associação de partição em uma limite de linha [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-out-of-line-assl.md)elemento.|  
|[Elemento Perspective &#40;ASSL&#41;](perspective-element-assl.md)|Define detalhes para uma perspectiva de um [cubo](cube-element-assl.md) elemento.|  
|[Elemento ProactiveCaching &#40;ASSL&#41;](proactivecaching-element-assl.md)|Define configurações de cache pró-ativo para o elemento pai.|  
|[Elemento QueryNotification &#40;ASSL&#41;](querynotification-element-assl.md)|Contém informações para o [ProactiveCaching](proactivecaching-element-assl.md) elemento sobre uma consulta a ser executada para determinar se uma fonte de dados foi modificada.|  
|[Elemento ReportFormatParameter &#40;ASSL&#41;](reportformatparameter-element-asl.md)|Contém o nome e o valor de um parâmetro que especifica como uma [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] relatório é formatado no tempo de execução.|  
|[Elemento ReportParameter &#40;ASSL&#41;](reportparameter-element-assl.md)|Contém o nome e valor de um parâmetro que é transmitido para um relatório do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] no tempo de execução.|  
|[Elemento de função &#40;ASSL&#41;](role-element-assl.md)|Contém informações sobre uma função de segurança.|  
|[Elemento de servidor &#40;ASSL&#41;](server-element-assl.md)|Descreve uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento ServerProperty &#40;ASSL&#41;](serverproperty-element-assl.md)|Define uma propriedade de servidor associada com um [Server](server-element-assl.md) elemento.|  
|[Elemento SkippedLevelsColumn &#40;ASSL&#41;](skippedlevelscolumn-element-assl.md)|Fornece os detalhes de uma coluna que armazena o número de níveis ignorados (vazios) entre cada membro e seu pai.|  
|[Elemento SourceMeasureGroup &#40;ASSL&#41;](sourcemeasuregroup-element-assl.md)|Identifica o grupo de medidas que serve como a fonte de dados para uma coluna de estrutura de mineração.|  
|[Elemento TableNotification &#40;ASSL&#41;](tablenotification-element-assl.md)|Contém informações para o [ProactiveCaching](proactivecaching-element-assl.md) elemento sobre uma tabela ou exibição em uma fonte de dados que foi modificada.|  
|[Elemento trace &#40;ASSL&#41;](trace-element-assl.md)|Define um rastreamento que pode ser consultado.|  
|[Elemento Translation &#40;ASSL&#41;](translation-element-assl.md)|Fornece uma tradução localizada para o pai da coleção [Translations](../collections/translations-element-assl.md) .|  
|[Elemento UnaryOperatorColumn &#40;ASSL&#41;](unaryoperatorcolumn-element-assl.md)|Define os detalhes de uma coluna que fornece um operador unário.|  
|[Elemento UnknownMemberTranslation &#40;ASSL&#41;](unknownmembertranslation-element-assl.md)|Contém uma tradução para a legenda do [UnknownMember](../properties/unknownmember-element-assl.md) elemento para um [dimensão](dimension-element-assl.md) elemento.|  
|[Elemento ValueColumn &#40;ASSL&#41;](valuecolumn-element-assl.md)|Identifica a coluna que fornece o valor do elemento pai.|  
  
## <a name="see-also"></a>Consulte também  
 [Hierarquia Analysis Services Scripting Language XML elemento &#40;ASSL&#41;](../analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
