---
title: Processar o elemento (ASSL) | Microsoft Docs
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
- Process Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Process
helpviewer_keywords:
- Process element
ms.assetid: 4aa08718-be44-4781-92cf-7b32b20f862c
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f1217cb2ba18a7eaad4b948821b1403e02274fbc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37289442"
---
# <a name="process-element-assl"></a>Elemento Process (ASSL)
  Determina se um usuário pode processar o proprietário do elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Permission> <-- or one of the other elements contained in the Element Relationships table -->  
   ...  
   <Process>...</Process>  
   ...  
</Permission>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Booliano|  
|Valor padrão|Falso|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[CubePermission](../objects/cubepermission-element-assl.md), [DatabasePermission](../objects/databasepermission-element-assl.md), [DimensionPermission](../objects/dimensionpermission-element-assl.md), [MiningModelPermission](../objects/miningmodelpermission-element-assl.md), [MiningStructurePermission ](../objects/miningstructurepermission-element-assl.md), [Permissão](../data-type/permission-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Os elementos que correspondem aos pais de `Process` no modelo de objeto AMO (Objetos de Gerenciamento de Análise) são <xref:Microsoft.AnalysisServices.CubePermission>, <xref:Microsoft.AnalysisServices.DatabasePermission>, <xref:Microsoft.AnalysisServices.DimensionPermission>, <xref:Microsoft.AnalysisServices.MiningModelPermission>, <xref:Microsoft.AnalysisServices.MiningStructurePermission> e <xref:Microsoft.AnalysisServices.Permission>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de função &#40;ASSL&#41;](../objects/role-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
