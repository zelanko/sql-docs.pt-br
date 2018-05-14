---
title: Elemento DefaultMember (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: aad56fe9918235afb24a8f8f56bf98715964125a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="defaultmember-element-assl"></a>Elemento DefaultMember (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
## <a name="remarks"></a>Remarks  
 O elemento **DefaultMember** define o membro padrão para o elemento pai. Se **DefaultMember** não for especificado ou é definido como uma cadeia de caracteres vazia, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] escolherá um membro a ser usado como o membro padrão.  
  
 Para elementos **ManyToManyMeasureGroupDimension** , o elemento **DefaultMember** contém uma expressão MDC que especifica um membro na dimensão especificada no elemento **CubeDimensionID** do **ManyToManyMeasureGroupDimension**. A expressão MDX é semelhante do [StrToMember](../../../mdx/strtomember-mdx.md) função MDX com a palavra-chave CONSTRAINED, em que ele não pode incluir funções MDX ou definidas pelo usuário.  
  
 Para obter mais informações sobre membros padrão, consulte [Definir um membro padrão](../../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md).  
  
 Os elementos que correspondem aos pais de **DefaultMember** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.AttributePermission>, <xref:Microsoft.AnalysisServices.DimensionAttribute>, e <xref:Microsoft.AnalysisServices.PerspectiveAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
