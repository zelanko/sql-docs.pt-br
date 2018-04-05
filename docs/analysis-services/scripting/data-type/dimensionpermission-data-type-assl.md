---
title: Tipo de dados DimensionPermission (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- DimensionPermission Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DimensionPermission data type
ms.assetid: 066405ff-903f-467a-b0d5-e58653952c52
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: da9bbbd41c8c36170146b9798830ae63463c894d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="dimensionpermission-data-type-assl"></a>Tipo de dados DimensionPermission (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Define um tipo de dados derivado que representa as permissões atribuídas a uma dimensão de banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionPermission>  
   <!-- The following elements extend Permission -->  
   <AttributePermissions>...</AttributePermissions>  
   <AllowedRowsExpression>...</AllowedRowsExpression>  
</DimensionPermission>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|[Permissão](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|Tipos de dados derivados|Nenhum|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|[AttributePermissions](../../../analysis-services/scripting/collections/attributepermissions-element-assl.md), [AllowedRowsExpression](../../../analysis-services/scripting/collections/attributepermissions-element-assl.md)|  
|Elementos derivados|[DimensionPermission](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Este elemento tem as validações a seguir no valor 2 DeploymentMode (modo de servidor de tabela).  
  
-   O atributo*AttributePermission* deve ser vazio ou um erro ocorre.  
  
 Este elemento tem as validações a seguir no valor 0 DeploymentMode (OLAP).  
  
-   O atributo*AllowedRowsExpression* deve ser vazio ou um erro ocorre.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.DimensionPermission>.  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados XML de linguagem de script &#40; do Analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
