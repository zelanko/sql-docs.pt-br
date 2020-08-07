---
title: sys. resource_stats (banco de dados SQL do Azure) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2018
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- resource_stats
- sys.resource_stats
- sys.resource_stats_TSQL
- resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_stats
- resource_stats
ms.assetid: 02379a1b-3622-4578-8c59-a1b8f1a17914
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: be336780f5bbfd45660ea376c0d689b577f052da
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87822798"
---
# <a name="sysresource_stats-azure-sql-database"></a>sys.resource_stats (Banco de Dados SQL do Azure)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  Retorna os dados de armazenamento e de utilização da CPU para um Banco de Dados SQL do Azure. Os dados são coletados e agregados em intervalos de cinco minutos. Para cada banco de dados de usuário, há uma linha para cada janela de relatório de cinco minutos, na qual há uma alteração no consumo de recursos. Os dados retornados incluem uso de CPU, alteração de tamanho de armazenamento e modificação de SKU de banco de dados. Bancos de dados ociosos sem alterações podem não ter linhas para cada intervalo de cinco minutos. Os dados históricos são retidos por aproximadamente 14 dias.  
  
 A exibição **Sys. resource_stats** tem definições diferentes, dependendo da versão do servidor de banco de dados SQL do Azure ao qual o banco de dados está associado. Considere essas diferenças e quaisquer modificações que seu aplicativo exige ao fazer a atualização para uma nova versão do servidor.  
  
 A tabela a seguir descreve as colunas disponíveis em um servidor v12:  
  
|Colunas|Tipo de Dados|Descrição|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|Hora UTC indicando o início do intervalo de relatórios de cinco minutos.|  
|end_time|**datetime**|Hora UTC indicando o final do intervalo de relatórios de cinco minutos.|  
|database_name|**nvarchar(128)**|Nome do banco de dados do usuário.|  
|sku|**nvarchar(128)**|Camada de serviço do banco de dados. O valores possíveis são os seguintes:<br /><br /> Basic<br /><br /> Standard<br /><br /> Premium<br /><br />Uso Geral<br /><br />Comercialmente Crítico|  
|storage_in_megabytes|**float**|O tamanho máximo de armazenamento em megabytes para o período de tempo, incluindo dados do banco de dados, índices, procedimentos armazenados e metadados.|  
|avg_cpu_percent|**decimal (5, 2)**|Utilização média de computação, em porcentagem, do limite da camada de serviço.|  
|avg_data_io_percent|**decimal (5, 2)**|Utilização média de E/S em percentagem com base no limite da camada de serviço. Para bancos de dados de hiperescala, consulte [data e/s em estatísticas de utilização de recursos](https://docs.microsoft.com/azure/sql-database/sql-database-hyperscale-performance-diagnostics#data-io-in-resource-utilization-statistics).|  
|avg_log_write_percent|**decimal (5, 2)**|Utilização média do recurso de gravação, em porcentagem, do limite da camada de serviço.|  
|max_worker_percent|**decimal (5, 2)**|Máximo de trabalhos simultâneos (solicitações) em porcentagem com base no limite da camada de serviço do banco de dados.<br /><br /> No momento, o máximo é calculado para o intervalo de cinco minutos com base nas amostras de 15 segundos de contagens de trabalho simultâneas.|  
|max_session_percent|**decimal (5, 2)**|Máximo de sessões simultâneas em porcentagem com base no limite da camada de serviço do banco de dados.<br /><br /> No momento, o máximo é calculado para o intervalo de cinco minutos com base nas amostras de 15 segundos de contagens de sessão simultâneas.|  
|dtu_limit|**int**|Configuração de DTU máxima do banco de dados atual para este banco de dados durante esse intervalo. |
|xtp_storage_percent|**decimal (5, 2)**|Utilização de armazenamento para OLTP na memória em porcentagem do limite da camada de serviço (no final do intervalo de relatórios). Isso inclui a memória usada para o armazenamento dos seguintes objetos OLTP na memória: tabelas com otimização de memória, índices e variáveis de tabela. Ele também inclui a memória usada para processar operações ALTER TABLE.<br /><br /> Retornará 0 se o OLTP na memória não for usado no banco de dados.|
|avg_login_rate_percent|**decimal (5, 2)**|Identificado apenas para fins informativos. Não há suporte. A compatibilidade futura não está garantida.|
|avg_instance_cpu_percent|**decimal (5, 2)**|Uso médio de CPU do banco de dados como uma porcentagem do processo do banco de dados SQL.|
|avg_instance_memory_percent|**decimal (5, 2)**|Uso médio de memória do banco de dados como uma porcentagem do processo do banco de dados SQL.|
|cpu_limit|**decimal (5, 2)**|Número de vCores para este banco de dados durante esse intervalo. Para bancos de dados que usam o modelo baseado em DTU, essa coluna é nula.|
|allocated_storage_in_megabytes|**float**|A quantidade de espaço de arquivo formatado em MB disponibilizada para armazenar dados de banco de dados. O espaço de arquivo formatado também é conhecido como espaço de dados alocado.  Para obter mais informações, consulte: [Gerenciamento de espaço de arquivo no banco de dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-file-space-management)|
  
> [!TIP]  
>  Para obter mais contexto sobre esses limites e camadas de serviço, consulte as [camadas de serviço](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)de tópicos.  
    
## <a name="permissions"></a>Permissões  
 Essa exibição está disponível para todas as funções de usuário com permissões para se conectar ao banco de dados **mestre** virtual.  
  
## <a name="remarks"></a>Comentários  
 Os dados retornados por **Sys. resource_stats** são expressos como uma porcentagem do limite máximo permitido para a camada de serviço/nível de desempenho que você está executando.  
  
 Quando um banco de dados é membro de um pool elástico, as estatísticas de recursos apresentadas como valores percentuais são expressas como a porcentagem do limite máximo para os bancos de dados, conforme definido na configuração do pool elástico.  
  
 Para obter uma exibição mais granular desses dados, use **Sys. dm_db_resource_stats** exibição de gerenciamento dinâmico em um banco de dados de usuário. Essa visualização captura dados a cada 15 segundos e mantém dados históricos por 1 hora.  Para obter mais informações, consulte [Sys. dm_db_resource_stats &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md).  

## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todos os bancos de dados que estão com média de pelo menos 80% de utilização de computação durante a última semana.  
  
```sql  
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
    
## <a name="see-also"></a>Consulte Também  
 [Camadas de serviço](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [Limites e recursos da camada de serviço](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
