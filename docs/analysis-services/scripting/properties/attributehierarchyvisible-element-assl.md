---
title: Elemento AttributeHierarchyVisible (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: AttributeHierarchyVisible Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AttributeHierarchyVisible
helpviewer_keywords: AttributeHierarchyVisible element
ms.assetid: a3289a9a-dbd6-43e8-a7ca-ee8a1da92a32
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4a2f17b1949df1acc232ae4103700a6b393cbebd
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="attributehierarchyvisible-element-assl"></a>Elemento AttributeHierarchyVisible (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Determina se a hierarquia de atributo é visível para aplicativos cliente.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttribute> <!-- or CubeAttribute or PerspectiveAttribute -->  
   ...  
   <AttributeHierarchyVisible>...</AttributeHierarchyVisible>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Booliano|  
|Valor padrão|**Verdadeiro**|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[CubeAttribute](../../../analysis-services/scripting/data-type/cubeattribute-data-type-assl.md), [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [PerspectiveAttribute](../../../analysis-services/scripting/data-type/perspectiveattribute-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O elemento **AttributeHierarchyVisible** determina se a hierarquia de atributo associada ao atributo é visível aos aplicativos cliente. Se este elemento for definido como **False**, a hierarquia de atributo ainda poderá ser usada para criar hierarquias definidas pelo usuário e poderá ser consultada pelas instruções MDX (Multidimensional Expressions).  
  
 Os elementos que correspondem aos pais de **AttributeHierarchyVisible** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.CubeAttribute>, <xref:Microsoft.AnalysisServices.DimensionAttribute>, e <xref:Microsoft.AnalysisServices.PerspectiveAttribute>.  
  
## <a name="see-also"></a>Consulte Também  
 [Elemento AttributeHierarchyEnabled &#40; ASSL &#41;](../../../analysis-services/scripting/properties/attributehierarchyenabled-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
