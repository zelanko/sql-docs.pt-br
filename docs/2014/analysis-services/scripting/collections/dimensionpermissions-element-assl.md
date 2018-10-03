---
title: Elemento DimensionPermissions (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DimensionPermissions Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DimensionPermissions
helpviewer_keywords:
- DimensionPermissions element
ms.assetid: cb9fdfbf-2118-423b-ba02-fa36813dbea0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: af96e23a71064cb1d68c292f4224ee76b8395588
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48068726"
---
# <a name="dimensionpermissions-element-assl"></a>Elemento DimensionPermissions (ASSL)
  Contém a coleção de permissões aplicáveis a um [dimensão](../objects/dimension-element-assl.md) elemento ou um [CubePermission](../objects/cubepermission-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Dimension> <!-- or CubePermission -->  
   ...  
   <DimensionPermissions>  
            <DimensionPermission>...</DimensionPermission> <!-- parent: Dimension -->  
      <!-- or -->  
      <DimensionPermission xsi:type="CubeDimensionPermission">...</DimensionPermission> <!-- parent: CubePermission -->  
      </DimensionPermissions>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|None|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[CubePermission](../objects/cubepermission-element-assl.md), [dimensão](../objects/dimension-element-assl.md)|  
|Elementos filho|[DimensionPermission](../objects/dimensionpermission-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 Para elementos `CubePermission`, os elementos `DimensionPermission` nessa coleção substituem as permissões especificadas na coleção `DimensionPermissions` de cada dimensão mencionada explicitamente. Se uma dimensão não for mencionada nessa coleção, o elemento `CubePermission` herda as permissões especificadas na coleção  `DimensionPermissions` de dimensão.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.DimensionPermissionCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Coleções &#40;ASSL&#41;](collections-assl.md)  
  
  
