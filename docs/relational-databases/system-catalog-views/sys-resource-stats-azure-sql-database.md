---
title: sys. resource_stats (banco de dados do SQL Azure) | Microsoft Docs
ms.custom: 
ms.date: 05/23/2016
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- resource_stats
- sys.resource_stats
- sys.resource_stats_TSQL
- resource_stats_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sys.resource_stats
- resource_stats
ms.assetid: 02379a1b-3622-4578-8c59-a1b8f1a17914
caps.latest.revision: "28"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dad039b91c30e4c8d89168dd90d549ec6507c750
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysresourcestats-azure-sql-database"></a>sys.resource_stats (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna os dados de armazenamento e de utilização da CPU para um Banco de Dados SQL do Azure. Os dados são coletados e agregados em intervalos de cinco minutos. Para cada banco de dados de usuário, há uma linha para cada janela de relatório de cinco minutos no qual há uma alteração no consumo de recursos. Isso inclui o uso de CPU, a alteração do tamanho do armazenamento ou a alteração de SKU do banco de dados. Os bancos de dados ociosos sem alterações podem não ter linhas para cada intervalo de cinco minutos. Os dados históricos são retidos por aproximadamente 14 dias.  
  
 O **sys. resource_stats** exibição tem definições diferentes dependendo da versão do servidor de banco de dados SQL do Azure que o banco de dados está associado. Considere essas diferenças e quaisquer modificações que seu aplicativo exige ao fazer a atualização para uma nova versão do servidor.  
  
 A tabela a seguir descreve as colunas disponíveis em um servidor v12:  
  
|Colunas (servidor v12)|Tipo de Dados|Description|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|Hora UTC que indica o início do intervalo de relatório de 5 minutos.|  
|end_time|**datetime**|Hora UTC que indica o final do intervalo de relatório 5 minutos.|  
|database_name|**varchar**|Nome do banco de dados do usuário.|  
|sku|**varchar**|Camada de serviço do banco de dados. O valores possíveis são os seguintes:<br /><br /> Basic<br /><br /> Standard<br /><br /> Premium|  
|storage_in_megabytes|**float**|Tamanho máximo de armazenamento em megabytes para o período de tempo, inclusive dados do banco de dados, índices, procedimentos armazenados e metadados.|  
|avg_cpu_percent|**numeric**|Utilização média de computação, em porcentagem, do limite da camada de serviço.|  
|avg_data_io_percent|**numeric**|Utilização média de E/S em percentagem com base no limite da camada de serviço.|  
|avg_log_write_percent|**numeric**|Utilização média do recurso de gravação, em porcentagem, do limite da camada de serviço.|  
|max_worker_percent|**decimal (5,2)**|Máximo simultâneos trabalhadores (solicitações) em porcentagem com base no limite da camada de serviço do banco de dados.<br /><br /> Máximo está atualmente calculado para o intervalo de 5 minutos com base em 15 segundo exemplos de contagens de trabalho simultâneos.|  
|max_session_percent|**decimal (5,2)**|Máximo de sessões simultâneas em porcentagem com base no limite da camada de serviço do banco de dados.<br /><br /> Máximo está atualmente calculado para o intervalo de 5 minutos com base em 15 segundo exemplos de contagens de sessões simultâneas.|  
|dtu_limit|**int**|Banco de dados max DTU configuração atual para este banco de dados durante esse intervalo.|  
  
> [!TIP]  
>  Para obter mais contexto sobre esses limites e as camadas de serviço, consulte os tópicos [camadas de serviço](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/) e [limites e recursos da camada de serviço](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/).  
  
 A tabela a seguir descreve as colunas disponíveis em um servidor v11:  
  
