---
title: Elemento DataSourcePermissions (ASSL) | Microsoft Docs
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
- DataSourcePermissions Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- DataSourcePermissions element
ms.assetid: 6e1cfbec-65b9-4942-a628-f7f7c891e35f
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 774b06c14bfbd5d7c90c4b2f07d3ff4c40bd746a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121790"
---
# <a name="datasourcepermissions-element-assl"></a>Elemento DataSourcePermissions (ASSL)
  Contém a coleção de [DataSourcePermission](../objects/datasourcepermission-element-assl.md) elementos associados a um [DataSource](../data-type/datasource-data-type-assl.md) tipo de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DataSource>  
   ...  
   <DataSourcePermissions>  
      <DataSourcePermission>...</DataSourcePermission>  
   </DataSourcePermissions>  
   ...  
</DataSource>  
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
|Elementos pai|[Fonte de dados](../data-type/datasource-data-type-assl.md)|  
|Elementos filho|[DataSourcePermission](../objects/datasourcepermission-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados Permission &#40;ASSL&#41;](../data-type/permission-data-type-assl.md)   
 [Coleções &#40;ASSL&#41;](collections-assl.md)  
  
  