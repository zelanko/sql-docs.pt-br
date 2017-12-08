---
title: Elemento CellPermissions (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: CellPermissions Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: CellPermissions
helpviewer_keywords: CellPermissions element
ms.assetid: 4a604f2f-f4c3-42bd-a42b-951263942cc6
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 04b97d86aa822ca18222c061532a96357ef265d7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="cellpermissions-element-assl"></a>Elemento CellPermissions (ASSL)
  Contém a coleção de permissões para células no associado [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CubePermission>  
   ...  
   <CellPermissions>  
      <CellPermission>...</CellPermission>  
   </CellPermissions>  
   ...  
</CubePermission>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md)|  
|Elementos filho|[CellPermission](../../../analysis-services/scripting/objects/cellpermission-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 A coleção pode conter até um **CellPermission** do objeto para cada valor permitido do [acesso](../../../analysis-services/scripting/properties/access-element-assl.md) elemento.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.CellPermissionCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de permissão de dados &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)   
 [Coleções de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
