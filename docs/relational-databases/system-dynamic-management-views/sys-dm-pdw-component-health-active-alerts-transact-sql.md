---
title: sys.dm_pdw_component_health_active_alerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c53e4a36-b841-424a-b8e2-255b1878deb6
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f236e451d155c88b9ceda2b1b09bbed112b8f79b
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmpdwcomponenthealthactivealerts-transact-sql"></a>sys.dm_pdw_component_health_active_alerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Armazena alertas ativos em [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] componentes.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**Int**|Identificador exclusivo de um [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] nó.<br /><br /> pdw_node_id, identificação_do_componente, component_instance_id, alert_id e alert_instance_id formam a chave para este modo de exibição.|NOT NULL|  
|identificação_do_componente|**Int**|A ID do componente. Consulte [sys.pdw_health_components &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> pdw_node_id, identificação_do_componente, component_instance_id, alert_id e alert_instance_id formam a chave para este modo de exibição.|NOT NULL|  
|component_instance_id|**nvarchar(255)**|pdw_node_id, identificação_do_componente, component_instance_id, alert_id e alert_instance_id formam a chave para este modo de exibição.|NOT NULL|  
|alert_id|**Int**|A ID para o tipo de alerta. Consulte [sys.pdw_health_alerts &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md).<br /><br /> pdw_node_id, identificação_do_componente, component_instance_id, alert_id e alert_instance_id formam a chave para este modo de exibição.|NOT NULL|  
|alert_instance_id|**nvarchar(36)**|Identifica uma instância de um determinado alerta.<br /><br /> pdw_node_id, identificação_do_componente, component_instance_id, alert_id e alert_instance_id formam a chave para este modo de exibição.|NOT NULL|  
|current_value|**nvarchar(255)**|Usado quando o alerta é do tipo StatusChange. Este é o status atual do componente. Valor é NULL para alertas do tipo de limite. Consulte [sys.pdw_health_alerts &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) para obter uma lista de tipos de alertas.|NULL|  
|previous_value|**nvarchar(255)**|Usado quando o alerta é do tipo StatusChange. Este é o status do componente anterior. Valor é NULL para alertas do tipo de limite. Consulte [sys.pdw_health_alerts &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) para obter uma lista de tipos de alertas.|NULL|  
|create_time|**datetime**|Hora e data em que o alerta foi gerado.|NOT NULL|  
  
 Para obter informações sobre o máximo de linhas mantido por esta exibição, consulte "Mínimo e máximo valores" a [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse Parallel Data Warehouse e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
