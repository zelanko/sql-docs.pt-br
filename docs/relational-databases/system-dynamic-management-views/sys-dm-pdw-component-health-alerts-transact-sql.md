---
description: sys. dm_pdw_component_health_alerts (Transact-SQL)
title: sys. dm_pdw_component_health_alerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 88f05392-1e97-4693-ba60-a4910af3c000
author: markingmyname
ms.author: maghan
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1394d13bae5cc86fde37424925f259ce88b8c97d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89531160"
---
# <a name="sysdm_pdw_component_health_alerts-transact-sql"></a>sys. dm_pdw_component_health_alerts (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Armazena alertas emitidos anteriormente em componentes de dispositivo.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Identificador exclusivo de um [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] nó.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id e alert_instance_id formam a chave para essa exibição.|NOT NULL|  
|component_id|**int**|A ID do componente. Consulte [Sys. pdw_health_components &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id e alert_instance_id formam a chave para essa exibição.|NOT NULL|  
|component_instance_id|**nvarchar(255)**|pdw_node_id, component_id, component_instance_id, alert_id e alert_instance_id formam a chave para essa exibição.|NOT NULL|  
|alert_id|**int**|A ID do tipo de alerta. Consulte [Sys. pdw_health_alerts &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md).<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id e alert_instance_id formam a chave para essa exibição.|NOT NULL|  
|alert_instance_id|**nvarchar (36)**|Identifica uma instância de um determinado alerta.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id e alert_instance_id formam a chave para essa exibição.|NOT NULL|  
|previous_value|**nvarchar(255)**|Usado quando o alerta é do tipo StatusChange. Este é o status do componente anterior. O valor é nulo para alertas do tipo limite. Consulte [Sys. pdw_health_alerts &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) para obter uma lista de tipos de alertas.|NULO|  
|current_value|**nvarchar(255)**|Usado quando o alerta é do tipo StatusChange. Este é o status atual do componente. O valor é nulo para alertas do tipo limite. Consulte [Sys. pdw_health_alerts &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) para obter uma lista de tipos de alertas.|NULO|  
|create_time|**datetime**|Hora e data em que o alerta foi gerado.|NOT NULL|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico de SQL Data Warehouse e paralelo data warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
