---
title: sys.elastic_pool_resource_stats (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology: system-objects
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
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 5f7f13ebb5699fc0fe2174e7ee1af9d6c44bcbfb
ms.sourcegitcommit: b8e2e3e6e04368aac54100c403cc15fd4e4ec13a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45563262"
---
# <a name="syselasticpoolresourcestats-azure-sql-database"></a>sys.elastic_pool_resource_stats (banco de dados SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna estatísticas de uso de recursos de todos os pools de banco de dados Elástico em um servidor lógico. Para cada pool de banco de dados Elástico, há uma linha para cada janela (quatro linhas por minuto) de relatórios de 15 segundos. Isso inclui a CPU, IO, Log, consumo de armazenamento e utilização de solicitações/sessões simultâneas por todos os bancos de dados no pool. Estes dados são retidos por 14 dias. 
  
||  
|-|  
|**Aplica-se ao**: [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12.|  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**start_time**|**datetime2**|Hora UTC que indica o início da segunda 15 intervalo de relatório.|  
|**end_time**|**datetime2**|Hora UTC que indica o final do segundo 15 intervalo de relatório.|  
|**elastic_pool_name**|**nvarchar(128)**|Nome do pool Elástico do banco de dados.|  
|**avg_cpu_percent**|**decimal(5,2)**|Média de utilização em porcentagem do limite do pool de computação.|  
|**avg_data_io_percent**|**decimal(5,2)**|Utilização média de e/s em percentagem com base no limite do pool.|  
|**avg_log_write_percent**|**decimal(5,2)**|Média de utilização de recursos de gravação em percentual do limite do pool.|  
|**avg_storage_percent**|**decimal(5,2)**|Média de utilização de armazenamento em percentual do limite do pool de armazenamento.|  
|**max_worker_percent**|**decimal(5,2)**|Máximo de trabalhos simultâneos (solicitações) em porcentagem do limite do pool.|  
|**max_session_percent**|**decimal(5,2)**|Máximo de sessões simultâneas em percentual, com base no limite do pool.|  
|**elastic_pool_dtu_limit**|**int**|Máximo do pool Elástico DTU configuração atual para este pool Elástico durante este intervalo.|  
|**elastic_pool_storage_limit_mb**|**bigint**|Limite de armazenamento máximo do pool Elástico atual configuração para este pool Elástico em megabytes durante este intervalo.|
|**avg_allocated_storage_percent**|**decimal(5,2)**|A porcentagem de espaço de dados alocado por todos os bancos de dados no pool Elástico.  Esta é a razão do espaço de dados alocado para o tamanho máximo dos dados para o pool Elástico.  Para obter mais informações, consulte: [gerenciamento de espaço de arquivo no banco de dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-file-space-management)|  
  
## <a name="remarks"></a>Comentários  
 Essa exibição existe no banco de dados mestre do servidor lógico. Você deve estar conectado ao banco de dados mestre para consultar **sys.elastic_pool_resource_stats**.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na **dbmanager** função.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna os dados de utilização de recursos ordenados pelo tempo mais recente de todos os pools de banco de dados Elástico no servidor lógico atual.  
  
```  
SELECT * FROM sys.elastic_pool_resource_stats   
ORDER BY end_time DESC;  
```  
  
 O exemplo a seguir calcula o consumo médio de porcentagem DTU para um determinado pool.  
  
```  
SELECT start_time, end_time,      
  (SELECT Max(v)      
FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS value(v)) AS [avg_DTU_percent]    
FROM sys.elastic_pool_resource_stats   
WHERE elastic_pool_name = '<your pool name>'   
ORDER BY end_time DESC;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Controle o crescimento explosivo com bancos de dados Elásticos](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)   
 [Criar e gerenciar um pool de banco de dados Elástico do banco de dados SQL (versão prévia)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)   
 [sys. resource_stats &#40;banco de dados SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [sys.DM db_resource_stats &#40;banco de dados SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)  
  
  
