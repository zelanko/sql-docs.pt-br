---
title: Elemento DefaultMember (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DefaultMember Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DefaultMember
helpviewer_keywords:
- DefaultMember element
ms.assetid: db4eea9f-f7cf-40de-abd0-b62014e7ec2d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6c90abe48fc1d3bfa099e39234d22df822a03782
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48055287"
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[AttributePermission](../objects/attributepermission-element-assl.md), [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [ManyToManyMeasureGroupDimension](../data-type/dimension-data-type-assl.md), [PerspectiveAttribute](../data-type/perspectiveattribute-data-type-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O elemento `DefaultMember` define o membro padrão para o elemento pai. Se `DefaultMember` não for especificado ou é definido como uma cadeia de caracteres vazia [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] escolherá um membro a ser usado como o membro padrão.  
  
 Para elementos `ManyToManyMeasureGroupDimension`, o elemento `DefaultMember` contém uma expressão MDC que especifica um membro na dimensão especificada no elemento `CubeDimensionID` do `ManyToManyMeasureGroupDimension`. A expressão MDX é semelhante para o [StrToMember](/sql/mdx/strtomember-mdx) função MDX com a palavra-chave CONSTRAINED, em que ele não pode incluir funções MDX ou definidas pelo usuário.  
  
 Para obter mais informações sobre membros padrão, consulte [Definir um membro padrão](../../multidimensional-models/attribute-properties-define-a-default-member.md).  
  
 Os elementos que correspondem aos pais de `DefaultMember` no modelo de objeto AMO (Objetos de Gerenciamento de Análise) são <xref:Microsoft.AnalysisServices.AttributePermission>, <xref:Microsoft.AnalysisServices.DimensionAttribute> e <xref:Microsoft.AnalysisServices.PerspectiveAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
