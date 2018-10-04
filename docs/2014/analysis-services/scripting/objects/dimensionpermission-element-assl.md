---
title: Elemento DimensionPermission (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DimensionPermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DimensionPermission
helpviewer_keywords:
- DimensionPermission element
ms.assetid: e06efbda-64fd-4dca-a2b5-c8ffbf21512c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 416755e486ce7acadb1ff43926aeeb4b50a56c04
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48225958"
---
# <a name="dimensionpermission-element-assl"></a>Elemento DimensionPermission (ASSL)
  Define as permissões que pertencem a um determinado [função](role-element-assl.md) elemento para uma dimensão de banco de dados específico ou a dimensão do cubo.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionPermissions>  
   <DimensionPermission xsi:type="DimensionPermission">...</DimensionPermission> <!-- ancestor: Dimension -->  
   <!-- or -->  
   <DimensionPermission xsi:type="CubeDimensionPermission">...</DimensionPermission> <!-- ancestor: CubePermission -->  
</DimensionPermissions>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados||  
|Valor padrão|None|  
|Cardinalidade|0-n: elemento opcional que pode ocorrer uma vez ou mais.|  
  
|Ancestral ou pai|Tipo de Dados|  
|------------------------|---------------|  
|[Dimension](../data-type/permission-data-type-assl.md)|  
|[CubePermission](../data-type/cubedimensionpermission-data-type-assl.md)|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[DimensionPermissions](../collections/dimensionpermissions-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 Os elementos correspondentes no modelo de objeto AMO (Objetos de Gerenciamento de Análise) são <xref:Microsoft.AnalysisServices.DimensionPermission> e <xref:Microsoft.AnalysisServices.CubeDimensionPermission>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
