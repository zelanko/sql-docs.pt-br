---
title: Monitorar com exibições do sistema
description: Este artigo lista as exibições do sistema que você pode usar para monitorar o dispositivo de sistema de plataforma de análise.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 1979d5e698747e6104f7e743108cc1553de702e5
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400950"
---
# <a name="monitor-the-appliance-with-system-views---analytics-platform-system"></a>Monitorar o dispositivo com exibições do sistema – Analytics Platform System
Este artigo lista as exibições do sistema que você pode usar para monitorar SQL Server PDW.  
  
## <a name="to-monitor-the-appliance-by-using-system-views"></a>Para monitorar o dispositivo usando exibições do sistema  
O SQL Server PDW inclui exibições de sistema abrangentes que permitem que você obtenha informações detalhadas sobre a integridade, o estado e o desempenho do dispositivo. Esta tabela fornece links para exibições do sistema que podem ser usadas para cada recurso de monitoramento.  
  
![Alertas de exibições do sistema do PDW](./media/monitor-the-appliance-by-using-system-views/PDW_system_views_alerts.png "PDW_system_views_alerts")  
  
|||  
|-|-|  
|**Information Type**|**Exibições do sistema relacionadas**|  
|Status geral do dispositivo|[sys. dm_pdw_sys_info](../relational-databases/system-dynamic-management-views/sys-dm-pdw-sys-info-transact-sql.md)|  
|Alertas|[sys.pdw_health_alerts](../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)<br /><br />[sys.dm_pdw_component_health_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-alerts-transact-sql.md)<br /><br />[sys. dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)<br /><br />[sys.dm_pdw_component_health_status](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)|  
|Componentes do dispositivo e seu status|[sys.pdw_health_component_groups](../relational-databases/system-catalog-views/sys-pdw-health-component-groups-transact-sql.md)<br /><br />[sys.pdw_health_components](../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)<br /><br />[sys.pdw_health_component_properties](../relational-databases/system-catalog-views/sys-pdw-health-component-properties-transact-sql.md)<br /><br />[sys.pdw_health_component_status_mappings](../relational-databases/system-catalog-views/sys-pdw-health-component-status-mappings-transact-sql.md)<br /><br />[sys. dm_pdw_nodes](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)|  
|Monitorar solicitações (incluindo consultas, carregamentos, backups e restaurações)|[sys. dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)<br /><br />[sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)<br /><br />[sys.dm_pdw_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)<br /><br />[sys. dm_pdw_sql_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-sql-requests-transact-sql.md)<br /><br />[sys.dm_pdw_dms_workers](../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md)<br /><br />[sys. dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)<br /><br />[sys. dm_pdw_errors](../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)<br /><br />[sys. pdw_distributions](../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)|  
|Monitore informações adicionais para cargas, backups e restaurações.|[sys. pdw_loader_backup_runs](../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)<br /><br />[sys. pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)<br /><br />[sys.pdw_loader_run_stages](../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)|  
|Informações de desempenho e logs no nível do sistema operacional|[sys.dm_pdw_os_performance_counters](../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-performance-counters-transact-sql.md)<br /><br />[sys.dm_pdw_os_event_logs](../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-event-logs-transact-sql.md)<br /><br />[sys. dm_pdw_os_threads](../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-threads-transact-sql.md)|  
  
## <a name="see-also"></a>Consulte Também  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Monitoramento de dispositivo &#40;o sistema de plataforma de análise&#41;](appliance-monitoring.md)  
  
