---
title: sys. dm_pdw_component_health_active_alerts (Transact-SQL
ms.custom: seo-dt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: c53e4a36-b841-424a-b8e2-255b1878deb6
author: stevestein
ms.author: sstein
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 90531889d3e510d342ff39abdf069f75f3c371aa
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401709"
---
# <a name="sysdm_pdw_component_health_active_alerts-transact-sql"></a>sys. dm_pdw_component_health_active_alerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Armazena alertas ativos em [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] componentes.  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**inteiro**|Identificador exclusivo de um [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] nó.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id e alert_instance_id formam a chave para essa exibição.|NOT NULL|  
|component_id|**inteiro**|A ID do componente. Consulte [Sys. pdw_health_components &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id e alert_instance_id formam a chave para essa exibição.|NOT NULL|  
|component_instance_id|**nvarchar (255)**|pdw_node_id, component_id, component_instance_id, alert_id e alert_instance_id formam a chave para essa exibição.|NOT NULL|  
|alert_id|**inteiro**|A ID do tipo de alerta. Consulte [Sys. pdw_health_alerts &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md).<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id e alert_instance_id formam a chave para essa exibição.|NOT NULL|  
|alert_instance_id|**nvarchar (36)**|Identifica uma instância de um determinado alerta.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id e alert_instance_id formam a chave para essa exibição.|NOT NULL|  
|current_value|**nvarchar (255)**|Usado quando o alerta é do tipo StatusChange. Este é o status atual do componente. O valor é nulo para alertas do tipo limite. Consulte [Sys. pdw_health_alerts &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) para obter uma lista de tipos de alertas.|NULO|  
|previous_value|**nvarchar (255)**|Usado quando o alerta é do tipo StatusChange. Este é o status do componente anterior. O valor é nulo para alertas do tipo limite. Consulte [Sys. pdw_health_alerts &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) para obter uma lista de tipos de alertas.|NULO|  
|create_time|**horário**|Hora e data em que o alerta foi gerado.|NOT NULL|  
  
 Para obter informações sobre o máximo de linhas retidas por essa exibição, consulte "valores mínimos e [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]máximos" no.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico de SQL Data Warehouse e paralelo data warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
