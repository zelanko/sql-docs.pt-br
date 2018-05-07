---
title: sys.pdw_health_component_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 66999c0c-dc43-4327-99fb-8366f465e69d
caps.latest.revision: 7
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 60e82089b66ff4a8a4263dd56b9ec2871a92869a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="syspdwhealthcomponentproperties-transact-sql"></a>sys.pdw_health_component_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Armazena as propriedades que descrevem um dispositivo. Algumas propriedades mostram o status do dispositivo e algumas propriedades descrevem o próprio dispositivo.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**Int**|Identificador exclusivo da propriedade de um componente.<br /><br /> property_id e identificação_do_componente formam a chave para este modo de exibição.|NOT NULL|  
|identificação_do_componente|**Int**|A ID do componente. Consulte [sys.pdw_health_components &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> property_id e identificação_do_componente formam a chave para este modo de exibição.|NOT NULL|  
|property_name|**nvarchar(255)**|Nome da propriedade.|NOT NULL|  
|physical_name|**nvarchar(32)**|Nome da propriedade conforme definido pelo fabricante.|NOT NULL|  
|is_key|**bit**|Determina se a instância do dispositivo é exclusivo ou não exclusivo.|NOT NULL<br /><br /> 0 - a instância do dispositivo é exclusiva.<br /><br /> 1 - dispositivo instância não é exclusiva.|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e exibições de catálogo do Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
