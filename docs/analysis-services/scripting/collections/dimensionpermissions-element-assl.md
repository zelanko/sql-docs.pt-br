---
title: Elemento DimensionPermissions (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DimensionPermissions Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DimensionPermissions
helpviewer_keywords:
- DimensionPermissions element
ms.assetid: cb9fdfbf-2118-423b-ba02-fa36813dbea0
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d4621358267f2741b87b739e671a0f00874d3862
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="dimensionpermissions-element-assl"></a>Elemento DimensionPermissions (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém a coleção de permissões aplicáveis a um [dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md) elemento ou um [CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md) elemento.  
  
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
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md), [dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|Elementos filho|[DimensionPermission](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Para elementos **CubePermission** , os elementos **DimensionPermission** nessa coleção substituem as permissões especificadas na coleção **DimensionPermissions** de cada dimensão mencionada explicitamente. Se uma dimensão não for mencionada nessa coleção, o elemento **CubePermission** herda as permissões especificadas na coleção **DimensionPermissions** de dimensão.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.DimensionPermissionCollection>.  
  
## <a name="see-also"></a>Consulte Também  
 [Coleções de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
