---
title: sys. dm_db_resource_stats (banco de dados SQL do Azure) | Microsoft Docs
ms.custom: ''
ms.date: 05/21/2019
ms.service: sql-database
ms.reviewer: ''
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
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 1dd66834788896e6952a0352eb2a19fd1a828513
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75245960"
---
# <a name="sysdm_db_resource_stats-azure-sql-database"></a>sys.dm_db_resource_stats (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna o consumo de CPU, E/S e consumo de memória para um banco de dados [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Existe uma linha para cada 15 segundos, mesmo se não houver nenhuma atividade no banco de dados. Os dados históricos são mantidos por aproximadamente uma hora.  
  
|Colunas|Tipo de Dados|DESCRIÇÃO|  
|-------------|---------------|-----------------|  
|end_time|**datetime**|Hora UTC que indica o término do intervalo de relatório atual.|  
|avg_cpu_percent|**decimal (5, 2)**|Utilização média de computação, em porcentagem, do limite da camada de serviço.|  
|avg_data_io_percent|**decimal (5, 2)**|Média de utilização de e/s de dados em porcentagem do limite da camada de serviço. Para bancos de dados de hiperescala, consulte [data e/s em estatísticas de utilização de recursos](https://docs.microsoft.com/azure/sql-database/sql-database-hyperscale-performance-diagnostics#data-io-in-resource-utilization-statistics).|  
|avg_log_write_percent|**decimal (5, 2)**|Média de gravações do log de transações (em MBps) como percentual do limite da camada de serviço.|  
|avg_memory_usage_percent|**decimal (5, 2)**|Utilização média de memória, em porcentagem, do limite da camada de serviço.<br /><br /> Isso inclui a memória usada para páginas do pool de buffers e o armazenamento de objetos OLTP na memória.|  
|xtp_storage_percent|**decimal (5, 2)**|Utilização de armazenamento para OLTP na memória em porcentagem do limite da camada de serviço (no final do intervalo de relatórios). Isso inclui a memória usada para o armazenamento dos seguintes objetos OLTP na memória: tabelas com otimização de memória, índices e variáveis de tabela. Ele também inclui a memória usada para processar operações ALTER TABLE.<br /><br /> Retornará 0 se o OLTP na memória não for usado no banco de dados.|  
|max_worker_percent|**decimal (5, 2)**|Máximo de trabalhos simultâneos (solicitações) em porcentagem do limite da camada de serviço do banco de dados.|  
|max_session_percent|**decimal (5, 2)**|Máximo de sessões simultâneas em porcentagem do limite da camada de serviço do banco de dados.|  
|dtu_limit|**int**|Configuração de DTU máxima do banco de dados atual para este banco de dados durante esse intervalo. Para bancos de dados que usam o modelo baseado em vCore, essa coluna é nula.|
|cpu_limit|**decimal (5, 2)**|Número de vCores para este banco de dados durante esse intervalo. Para bancos de dados que usam o modelo baseado em DTU, essa coluna é nula.|
|avg_instance_cpu_percent|**decimal (5, 2)**|Uso médio de CPU do banco de dados como uma porcentagem do processo do BD SQL.|
|avg_instance_memory_percent|**decimal (5, 2)**|Uso médio de memória do banco de dados como uma porcentagem do processo do BD SQL.|
|avg_login_rate_percent|**decimal (5, 2)**|Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.|
|replica_role|**int**|Representa a função da réplica atual com 0 como primário, 1 como secundário e 2 como encaminhador (primário do secundário geográfico). Você verá "1" quando conectado com a intenção ReadOnly a todos os secundários legíveis. Se estiver se conectando a um secundário geográfico sem especificar a intenção ReadOnly, você deverá ver "2" (conectando-se ao encaminhador).|
|||
  
> [!TIP]  
>  Para obter mais contexto sobre esses limites e camadas de serviço, consulte os tópicos [camadas de serviço](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/) e [limites e capacidades de camada de serviço](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/).  
  
## <a name="permissions"></a>Permissões  
 Essa exibição exige a permissão VIEW DATABASE STATE.  
  
## <a name="remarks"></a>Comentários  
 Os dados retornados por **Sys. dm_db_resource_stats** são expressos como uma porcentagem do limite máximo permitido para a camada de serviço/nível de desempenho que você está executando.
 
 Se o banco de dados fez failover para outro servidor nos últimos 60 minutos, a exibição retornará apenas dados para o tempo pelo qual ele foi o banco de dados primário desde esse failover.  
  
 Para uma exibição menos granular desses dados com um período de retenção mais longo, use o modo de exibição de catálogo **Sys. resource_stats** no banco de dados **mestre** . Essa exibição captura dados a cada 5 minutos e mantém dados históricos por 14 dias.  Para obter mais informações, consulte [Sys. resource_stats &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md).  
  
 Quando um banco de dados é membro de um pool elástico, as estatísticas de recursos apresentadas como valores percentuais são expressas como a porcentagem do limite máximo para os bancos de dados, conforme definido na configuração do pool elástico.  
  
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
    AVG(avg_log_write_percent) AS 'Average Log Write I/O Throughput Utilization In Percent',   
    MAX(avg_log_write_percent) AS 'Maximum Log Write I/O Throughput Utilization In Percent',   
    AVG(avg_memory_usage_percent) AS 'Average Memory Usage In Percent',   
    MAX(avg_memory_usage_percent) AS 'Maximum Memory Usage In Percent'   
FROM sys.dm_db_resource_stats;  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys. resource_stats &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [Camadas de serviço](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [Limites e recursos da camada de serviço](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
