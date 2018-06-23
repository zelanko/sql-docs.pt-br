---
title: Elemento MiningModelPermissions (ASSL) | Microsoft Docs
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
- MiningModelPermissions Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningModelPermissions
helpviewer_keywords:
- MiningModelPermissions element
ms.assetid: 6cbcf029-9627-4839-9fc5-15e58e1ba0c3
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 701a5e139f3a5f2f98799be7dfc5f6dec1db3ced
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117988"
---
# <a name="miningmodelpermissions-element-assl"></a>Elemento MiningModelPermissions (ASSL)
  Contém a coleção de permissões para um [MiningModel](../objects/miningmodel-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningModel>  
   ...  
   <MiningModelPermissions>  
      <MiningModelPermission xsi:type="Permission">...</MiningModelPermission>  
   </MiningModelPermissions>  
   ...  
</MiningModel>  
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
|Elementos pai|[MiningModel](../objects/miningmodel-element-assl.md)|  
|Elementos filho|[MiningModelPermission](../objects/miningmodelpermission-element-assl.md) do tipo [permissão](../data-type/permission-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.MiningModelPermissionCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados Permission &#40;ASSL&#41;](../data-type/permission-data-type-assl.md)   
 [Coleções &#40;ASSL&#41;](collections-assl.md)  
  
  