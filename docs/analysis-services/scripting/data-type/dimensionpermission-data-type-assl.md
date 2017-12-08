---
title: Tipo de dados DimensionPermission (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
apiname: DimensionPermission Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DimensionPermission data type
ms.assetid: 066405ff-903f-467a-b0d5-e58653952c52
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d0cafbd3a0c86682d3993a5e32547d0430b751a1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="dimensionpermission-data-type-assl"></a>Tipo de dados DimensionPermission (ASSL)
  Define um tipo de dados derivado que representa as permissões atribuídas a uma dimensão de banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionPermission>  
   <!-- The following elements extend Permission -->  
   <AttributePermissions>...</AttributePermissions>  
   <AllowedRowsExpression>...</AllowedRowsExpression>  
</DimensionPermission>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|[Permissão](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|Tipos de dados derivados|Nenhuma|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|[AttributePermissions](../../../analysis-services/scripting/collections/attributepermissions-element-assl.md), [AllowedRowsExpression](../../../analysis-services/scripting/collections/attributepermissions-element-assl.md)|  
|Elementos derivados|[DimensionPermission](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 Este elemento tem as validações a seguir no valor 2 DeploymentMode (modo de servidor de tabela).  
  
-   O atributo*AttributePermission* deve ser vazio ou um erro ocorre.  
  
 Este elemento tem as validações a seguir no valor 0 DeploymentMode (OLAP).  
  
-   O atributo*AllowedRowsExpression* deve ser vazio ou um erro ocorre.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.DimensionPermission>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script &#40; do Analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
