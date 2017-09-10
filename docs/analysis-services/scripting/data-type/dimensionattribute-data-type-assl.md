---
title: Tipo de dados DimensionAttribute (ASSL) | Microsoft Docs
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
apiname:
- DimensionAttribute Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DimensionAttribute
helpviewer_keywords:
- DimensionAttribute data type
ms.assetid: 94349a87-b284-49d1-ac72-888f0375ceb8
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ea4cdde9cf38c673b5894849097c2cc3c6c43309
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="dimensionattribute-data-type-assl"></a>Tipo de dados DimensionAttribute (ASSL)
  Define um tipo de dados primitivo que representa um atributo em uma dimensão.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttribute>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Description>...</Description>  
   <Type>...</Type>  
   <Usage>...</Usage>  
   <Source>...</Source>  
   <EstimatedCount>...</EstimatedCount>  
   <KeyColumns>...</KeyColumns>  
   <NameColumn>...</NameColumn>  
   <ValueColumn>...</ValueColumn>  
   <Translations>...</Translations>  
   <AttributeRelationships>...</AttributeRelationships>  
   <DiscretizationMethod>...</DiscretizationMethod>  
   <DiscretizationBucketCount>...</DiscretizationBucketCount>  
   <RootMemberIf>...</RootMemberIf>  
   <OrderBy>...</OrderBy>  
   <DefaultMember>...</DefaultMember>  
   <OrderByAttributeID>...</OrderByAttributeID>  
   <SkippedLevelsColumn>...</SkippedLevelsColumn>  
   <NamingTemplate>...</NamingTemplate>  
   <MembersWithData>...</MembersWithData>  
   <MembersWithDataCaption>...</MembersWithDataCaption>  
   <NamingTemplateTranslations>...</NamingTemplateTranslations>  
   <CustomRollupColumn>...</CustomRollupColumn>  
   <CustomRollupPropertiesColumn>...</CustomRollupPropertiesColumn>  
   <UnaryOperatorColumn>...</UnaryOperatorColumn>  
   <AttributeHierarchyOrdered>...</AttributeHierarchyOrdered>  
   <MemberNamesUnique>...</MemberNamesUnique>  
   <IsAggregatable>...</IsAggregatable>  
   <AttributeHierarchyEnabled>...</AttributeHierarchyEnabled>  
   <AttributeHierarchyOptimizedState>...</AttributeHierarchyOptimizedState>  
   <AttributeHierarchyVisible>...</AttributeHierarchyVisible>  
   <AttributeHierarchyDisplayFolder>...</AttributeHierarchyDisplayFolder>  
   <KeyUniquenessGuarantee>...<KeyUniquenessGuarantee>  
   <InstanceSelection>...</InstanceSelection>  
   <Annotations>...</Annotations>  
