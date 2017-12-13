---
title: Elemento DatabasePermissions (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DatabasePermissions Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DatabasePermissions
helpviewer_keywords: DatabasePermissions element
ms.assetid: c4ce0da3-f7ba-4f11-8cd8-236c32992aaf
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b72d1de3108d0209c4d9a45818d13d27e09c5663
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="databasepermissions-element-assl"></a>Elemento DatabasePermissions (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém a coleção de [DatabasePermission](../../../analysis-services/scripting/objects/databasepermission-element-assl.md) elementos associados a um [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Database>  
   ...  
   <DatabasePermissions>  
      <DatabasePermission>...</DatabasePermission>  
      </DatabasePermissions>  
      ...  
</Database>  
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
|Elementos pai|[Banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md)|  
|Elementos filho|[DatabasePermission](../../../analysis-services/scripting/objects/databasepermission-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.DatabasePermissionCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de permissão de dados &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)   
 [Coleções de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
