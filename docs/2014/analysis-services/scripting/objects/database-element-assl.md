---
title: Elemento (ASSL) do banco de dados | Microsoft Docs
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
- Database Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DATABASE
helpviewer_keywords:
- Database element
ms.assetid: c3bc7eaf-ed0d-4395-a3b7-8d9cfacfe911
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 56efc69c0e8f7f0e3e008aa5ea769774ee5014af
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37332808"
---
# <a name="database-element-assl"></a>Elemento Database (ASSL)
  Define uma [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Databases>  
   <Database>  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <LastUpdate>...</LastUpdate>  
      <Description>...</Description>  
      <State>   </State>  
      <AggregationPrefix>...</AggregationPrefix>  
      <EstimatedSize>...</EstimatedSize>  
      <LastProcessed>...</LastProcessed>  
      <Language>...</Language>  
            <Collation>...</Collation>  
      <Visible>...</Visible>  
      <MasterDatasourceID>...</MasterDataSourceID>  
      <Accounts>...</Accounts>  
      <DataSources>...</DataSources>  
      <DataSourceViews>...</DataSourceViews>  
      <Dimensions>...</Dimensions>  
      <Cubes>...</Cubes>  
      <MiningStructures>...</MiningStructures>  
            <Roles>...</Roles>  
      <Assemblies>...</Assemblies>  
      <DatabasePermissions>...</DatabasePermissions>  
            <Translations>...</Translations>  
      <Annotations>...</Annotations>  
   </Database>  
</Databases>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Bancos de dados](../collections/databases-element-assl.md)|  
|Elementos filho|[Contas](../collections/accounts-element-assl.md), [AggregationPrefix](../properties/aggregationprefix-element-assl.md), [anotações](../collections/annotations-element-assl.md), [Assemblies](../collections/assemblies-element-assl.md), [agrupamento](../properties/collation-element-assl.md), [ CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [cubos](../collections/cubes-element-assl.md), [DatabasePermissions](../collections/databasepermissions-element-assl.md), [fontes de dados](../collections/datasources-element-assl.md), [DataSourceViews](../collections/datasourceviews-element-assl.md), [Descrição](../properties/description-element-assl.md), [dimensões](../collections/dimensions-element-assl.md), [EstimatedSize](../properties/estimatedsize-element-assl.md), [ID](../properties/id-element-assl.md), [linguagem](../properties/language-element-assl.md), [ LastProcessed](../properties/lastprocessed-element-assl.md), [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [LastUpdate](../properties/lastupdate-element-assl.md), [MasterDatasourceID](../properties/datasourceid-element-assl.md), [MiningStructures](../collections/miningstructures-element-assl.md), [Nome](../properties/name-element-assl.md), [funções](../collections/roles-element-assl.md), [estado](../properties/state-element-assl.md), [traduções](../collections/translations-element-assl.md), [visíveis](../properties/visible-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Database>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de servidor &#40;ASSL&#41;](server-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