|Colunas (servidor v11)|Tipo de Dados|Description|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|Hora UTC que indica o início do intervalo de relatório de 5 minutos.|  
|end_time|**datetime**|Hora UTC que indica o final do intervalo de relatório 5 minutos.|  
|database_name|**nvarchar**|Nome do banco de dados.|  
|sku|**nvarchar**|Camada de serviço do banco de dados. O valores possíveis são os seguintes:<br /><br /> Web<br /><br /> Business<br /><br /> Basic<br /><br /> Standard<br /><br /> Premium|  
|usage_in_seconds|**int**|*Observação: Esta coluna é preterida para v11 e seu valor é sempre definido como 0.*<br /><br /> Tempo de CPU usado desde que a última medida foi feita.<br /><br /> Para a medida de CPU, recomendamos que você use o **avg_cpu_cores_used** coluna, em vez desta coluna.|  
|storage_in_megabytes|**decimal**|Tamanho máximo de armazenamento em megabytes para o período de tempo, inclusive dados do banco de dados, índices, procedimentos armazenados e metadados.|  
|avg_cpu_cores_used|**decimal**|*Observação: Esta coluna é preterida para v11 e seu valor é sempre definido como 0.*<br /><br /> Média de núcleos de CPU usados nesse intervalo.|  
|avg_physical_read_iops|**decimal**|*Observação: Esta coluna é preterida para v11 e seu valor é sempre definido como 0.*<br /><br /> Média de IOPS lidos nesse intervalo.|  
|avg_physical_write_iops|**decimal**|*Observação: Esta coluna é preterida para v11 e seu valor é sempre definido como 0.*<br /><br /> Média de IOPS de gravação neste intervalo.|  
|active_memory_used_kb|**bigint**|*Observação: Esta coluna é preterida para v11 e seu valor é sempre definido como 0.*<br /><br /> Contagem de memória ativa que está sendo usada no final desse intervalo.|  
|active_session_count|**int**|Contagem de sessões ativas no final desse intervalo.|  
|active_worker_count|**int**|Contagem de operadores ativos no final desse intervalo.|  
|avg_cpu_percent|**decimal**|Utilização média de computação, em porcentagem, do limite da camada de serviço.|  
|avg_physical_data_read_percent|**decimal**|Utilização média de E/S em percentagem com base no limite da camada de serviço.|  
|avg_log_write_percent|**decimal**|Utilização média do recurso de gravação, em porcentagem, do limite da camada de serviço.|  
  
## <a name="permissions"></a>Permissões  
 Essa exibição está disponível para todas as funções de usuário com permissões para se conectar ao virtual **mestre** banco de dados.  
  
## <a name="remarks"></a>Comentários  
 Os dados retornados por **sys. resource_stats** é expresso como uma porcentagem do máximo permitido de limites DTU para o nível de desempenho/da camada de serviço que você está executando para bancos de dados Basic, Standard e Premium.  Para as camadas Web e Negócios, esses números indicam as percentagens em termos da camada de desempenho Standard S2.  Por exemplo, ao executar com relação a um banco de dados Web, se avg_cpu_percent retornar 70%, isso indica 70% do limite da camada S2. Além disso, para camadas Web e Negócios, as percentagens podem refletir um número além de 100%, o que também é baseado no limite da camada S2.  
  
 Quando um banco de dados é um membro de um pool Elástico, as estatísticas de recursos apresentadas como valores de porcentagem são expressos como o percentual do limite máximo de DTU de bancos de dados conforme definido na configuração do pool Elástico.  
  
 Para obter uma exibição mais granular desses dados, use **sys.DM db_resource_stats** exibição de gerenciamento dinâmico em um banco de dados do usuário. Essa visualização captura dados a cada 15 segundos e mantém dados históricos por 1 hora.  Para obter mais informações, consulte [sys.DM db_resource_stats &#40; Banco de dados SQL do Azure &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md).  

## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todos os bancos de dados que estão com média de pelo menos 80% de utilização de computação durante a última semana.  
  
```  
DECLARE @s datetime;  
DECLARE @e datetime;  
SET @s= DateAdd(d,-7,GetUTCDate());  
SET @e= GETUTCDATE();  
SELECT database_name, AVG(avg_cpu_percent) AS Average_Compute_Utilization   
FROM sys.resource_stats   
WHERE start_time BETWEEN @s AND @e  
GROUP BY database_name  
HAVING AVG(avg_cpu_percent) >= 80  
```  
  
 O exemplo a seguir calcula o consumo percentual de DTU médio para um determinado banco de dados. (Esta consulta só funciona quando executada em um servidor v11.)  
  
```  
SELECT start_time, end_time,      
  (SELECT Max(v)      
   FROM (VALUES (avg_cpu_percent), (avg_physical_data_read_percent), (avg_log_write_percent)) AS value(v)) AS [avg_DTU_percent]    
FROM sys.resource_stats   
WHERE database_name = '<your db name>'   
ORDER BY end_time DESC;  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Camadas de serviço](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [Limites e recursos de nível de serviço](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
