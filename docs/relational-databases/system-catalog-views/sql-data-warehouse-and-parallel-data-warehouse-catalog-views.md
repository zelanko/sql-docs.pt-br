---
description: Exibições de Catálogo do Azure Synapse Analytics e do Parallel Data Warehouse
title: Exibições do catálogo
titleSuffix: Azure Synapse Analytics and Parallel Data Warehouse
ms.date: 10/29/2019
ms.service: sql-data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ef6f58e2-0162-4bb2-951a-a786da7453e4
author: julieMSFT
ms.author: jrasnick
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.custom: seo-dt-2019
ms.openlocfilehash: 8ff25c5988b3e989be11758591af1f69f778b72f
ms.sourcegitcommit: 76ab3b57718341c6057613c9bd38cf82fb17786e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92059574"
---
# <a name="azure-synapse-analytics-and-parallel-data-warehouse-catalog-views"></a>Exibições de Catálogo do Azure Synapse Analytics e do Parallel Data Warehouse

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

 Este tópico lista as [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] exibições do catálogo e do.  
  
## <a name="sssdw-and-sspdw-catalog-views"></a>Exibições do catálogo do [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 As exibições de catálogo a seguir se aplicam a [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] :  
  
 [&#41;&#40;Transact-SQL de sys.pdw_column_distribution_properties ](../../relational-databases/system-catalog-views/sys-pdw-column-distribution-properties-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.pdw_distributions ](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.pdw_index_mappings ](../../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md)  
  
 [sys.pdw_loader_backup_run_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
 [sys.pdw_loader_backup_runs &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.pdw_nodes_column_store_dictionaries ](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.pdw_nodes_column_store_row_groups ](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.pdw_nodes_column_store_segments ](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-segments-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.pdw_nodes_columns ](../../relational-databases/system-catalog-views/sys-pdw-nodes-columns-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.pdw_nodes_indexes ](../../relational-databases/system-catalog-views/sys-pdw-nodes-indexes-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.pdw_nodes_partitions ](../../relational-databases/system-catalog-views/sys-pdw-nodes-partitions-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.pdw_nodes_pdw_physical_databases ](../../relational-databases/system-catalog-views/sys-pdw-nodes-pdw-physical-databases-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.pdw_nodes_tables ](../../relational-databases/system-catalog-views/sys-pdw-nodes-tables-transact-sql.md) 

 [sys.pdw_replicated_table_cache_state (Transact-SQL)](sys-pdw-replicated-table-cache-state-transact-sql.md) 
  
 [&#41;&#40;Transact-SQL de sys.pdw_table_distribution_properties ](../../relational-databases/system-catalog-views/sys-pdw-table-distribution-properties-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.pdw_table_mappings ](../../relational-databases/system-catalog-views/sys-pdw-table-mappings-transact-sql.md) 

## <a name="sssdw-catalog-views"></a>[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Exibições do catálogo

 As exibições de catálogo a seguir se aplicam [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] somente a:

 [sys.pdw_materialized_view_column_distribution_properties &#40;Transact-SQL&#41;](./sys-pdw-materialized-view-column-distribution-properties-transact-sql.md?view=azure-sqldw-latest) 

 [sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](./sys-pdw-materialized-view-distribution-properties-transact-sql.md?view=azure-sqldw-latest) 

 [&#41;de &#40;Transact-SQL de sys.pdw_materialized_view_mappings ](./sys-pdw-materialized-view-mappings-transact-sql.md?view=azure-sqldw-latest) (versão prévia)

 [&#41;&#40;Transact-SQL de sys.pdw_permanent_table_mappings ](../../relational-databases/system-catalog-views/sys-pdw-permanent-table-mappings-transact-sql.md)

 [&#41;&#40;Transact-SQL de sys.workload_management_workload_classifier_details ](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifier-details-transact-sql.md)
  
 [&#41;&#40;Transact-SQL de sys.workload_management_workload_classifiers ](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifiers-transact-sql.md)
  
 [&#41;&#40;Transact-SQL de sys.workload_management_workload_groups ](./sys-workload-management-workload-groups-transact-sql.md?view=azure-sqldw-latest)

## <a name="sspdw-catalog-views"></a>[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Exibições do catálogo

 As exibições de catálogo a seguir se aplicam [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] somente a:

 [&#41;&#40;Transact-SQL de sys.pdw_database_mappings ](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.pdw_diag_event_properties ](../../relational-databases/system-catalog-views/sys-pdw-diag-event-properties-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.pdw_diag_events ](../../relational-databases/system-catalog-views/sys-pdw-diag-events-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.pdw_diag_sessions ](../../relational-databases/system-catalog-views/sys-pdw-diag-sessions-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.pdw_health_alerts ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.pdw_health_component_groups ](../../relational-databases/system-catalog-views/sys-pdw-health-component-groups-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.pdw_health_component_properties ](../../relational-databases/system-catalog-views/sys-pdw-health-component-properties-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.pdw_health_component_status_mappings ](../../relational-databases/system-catalog-views/sys-pdw-health-component-status-mappings-transact-sql.md)  
  
 [&#41;&#40;Transact-SQL de sys.pdw_health_components ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)  
  
 [sys.pdw_loader_run_stages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
