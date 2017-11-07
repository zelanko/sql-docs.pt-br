---
title: Tipo de dados CubeAttribute (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- CubeAttribute Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- CubeAttribute
helpviewer_keywords:
- CubeAttribute data type
ms.assetid: 114ffb44-460b-4971-b31b-dd844e960b81
caps.latest.revision: 45
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c04b5602de94ac46b736ebfc878760174ced5a8d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="cubeattribute-data-type-assl"></a>Tipo de dados CubeAttribute (ASSL)
  Define um tipo de dados primitivo que representa um atributo associado a um [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento.  
  
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhuma|  
|Tipos de dados derivados|Nenhuma|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|[AggregationUsage](../../../analysis-services/scripting/properties/aggregationusage-element-assl.md), [anotações](../../../analysis-services/scripting/collections/annotations-element-assl.md), [AttributeHierarchyEnabled](../../../analysis-services/scripting/properties/attributehierarchyenabled-element-assl.md), [AttributeHierarchyOptimizedState](../../../analysis-services/scripting/properties/attributehierarchyoptimizedstate-element-assl.md), [ AttributeHierarchyVisible](../../../analysis-services/scripting/properties/attributehierarchyvisible-element-assl.md), [AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md)|  
|Elementos derivados|[Atributo](../../../analysis-services/scripting/objects/attribute-element-assl.md) ([atributos](../../../analysis-services/scripting/collections/attributes-element-assl.md) coleção de [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md))|  
  
## <a name="remarks"></a>Comentários  
 O *AttributeHierarchyOptimizedState* elemento não é suportado ao executar o serviço em valores de propriedade de configuração DeploymentMode de 1 ou 2 (modos SharePoint ou Tabular, usados para executar [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e modelo de tabela bancos de dados).  
  
 Um atributo não pode ser adicionado como um nível de uma hierarquia quando a propriedade, *AtttributeHierarchyEnabled*, é definida como FALSE e a instância está operando com os valores de propriedade de configuração DeploymentMode de 1 ou 2 (modo de servidor SharePoint ou tabular).  
  
 Atributos no [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md) que não estão explicitamente incluídos no elemento de [atributos](../../../analysis-services/scripting/collections/attributes-element-assl.md) parte da coleção se tornam da coleção com valores padrão atribuídos a eles. Após serem adicionados à coleção, os atributos podem ser retornados pelo [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método.  
  
 O [AggregationUsage](../../../analysis-services/scripting/properties/aggregationusage-element-assl.md) elemento controla como [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] projeta agregações automaticamente para o atributo. O elemento **AggregationUsage** não limita nenhuma agregação que é criada manualmente para o cubo.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.CubeAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script &#40; do Analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

