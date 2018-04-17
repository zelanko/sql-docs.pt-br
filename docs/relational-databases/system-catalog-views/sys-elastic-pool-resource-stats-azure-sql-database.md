---
title: sys.elastic_pool_resource_stats (banco de dados do SQL Azure) | Microsoft Docs
ms.custom: ''
ms.date: 04/06/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- Azure SQL Database
f1_keywords:
- sys.elastic_pool_resource_stats catalog view
helpviewer_keywords:
- sys.elastic_pool_resource_stats_TSQL
- sys.elastic_pool_resource_stats
- elastic_pool_resource_stats_TSQL
- elastic_pool_resource_stats
ms.assetid: f242c1bd-3cc8-4c8b-8aaf-c79b6a8a0329
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: c7c1d272d3bcbfd85002624b15a69bd2bc31e0e7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="syselasticpoolresourcestats-azure-sql-database"></a>sys.elastic_pool_resource_stats (banco de dados do SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna estatísticas de uso de recursos de todos os pools de banco de dados Elástico em um servidor lógico. Para cada pool Elástico de banco de dados, há uma linha para cada relatório de janela (quatro linhas por minuto) de 15 segundos. Isso inclui a utilização da CPU, e/s, Log, o consumo de armazenamento e simultâneas/sessão de solicitação por todos os bancos de dados no pool. Esses dados são retidos por 14 dias. 
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12.|  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**start_time**|**datetime2**|Hora UTC que indica o início da segunda 15 intervalo de relatório.|  
|**end_time**|**datetime2**|Hora UTC que indica o final do intervalo de relatório de 15 segundos.|  
|**elastic_pool_name**|**nvarchar(128)**|Nome do pool Elástico de banco de dados.|  
|**avg_cpu_percent**|**decimal(5,2)**|Média de utilização em porcentagem do limite do pool de computação.|  
|**avg_data_io_percent**|**decimal(5,2)**|Utilização média de e/s em percentagem com base no limite do pool.|  
|**avg_log_write_percent**|**decimal(5,2)**|Média de utilização de recursos de gravação em porcentagem do limite do pool de.|  
|**avg_storage_percent**|**decimal(5,2)**|Média de utilização do armazenamento em porcentagem do limite do pool de armazenamento.|  
|**max_worker_percent**|**decimal(5,2)**|Máximo simultâneos trabalhadores (solicitações) em porcentagem com base no limite do pool.|  
|**max_session_percent**|**decimal(5,2)**|Máximo de sessões simultâneas em porcentagem com base no limite do pool.|  
|**elastic_pool_dtu_limit**|**Int**|Máximo do pool Elástico DTU configuração atual para este pool Elástico durante esse intervalo.|  
|**elastic_pool_storage_limit_mb**|**bigint**|Limite de armazenamento máximo do pool Elástico atual configuração para este pool Elástico em megabytes durante esse intervalo.|  
  
## <a name="remarks"></a>Remarks  
 Essa exibição existe no banco de dados mestre do servidor lógico. Você deve estar conectado ao banco de dados mestre para consulta **sys.elastic_pool_resource_stats**.  
  
## <a name="permissions"></a>Permissões  
 Requer a participação no **dbmanager** função.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna os dados de utilização de recursos ordenados pelo tempo mais recente de todos os pools de banco de dados Elástico no servidor lógico atual.  
  
```  
SELECT * FROM sys.elastic_pool_resource_stats   
ORDER BY end_time DESC;  
```  
  
 O exemplo a seguir calcula o consumo médio de percentual DTU para um determinado pool.  
  
```  
SELECT start_time, end_time,      
  (SELECT Max(v)      
FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS value(v)) AS [avg_DTU_percent]    
FROM sys.elastic_pool_resource_stats   
WHERE elastic_pool_name = '<your pool name>'   
ORDER BY end_time DESC;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Crescimento explosivo controlar com bancos de dados Elásticos](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)   
 [Criar e gerenciar um pool de banco de dados Elástico de banco de dados SQL (visualização)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)   
 [sys. resource_stats &#40;banco de dados do SQL Azure&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [sys.DM db_resource_stats &#40;banco de dados do SQL Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)  
  
  
