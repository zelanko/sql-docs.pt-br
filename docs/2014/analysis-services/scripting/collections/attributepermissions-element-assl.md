---
title: Elemento AttributePermissions (ASSL) | Microsoft Docs
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
- AttributePermissions Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AttributePermissions
helpviewer_keywords:
- AttributePermissions element
ms.assetid: ac703177-5936-440e-b1a5-a254a89258bc
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 98869453e0ecd50301e94cf5b7034173fc7a8a5b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37249036"
---
# <a name="attributepermissions-element-assl"></a>Elemento AttributePermissions (ASSL)
  Contém a coleção de permissões de atributo de um indivíduo [função](../objects/role-element-assl.md) elemento em uma dimensão específica de um [cubo](../objects/cube-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CubeDimensionPermission> <!-- or DimensionPermission -->  
   <AttributePermissions>  
      <AttributePermission>...</AttributePermission>  
      </AttributePermissions>  
</CubeDimensionPermission>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[CubeDimensionPermission](../data-type/permission-data-type-assl.md), [DimensionPermission](../objects/dimensionpermission-element-assl.md)|  
|Elementos filho|[AttributePermission](../objects/attributepermission-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Para `DimensionPermission`, essa coleção pode conter só um `AttributePermission` por atributo.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.AttributePermissionCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados Permission &#40;ASSL&#41;](../data-type/permission-data-type-assl.md)   
 [Coleções &#40;ASSL&#41;](collections-assl.md)  
  
  
