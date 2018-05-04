---
title: sys.dm_pdw_component_health_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 68cc3f7a-693c-4d5d-a76b-455352af8d7f
caps.latest.revision: 6
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: eb596110f98610690f2c255d6febd4d9748597e6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmpdwcomponenthealthstatus-transact-sql"></a>sys.dm_pdw_component_health_status (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Contém informações sobre o estado atual dos componentes do dispositivo.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**Int**||Não NULL|  
|identificação_do_componente|int|A ID do componente. Consulte [sys.pdw_health_components &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> pdw_node_id, identificação_do_componente, property_id e component_instance_id formam a chave para este modo de exibição.|Não NULL|  
|property_id|**Int**|A ID da propriedade. Consulte [sys.pdw_health_component_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-component-properties-transact-sql.md).|NOT NULL|  
|component_instance_id|**nvarchar(255)**|Identifica uma instância de um componente. Por exemplo, uma instância de uma CPU pode ser identificada por component_instance_id = 'CPU1'.<br /><br /> pdw_node_id, identificação_do_componente, property_id e component_instance_id formam a chave para este modo de exibição.|NOT NULL|  
|property_value|**nvarchar(255)**|O valor da propriedade atual.|NULL|  
|update_time|**datetime**|A última vez em que a métrica foi atualizada.|NOT NULL|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse Parallel Data Warehouse e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
