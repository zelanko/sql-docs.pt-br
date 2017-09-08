---
title: Elemento StorageEngineUsed (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- StorageEngineUsed Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
ms.assetid: 98895c10-f3c2-4d8a-be94-6128c828561d
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 188c9261964839c055b75e2abb4c1e8fc4ec3633
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="storageengineused-element-xmla"></a>Elemento StorageEngineUsed (XMLA)
  Contém um valor somente leitura que descreve o tipo do banco de dados atual.  
  
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
            <StorageEngineUsed >...</StorageEngineUsed>  
   </Database>  
</Databases>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[database](../../../analysis-services/scripting/objects/database-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Tradicional*|O modelo de banco de dados corresponde a um modo de armazenamento MOLAP, ROLAP ou HOLAP.|  
|*InMemory*|O modelo de banco de dados corresponde a um modo de armazenamento IMBI.|  
|*Misto*|O modelo de banco de dados mescla modos de armazenamento IMBI e MOLAP, ROLAP ou HOLAP.|  
  
 A enumeração que corresponde aos valores permitidos para **StorageEngineUsed** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.StorageEngineUsed>.  
  
 Os elementos que correspondem aos pais de **StorageEngineUsed** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.Database>.  
  
  
