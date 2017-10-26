---
title: Elemento DefaultMember (ASSL) | Microsoft Docs
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
- DefaultMember Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DefaultMember
helpviewer_keywords:
- DefaultMember element
ms.assetid: db4eea9f-f7cf-40de-abd0-b62014e7ec2d
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 411fbf97001ee719e144edfdd6de685e984da021
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="defaultmember-element-assl"></a>Elemento DefaultMember (ASSL)
  Contém uma linguagem MDX que identifica o membro padrão do elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AttributePermission> <!-- or DimensionAttribute, ManyToManyMeasureGroupDimension, PerspectiveAttribute -->  
      ...  
   <DefaultMember>...</DefaultMember>  
      ...  
</AttributePermission>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[AttributePermission](../../../analysis-services/scripting/objects/attributepermission-element-assl.md), [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [ManyToManyMeasureGroupDimension](../../../analysis-services/scripting/data-type/manytomanymeasuregroupdimension-data-type-assl.md), [PerspectiveAttribute](../../../analysis-services/scripting/data-type/perspectiveattribute-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O elemento **DefaultMember** define o membro padrão para o elemento pai. Se **DefaultMember** não for especificado ou é definido como uma cadeia de caracteres vazia, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] escolherá um membro a ser usado como o membro padrão.  
  
 Para elementos **ManyToManyMeasureGroupDimension** , o elemento **DefaultMember** contém uma expressão MDC que especifica um membro na dimensão especificada no elemento **CubeDimensionID** do **ManyToManyMeasureGroupDimension**. A expressão MDX é semelhante do [StrToMember](../../../mdx/strtomember-mdx.md) função MDX com a palavra-chave CONSTRAINED, em que ele não pode incluir funções MDX ou definidas pelo usuário.  
  
 Para obter mais informações sobre membros padrão, consulte [Definir um membro padrão](../../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md).  
  
 Os elementos que correspondem aos pais de **DefaultMember** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.AttributePermission>, <xref:Microsoft.AnalysisServices.DimensionAttribute>, e <xref:Microsoft.AnalysisServices.PerspectiveAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

