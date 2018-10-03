---
title: Tipo de dados CubeAttribute (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CubeAttribute Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeAttribute
helpviewer_keywords:
- CubeAttribute data type
ms.assetid: 114ffb44-460b-4971-b31b-dd844e960b81
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d64224c1b7489895ff0d9dca00a3841be0ed0bbc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48203296"
---
# <a name="cubeattribute-data-type-assl"></a>Tipo de dados CubeAttribute (ASSL)
  Define um tipo de dados primitivo que representa um atributo associado com um [cubo](../objects/cube-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CubeAttribute>  
   <AttributeID>...</AttributeID>  
   <AggregationUsage>...</AggregationUsage>  
   <AttributeHierarchyOptimizedState>...</AttributeHierarchyOptimizedState>  
   <AttributeHierarchyEnabled>...</AttributeHierarchyEnabled>  
   <AttributeHierarchyVisible>...</AttributeHierarchyVisible>  
   <Annotations>...</Annotations>  
</CubeAttribute>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|None|  
|Tipos de dados derivados|None|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|None|  
|Elementos filho|[AggregationUsage](../properties/aggregationusage-element-assl.md), [anotações](../collections/annotations-element-assl.md), [AttributeHierarchyEnabled](../properties/enabled-element-assl.md), [AttributeHierarchyOptimizedState](../properties/state-element-assl.md), [ AttributeHierarchyVisible](../properties/visible-element-assl.md), [AttributeID](../properties/id-element-assl.md)|  
|Elementos derivados|[Atributo](../objects/attribute-element-assl.md) ([atributos](../collections/attributes-element-assl.md) coleção de [CubeDimension](dimension-data-type-assl.md))|  
  
## <a name="remarks"></a>Comentários  
 O elemento *AttributeHierarchyOptimizedState* não tem suporte ao executar o serviço nos valores 1 ou 2 da propriedade de configuração do DeploymentMode (modos SharePoint ou Tabular, usados para executar o PowerPivot e os bancos de dados de modelo de tabela).  
  
 Um atributo não pode ser adicionado como um nível de uma hierarquia quando a propriedade, *AtttributeHierarchyEnabled*, é definida como FALSE e a instância está operando com os valores de propriedade de configuração DeploymentMode de 1 ou 2 (modo de servidor SharePoint ou tabular).  
  
 Os atributos na [CubeDimension](dimension-data-type-assl.md) elemento que não estão explicitamente incluídos na [atributos](../collections/attributes-element-assl.md) parte da coleção tornam-se da coleção com valores padrão atribuídos a eles. Após os atributos são adicionados à coleção, os atributos podem ser retornados pela [Discover](../../xmla/xml-elements-methods-discover.md) método.  
  
 O [AggregationUsage](../properties/aggregationusage-element-assl.md) controles de elemento como [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] projeta agregações automaticamente para o atributo. O elemento `AggregationUsage` não limita nenhuma agregação que é criada manualmente para o cubo.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.CubeAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
