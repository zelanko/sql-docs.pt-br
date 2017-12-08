---
title: Elemento de servidor (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Server Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: server
helpviewer_keywords: Server element
ms.assetid: 92ca67f6-817e-4a75-9244-8f8bcf412190
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 12b6eb44f2ef433657f7252f10059df892cb71cc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="server-element-assl"></a>Elemento Server (ASSL)
  Descreve uma instância de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Server>  
   <!—These elements are common to each major object -->  
   <Name>...</Name>  
   <ID>...</ID>  
   <CreatedTimestamp>...</CreatedTimestamp>  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   <Description>...</Description>  
   <Annotations>...</Annotations>  
   <!-- server elements or properties -->  
   <ProductName>...</ProductName>  
   <Edition>...</Edition>  
   <EditionId>...</Edition>  
   <Version>...</Version>  
   <ServerMode>...</ServerMode>  
   <ProductLevel>...</Databases>  
   <Databases>...</Databases>  
   <Assemblies>...</Assemblies>  
   <Traces>...</Traces>  
   <Roles>...</Roles>  
   <ServerProperties>...</ServerProperties>  
</Server>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|[Nome](../../../analysis-services/scripting/properties/name-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [descrição](../../../analysis-services/scripting/properties/description-element-assl.md), [anotações ](../../../analysis-services/scripting/collections/annotations-element-assl.md), [ProductName](../../../analysis-services/scripting/properties/productname-element-assl.md), [edição](../../../analysis-services/scripting/properties/edition-element-assl.md), [EditionId](../../../analysis-services/xmla/xml-elements-properties/editionid-element.md), [versão](../../../analysis-services/scripting/properties/version-element-assl.md), [ServerMode](../../../analysis-services/xmla/xml-elements-properties/editionid-element.md), [ProductLevel](../../../analysis-services/xmla/xml-elements-properties/productlabel-element.md), [bancos de dados](../../../analysis-services/scripting/collections/databases-element-assl.md), [Assemblies](../../../analysis-services/scripting/collections/assemblies-element-assl.md), [rastreamentos](../../../analysis-services/scripting/collections/traces-element-assl.md), [funções](../../../analysis-services/scripting/collections/roles-element-assl.md), [ServerProperties](../../../analysis-services/scripting/collections/serverproperties-element-assl.md)>|  
  
## <a name="remarks"></a>Comentários  
 O **servidor** elemento representa uma instância de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]e serve como o nó mais alto na hierarquia do nó do Analysis Services Scripting Language (ASSL).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Server>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
