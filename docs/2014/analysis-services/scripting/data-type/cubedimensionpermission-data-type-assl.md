---
title: Tipo de dados CubeDimensionPermission (ASSL) | Microsoft Docs
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
- CubeDimensionPermission Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeDimensionPermission
helpviewer_keywords:
- CubeDimensionPermission data type
ms.assetid: d9d39859-5f33-48bc-a402-0071755918de
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d215ed3dde22c3d0e16df4cc4d937c9ee3cb0a34
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36005711"
---
# <a name="cubedimensionpermission-data-type-assl"></a>Tipo de dados CubeDimensionPermission (ASSL)
  Define um tipo de dados primitivo que representa as permissões para uma única função em uma dimensão específica em um cubo.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CubeDimensionPermission>  
   <CubeDimensionID>...</CubeDimensionID>  
   <Description>...</Description>  
   <Read>...</Read>  
   <Write>...</Write>  
   <AttributePermissions>...</AttributePermissions>  
   <Annotations>...</Annotations>  
</CubeDimensionPermission>  
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
|Elementos filho|[Anotações](../collections/annotations-element-assl.md), [AttributePermissions](../collections/attributepermissions-element-assl.md), [CubeDimensionID](../properties/id-element-assl.md), [descrição](../properties/description-element-assl.md), [leitura](../properties/read-element-assl.md), [ Gravação](../properties/write-element-assl.md)|  
|Elementos derivados|[DimensionPermission](../objects/dimensionpermission-element-assl.md) ([DimensionPermissions](../collections/dimensionpermissions-element-assl.md) coleção de [dimensão](../objects/dimension-element-assl.md) ou [CubePermission](../objects/cubepermission-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.CubeDimensionPermission>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  