</DimensionAttribute>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhuma|  
|Tipos de dados derivados|Nenhuma|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|[Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md), [AttributeHierarchyDisplayFolder](../../../analysis-services/scripting/properties/attributehierarchydisplayfolder-element-assl.md), [AttributeHierarchyEnabled](../../../analysis-services/scripting/properties/attributehierarchyenabled-element-assl.md), [AttributeHierarchyOptimizedState](../../../analysis-services/scripting/properties/attributehierarchyoptimizedstate-element-assl.md), [AttributeHierarchyOrdered](../../../analysis-services/scripting/properties/attributehierarchyordered-element-assl.md), [AttributeHierarchyVisible](../../../analysis-services/scripting/properties/attributehierarchyvisible-element-assl.md), [AttributeRelationships](../../../analysis-services/scripting/collections/attributerelationships-element-assl.md), [CustomRollupColumn](../../../analysis-services/scripting/objects/customrollupcolumn-element-assl.md), [CustomRollupPropertiesColumn](../../../analysis-services/scripting/objects/customrolluppropertiescolumn-element-assl.md), [DefaultMember](../../../analysis-services/scripting/properties/defaultmember-element-assl.md), [Description](../../../analysis-services/scripting/properties/description-element-assl.md), [DiscretizationBucketCount](../../../analysis-services/scripting/properties/discretizationbucketcount-element-assl.md), [DiscretizationMethod](../../../analysis-services/scripting/properties/discretizationmethod-element-assl.md), [EstimatedCount](../../../analysis-services/scripting/properties/estimatedcount-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [InstanceSelection](../../../analysis-services/scripting/properties/instanceselection-element-assl.md), [IsAggregatable](../../../analysis-services/scripting/properties/isaggregatable-element-assl.md), [KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md), [KeyUniquenessGuarantee](../../../analysis-services/scripting/properties/keyuniquenessguarantee-element-assl.md), [MemberNamesUnique](../../../analysis-services/scripting/properties/membernamesunique-element-assl.md), [MembersWithData](../../../analysis-services/scripting/properties/memberswithdata-element-assl.md), [MembersWithDataCaption](../../../analysis-services/scripting/properties/memberswithdatacaption-element-assl.md), [Name](../../../analysis-services/scripting/properties/name-element-assl.md), [NameColumn](../../../analysis-services/scripting/objects/namecolumn-element-assl.md), [NamingTemplate](../../../analysis-services/scripting/properties/namingtemplate-element-assl.md), [NamingTemplateTranslations](../../../analysis-services/scripting/collections/namingtemplatetranslations-element-assl.md), [OrderBy](../../../analysis-services/scripting/properties/orderby-element-assl.md), [OrderByAttributeID](../../../analysis-services/scripting/properties/orderbyattributeid-element-assl.md), [RootMemberIf](../../../analysis-services/scripting/properties/rootmemberif-element-assl.md), [SkippedLevelsColumn](../../../analysis-services/scripting/objects/skippedlevelscolumn-element-assl.md), [Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md), [Translations](../../../analysis-services/scripting/collections/translations-element-assl.md), [Type](../../../analysis-services/scripting/properties/type-element-dimensionattribute-assl.md), [UnaryOperatorColumn](../../../analysis-services/scripting/objects/unaryoperatorcolumn-element-assl.md), [Usage](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md), [ValueColumn](../../../analysis-services/scripting/objects/valuecolumn-element-assl.md)|  
|Elementos derivados|[Attribute](../../../analysis-services/scripting/objects/attribute-element-assl.md) (coleção[Attributes](../../../analysis-services/scripting/collections/attributes-element-assl.md) de [Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md))|  
  
## <a name="remarks"></a>Comentários  
 As seguintes restrições se aplicam ao executar o serviço em valores de propriedade de configuração DeploymentMode de 1 e 2 (modos SharePoint e Tabular, usados para executar [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e bancos de dados de modelo de tabela):  
  
-   Elemento de uso aceita apenas valores KEY ou REGULAR.  
  
-   O elemento IsAggregatable não pode ser false.  
  
-   O elemento OrderBy aceita apenas valores KEY ou PROPERTYKEY.  
  
-   Uma coluna calculada não pode ser uma chave primária na tabela.  
  
-   Uma coluna calculada não pode conter DataSize na associação.  
  
-   Para cada coluna calculada, uma validação de sintaxe é executada antes de salvar a definição de atributo.  
  
-   Para AttributeRelationships, RelationshipType deve ser definido com o valor, Flexible.  
  
-   O atributo 'RowNumber', identificado por 'RowNumber', deve ter o tipo inteiro.  
  
-   Somente o atributo ‘RowNumber’ pode ter KeyBinding do tipo RowNumberBinding.  
  
-   Todos os atributos que não sejam 'RowNumber' devem ter uma Cardinalidade de um em relação à chave, a menos que o próprio atributo seja a chave.  
  
-   Quando a coluna especificada por OrderBy também é o PropertyKey, o OrderByAttributeId não pode apontar para a coluna de número de linha.  
  
-   Atributos usados como chaves devem estar relacionados a todos os outros atributos; outros tipos de relações não têm suporte.  
  
-   O elemento NullProcessing não pode ser definido como 'UnknownMember.'  
  
-   As associações não podem ser definidas como ´Value´.  
  
 Os seguintes elementos não têm suportados ao executar o serviço de configuração do DeploymentMode valores de propriedade de 1 e 2 (modos SharePoint e Tabular, usados para executar [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e bancos de dados de modelo de tabela):  
  
-   AttributeHierarchyOptimizedState  
  
-   CustomRollupColumn  
  
-   CustomRollupPropertiesColumn  
  
-   DefaultMember  
  
-   DiscretizationBucketCount  
  
-   DiscretizationMethod  
  
-   SkippedLevelsColumn  
  
-   Source  
  
-   UnaryOperatorColumn  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script &#40; do Analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
