---
title: Tipo de dados CubeAttribute (ASSL) | Microsoft Docs
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
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: dce594145db99d7edfa991c2e975f62e55d3ef34
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012581"
---
# <a name="cubeattribute-data-type-assl"></a>Tipo de dados CubeAttribute (ASSL)
  Define um tipo de dados primitivo que representa um atributo associado a um [cubo](../objects/cube-element-assl.md) elemento.  
  
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
|Tipos de dados base|Nenhum|  
|Tipos de dados derivados|Nenhum|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|[AggregationUsage](../properties/aggregationusage-element-assl.md), [anotações](../collections/annotations-element-assl.md), [AttributeHierarchyEnabled](../properties/enabled-element-assl.md), [AttributeHierarchyOptimizedState](../properties/state-element-assl.md), [ AttributeHierarchyVisible](../properties/visible-element-assl.md), [AttributeID](../properties/id-element-assl.md)|  
|Elementos derivados|[Atributo](../objects/attribute-element-assl.md) ([atributos](../collections/attributes-element-assl.md) coleção de [CubeDimension](dimension-data-type-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 O elemento *AttributeHierarchyOptimizedState* não tem suporte ao executar o serviço nos valores 1 ou 2 da propriedade de configuração do DeploymentMode (modos SharePoint ou Tabular, usados para executar o PowerPivot e os bancos de dados de modelo de tabela).  
  
 Um atributo não pode ser adicionado como um nível de uma hierarquia quando a propriedade, *AtttributeHierarchyEnabled*, é definida como FALSE e a instância está operando com os valores de propriedade de configuração DeploymentMode de 1 ou 2 (modo de servidor SharePoint ou tabular).  
  
 Atributos no [CubeDimension](dimension-data-type-assl.md) que não estão explicitamente incluídos no elemento de [atributos](../collections/attributes-element-assl.md) parte da coleção se tornam da coleção com valores padrão atribuídos a eles. Após serem adicionados à coleção, os atributos podem ser retornados pelo [Discover](../../xmla/xml-elements-methods-discover.md) método.  
  
 O [AggregationUsage](../properties/aggregationusage-element-assl.md) elemento controla como [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] projeta agregações automaticamente para o atributo. O elemento `AggregationUsage` não limita nenhuma agregação que é criada manualmente para o cubo.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.CubeAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  