---
title: sys.dm_pdw_component_health_alerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 88f05392-1e97-4693-ba60-a4910af3c000
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 652467f0f40b27f35b4c805a9d646e537d51f040
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47662894"
---
# <a name="sysdmpdwcomponenthealthalerts-transact-sql"></a>sys.dm_pdw_component_health_alerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Repositórios emitido anteriormente alertas sobre componentes do dispositivo.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Identificador exclusivo de um [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] nó.<br /><br /> pdw_node_id, identificação_do_componente, component_instance_id, alert_id e alert_instance_id formam a chave para esta exibição.|NOT NULL|  
|identificação_do_componente|**int**|A ID do componente. Ver [sys.pdw_health_components &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> pdw_node_id, identificação_do_componente, component_instance_id, alert_id e alert_instance_id formam a chave para esta exibição.|NOT NULL|  
|component_instance_id|**nvarchar(255)**|pdw_node_id, identificação_do_componente, component_instance_id, alert_id e alert_instance_id formam a chave para esta exibição.|NOT NULL|  
|alert_id|**int**|A ID para o tipo de alerta. Ver [sys.pdw_health_alerts &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md).<br /><br /> pdw_node_id, identificação_do_componente, component_instance_id, alert_id e alert_instance_id formam a chave para esta exibição.|NOT NULL|  
|alert_instance_id|**nvarchar(36)**|Identifica uma instância de um determinado alerta.<br /><br /> pdw_node_id, identificação_do_componente, component_instance_id, alert_id e alert_instance_id formam a chave para esta exibição.|NOT NULL|  
|previous_value|**nvarchar(255)**|Usado quando o alerta é do tipo StatusChange. Isso é o status do componente anterior. Valor é NULL para alertas do tipo de limite. Ver [sys.pdw_health_alerts &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) para obter uma lista dos tipos de alerta.|NULL|  
|current_value|**nvarchar(255)**|Usado quando o alerta é do tipo StatusChange. Isso é o status do componente atual. Valor é NULL para alertas do tipo de limite. Ver [sys.pdw_health_alerts &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) para obter uma lista dos tipos de alerta.|NULL|  
|create_time|**datetime**|Quando o alerta foi gerado de data e hora.|NOT NULL|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
