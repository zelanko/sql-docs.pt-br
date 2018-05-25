---
title: sys.DM db_resource_stats (banco de dados do SQL Azure) | Microsoft Docs
ms.custom: ''
ms.date: 04/06/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_resource_stats
- sys.dm_db_resource_stats_TSQL
- dm_db_resource_stats
- dm_db_resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_resource_stats
- dm_db_resource_stats
ms.assetid: 6e76b39f-236e-4bbf-b0b5-38be190d81e8
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: a91988c36604ce38c7022e6bc111cc1941e43a03
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmdbresourcestats-azure-sql-database"></a>sys.dm_db_resource_stats (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna o consumo de CPU, e/s e memória para um [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] banco de dados. Existe uma linha para cada 15 segundos, mesmo se não houver nenhuma atividade no banco de dados. Dados do histórico são mantidos por uma hora.  
  
|Colunas|Tipo de Dados|Description|  
|-------------|---------------|-----------------|  
|end_time|**datetime**|Hora UTC que indica o término do intervalo de relatório atual.|  
|avg_cpu_percent|**decimal (5,2)**|Utilização média de computação, em porcentagem, do limite da camada de serviço.|  
|avg_data_io_percent|**decimal (5,2)**|Média de dados utilização de e/s em porcentagem do limite da camada de serviço.|  
|avg_log_write_percent|**decimal (5,2)**|Utilização média do recurso de gravação, em porcentagem, do limite da camada de serviço.|  
|avg_memory_usage_percent|**decimal (5,2)**|Utilização média de memória, em porcentagem, do limite da camada de serviço.<br /><br /> Isso inclui a memória usada para o armazenamento de objetos OLTP na memória.|  
|xtp_storage_percent|**decimal (5,2)**|Utilização de armazenamento para OLTP na memória em porcentagem do limite da camada de serviço (no final do intervalo de relatório). Isso inclui a memória usada para o armazenamento dos seguintes objetos OLTP na memória: variáveis de tabela, índices e tabelas com otimização de memória. Ele também inclui a memória usada para processar operações de ALTER TABLE.<br /><br /> Retorna 0 se não for usado o OLTP na memória no banco de dados.|  
|max_worker_percent|**decimal (5,2)**|Máximo simultâneos trabalhadores (solicitações) em porcentagem do limite da camada de serviço do banco de dados.|  
|max_session_percent|**decimal (5,2)**|Máximo de sessões simultâneas em porcentagem do limite da camada de serviço do banco de dados.|  
|dtu_limit|**Int**|Banco de dados max DTU configuração atual para este banco de dados durante esse intervalo. |
|||
  
> [!TIP]  
>  Para obter mais contexto sobre esses limites e as camadas de serviço, consulte os tópicos [camadas de serviço](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/) e [limites e recursos da camada de serviço](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/).  
  
## <a name="permissions"></a>Permissões  
 Essa exibição exige a permissão VIEW DATABASE STATE.  
  
## <a name="remarks"></a>Remarks  
 Os dados retornados por **sys.DM db_resource_stats** é expresso como uma porcentagem do máximo permitido de limites para o nível de desempenho/da camada de serviço que você está executando.
 
 Se o banco de dados fez failover para outro servidor nos últimos 60 minutos, a exibição retornará apenas dados para o tempo pelo qual ele foi o banco de dados primário desde esse failover.  
  
 Para obter uma exibição menos detalhada desses dados, use **sys. resource_stats** exibição do catálogo de **mestre** banco de dados. Essa exibição captura dados a cada 5 minutos e mantém dados históricos por 14 dias.  Para obter mais informações, consulte [sys. resource_stats &#40;banco de dados do SQL Azure&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md).  
  
 Quando um banco de dados é um membro de um pool Elástico, estatísticas de recursos apresentadas como valores de porcentagem são expressas como porcentagem do limite máximo de bancos de dados conforme definido na configuração do pool Elástico.  
  
## <a name="example"></a>Exemplo  
  
O exemplo a seguir retorna os dados de utilização de recursos ordenados pelo tempo mais recente do banco de dados conectado no momento.  
  
```  
SELECT * FROM sys.dm_db_resource_stats ORDER BY end_time DESC;  
  
```  
  
 O exemplo a seguir identifica o consumo médio de DTU para o banco de dados do usuário durante a última hora, em termos de percentual do limite máximo de DTU permitido no nível de desempenho. Considere aumentar o nível de desempenho conforme essas porcentagens se aproximarem de consistentemente de 100%.  
  
```  
SELECT end_time,   
  (SELECT Max(v)    
   FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS    
   value(v)) AS [avg_DTU_percent]   
FROM sys.dm_db_resource_stats;  
  
```  
  
 O exemplo a seguir retorna os valores médio e máximo de percentual de CPU, E/S de dados e log e consumo de memória ao longo da última hora.  
  
```  
SELECT    
    AVG(avg_cpu_percent) AS 'Average CPU Utilization In Percent',   
    MAX(avg_cpu_percent) AS 'Maximum CPU Utilization In Percent',   
    AVG(avg_data_io_percent) AS 'Average Data IO In Percent',   
    MAX(avg_data_io_percent) AS 'Maximum Data IO In Percent',   
    AVG(avg_log_write_percent) AS 'Average Log Write Utilization In Percent',   
    MAX(avg_log_write_percent) AS 'Maximum Log Write Utilization In Percent',   
    AVG(avg_memory_usage_percent) AS 'Average Memory Usage In Percent',   
    MAX(avg_memory_usage_percent) AS 'Maximum Memory Usage In Percent'   
FROM sys.dm_db_resource_stats;  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [sys. resource_stats &#40;banco de dados do SQL Azure&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [Camadas de serviço](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [Limites e recursos de nível de serviço](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
