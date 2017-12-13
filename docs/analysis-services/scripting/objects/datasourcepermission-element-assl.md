---
title: Elemento DataSourcePermission (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
apiname: DataSourcePermission Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DataSourcePermission element
ms.assetid: 6dc6fb13-034e-479a-902e-27f3fb78c33f
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 642966c03fc114cec097ee409f265c58c1aa8cf2
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="datasourcepermission-element-assl"></a>Elemento DataSourcePermission (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Define as permissões padrão em uma [DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md) tipo de dados para um determinado [função](../../../analysis-services/scripting/objects/role-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DataSourcePermissions>  
   <DataSourcePermission xsi:type="Permission">  
      <!-- No child elements other than those from Permission are defined -->  
...</DataSourcePermission>  
</DataSourcePermissions>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[Permissão](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: elemento opcional que pode ocorrer uma vez ou mais.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[DataSourcePermissions](../../../analysis-services/scripting/collections/datasourcepermissions-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Os objetos**DataSourcePermission** podem existir somente para as funções possuídas pelo banco de dados e somente um objeto **DataSourcePermission** pode existir para qualquer função.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Role &#40; ASSL &#41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
