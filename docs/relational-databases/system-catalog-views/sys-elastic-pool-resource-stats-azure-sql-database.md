---
description: sys.elastic_pool_resource_stats (Banco de Dados SQL do Azure)
title: sys.elastic_pool_resource_stats
titleSuffix: Azure SQL Database
ms.date: 01/28/2019
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: reference
f1_keywords:
- sys.elastic_pool_resource_stats catalog view
helpviewer_keywords:
- sys.elastic_pool_resource_stats_TSQL
- sys.elastic_pool_resource_stats
- elastic_pool_resource_stats_TSQL
- elastic_pool_resource_stats
ms.assetid: f242c1bd-3cc8-4c8b-8aaf-c79b6a8a0329
author: markingmyname
ms.author: maghan
ms.custom: seo-dt-2019
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 39db2d1bd2d3525e1dc2902c11e362d70b212ebd
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809852"
---
# <a name="syselastic_pool_resource_stats-azure-sql-database"></a>sys.elastic_pool_resource_stats (Banco de Dados SQL do Azure)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  Retorna estatísticas de uso de recursos de todos os pools elásticos em um servidor do Banco de Dados SQL. Para cada pool elástico, há uma linha para cada janela de relatórios de 15 segundos (quatro linhas por minuto). Isso inclui a utilização de CPU, E/S, log, consumo de armazenamento e solicitações/sessões simultâneas de todos os bancos de dados no pool. Esses dados são mantidos por 14 dias. 
  
||  
|-|  
|**Aplica-se a**:  [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12.|  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**start_time**|**datetime2**|Hora UTC indicando o início do intervalo de relatório de 15 segundos.|  
|**end_time**|**datetime2**|Hora UTC indicando o final do intervalo de relatórios de 15 segundos.|  
|**elastic_pool_name**|**nvarchar(128)**|Nome do pool de banco de dados elástico.|  
|**avg_cpu_percent**|**decimal (5, 2)**|Média de utilização da computação em percentual do limite do pool.|  
|**avg_data_io_percent**|**decimal (5, 2)**|Média de utilização de E/S em percentual do limite do pool.|  
|**avg_log_write_percent**|**decimal (5, 2)**|Média de utilização dos recursos de gravação em percentual do limite do pool.|  
|**avg_storage_percent**|**decimal (5, 2)**|Média de utilização do armazenamento em percentual do limite de armazenamento do pool.|  
|**max_worker_percent**|**decimal (5, 2)**|Máximo de trabalhos (solicitações) simultâneos em percentual, com base no limite do pool.|  
|**max_session_percent**|**decimal (5, 2)**|Número máximo de sessões simultâneas em percentual, com base no limite do pool.|  
|**elastic_pool_dtu_limit**|**int**|Configuração atual de DTUs máximas do pool elástico para este pool elástico durante este intervalo.|  
|**elastic_pool_storage_limit_mb**|**bigint**|Configuração atual de limite máximo de armazenamento do pool elástico para este pool elástico em megabytes durante este intervalo.|
|**avg_allocated_storage_percent**|**decimal (5, 2)**|A porcentagem de espaço de dados alocada por todos os bancos de dado no pool elástico.  Esta é a taxa de espaço de dados alocada para o tamanho máximo de dados para o pool elástico.  Para obter mais informações, consulte: [Gerenciamento de espaço de arquivo no banco de dados SQL](/azure/sql-database/sql-database-file-space-management)|  
  
## <a name="remarks"></a>Comentários

 Essa exibição existe no banco de dados mestre do servidor do banco de dados SQL. Você deve estar conectado ao banco de dados mestre para consultar **Sys.elastic_pool_resource_stats**.  
  
## <a name="permissions"></a>Permissões

 Requer associação na função **DBManager** .  
  
## <a name="examples"></a>Exemplos

 O exemplo a seguir retorna os dados de utilização de recursos ordenados pela hora mais recente para todos os pools de banco de dados elástico no servidor do banco de dados SQL atual.  
  
```sql
SELECT * FROM sys.elastic_pool_resource_stats
ORDER BY end_time DESC;  
```

 O exemplo a seguir calcula o consumo percentual médio de DTU para um determinado pool.  

```sql
SELECT start_time, end_time,
  (SELECT Max(v)
FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS value(v)) AS [avg_DTU_percent]
FROM sys.elastic_pool_resource_stats
WHERE elastic_pool_name = '<your pool name>'
ORDER BY end_time DESC;  
```

## <a name="see-also"></a>Consulte Também

 [Controle o crescimento explosivo com bancos de dados elásticos](/azure/azure-sql/database/elastic-pool-overview)   
 [Criar e gerenciar um pool de banco de dados elástico do banco de dados SQL](/azure/azure-sql/database/elastic-pool-overview)   
 [sys.resource_stats &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [sys.dm_db_resource_stats &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)  
  
