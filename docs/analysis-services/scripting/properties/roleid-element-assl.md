---
title: Elemento RoleID (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- RoleID Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- RoleID
helpviewer_keywords:
- RoleID element
ms.assetid: 811e24c9-c732-41f9-bd5f-5c9e3503706a
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2892763b1c4dea2f3bc51e81bf91ba44b0232cb3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="roleid-element-assl"></a>Elemento RoleID (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Identifica a função para a qual permissões estão estando definidas.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Permission> <!-- or one of the listed below in the Element Relationships table -->  
   ...  
   <RoleID>...</RoleID>  
   ...  
</Permission>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md), [DatabasePermission](../../../analysis-services/scripting/objects/databasepermission-element-assl.md), [DimensionPermission](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md), [MiningModelPermission](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md), [MiningStructurePermission ](../../../analysis-services/scripting/objects/miningstructurepermission-element-assl.md), [Permissão](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 Os elementos que correspondem aos pais de **RoleID** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.CubePermission>, <xref:Microsoft.AnalysisServices.DatabasePermission>, <xref:Microsoft.AnalysisServices.DimensionPermission>, <xref:Microsoft.AnalysisServices.MiningModelPermission>, <xref:Microsoft.AnalysisServices.MiningStructurePermission>, e <xref:Microsoft.AnalysisServices.Permission>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
