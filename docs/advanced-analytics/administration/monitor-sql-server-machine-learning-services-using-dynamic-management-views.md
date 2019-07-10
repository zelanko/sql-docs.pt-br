---
title: Monitorar a execução do script R e Python usando exibições de gerenciamento dinâmico (DMVs) - aprendizagem de máquina do SQL Server
description: Use exibições de gerenciamento dinâmico (DMVs) para monitorar a execução de script externo de R e Python no SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 8d701d9e8595eee3a583e913baabc2148af214fe
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67681617"
---
# <a name="monitor-sql-server-machine-learning-services-using-dynamic-management-views-dmvs"></a>Monitorar serviços do SQL Server Machine Learning usando exibições de gerenciamento dinâmico (DMVs)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Use scripts de exibições de gerenciamento dinâmico (DMVs) para monitorar a execução de externos (R e Python), recursos usados, diagnosticar problemas e ajustar o desempenho em serviços do SQL Server Machine Learning.

Neste artigo, você encontrará as DMVs que são específicas para serviços do SQL Server Machine Learning. Você também encontrará consultas de exemplo que mostram:

+ As configurações e opções de configuração para o machine learning
+ Sessões ativas em execução de scripts R ou Python externos
+ Estatísticas de execução para o tempo de execução externo para R e Python
+ Contadores de desempenho para scripts externos
+ Uso de memória para o sistema operacional, do SQL Server e pools de recursos externos
+ Configuração de memória para o SQL Server e pools de recursos externos
+ Pools de recursos do administrador de recursos, incluindo os pools de recursos externos
+ Pacotes instalados para R e Python

Para obter mais informações sobre DMVs, consulte [exibições de gerenciamento dinâmico do sistema](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).

> [!TIP]
> Você também pode usar os relatórios personalizados para monitorar os serviços do SQL Server Machine Learning. Para obter mais informações, consulte [monitorar o machine learning usando relatórios personalizados no Management Studio](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md).

## <a name="dynamic-management-views"></a>Exibições de gerenciamento dinâmico

As seguintes exibições de gerenciamento dinâmico podem ser usadas ao monitorar cargas de trabalho de aprendizado de máquina no SQL Server. Para consultar as DMVs, você precisa `VIEW SERVER STATE` permissão na instância.

| Exibição de gerenciamento dinâmico | type | Descrição |
|-------------------------|------|-------------|
| [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) | Execução | Retorna uma linha para cada conta de trabalho ativa que executa um script externo. |
| [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) | Execução | Retorna uma linha para cada tipo de solicitação de script externo. |
| [sys.dm_os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md) | Execução | Retorna uma linha por contador de desempenho mantido pelo servidor. Se você usar o critério de pesquisa `WHERE object_name LIKE '%External Scripts%'`, você pode usar essas informações para ver quantos scripts foram executados, quais scripts foram executados usando qual modo de autenticação ou quantas R ou chamadas de Python foram emitidas na instância geral. |
| [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) | Administrador de Recursos | Retorna informações sobre o estado atual do pool de recursos externos no administrador de recursos, a configuração atual de pools de recursos e as estatísticas de pool de recursos. |
| [sys.dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md) | Administrador de Recursos | Retorna informações de afinidade de CPU sobre a configuração atual do pool de recursos externos no administrador de recursos. Retorna uma linha por agendador no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], onde cada agendador é mapeado para um processador individual. Use esta exibição para monitorar a condição de um agendador ou para identificar tarefas sem controle. |

Para obter informações sobre como monitorar [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instâncias, consulte [modos de exibição de catálogo](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md) e [Resource Governor relacionados exibições de gerenciamento dinâmico](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md).

## <a name="settings-and-configuration"></a>As configurações e definições

Exiba as opções de configuração e a configuração de instalação do serviços de Machine Learning.

![Saída da consulta de configuração e configurações](media/dmv-settings-and-configuration.png "de saída da consulta de configuração e configurações")

Execute a consulta abaixo para obter essa saída. Para obter mais informações sobre as exibições e funções usadas, consulte [sys.dm_server_registry](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md), [sys. Configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md), e [SERVERPROPERTY](../../t-sql/functions/serverproperty-transact-sql.md).

```sql
SELECT CAST(SERVERPROPERTY('IsAdvancedAnalyticsInstalled') AS INT) AS IsMLServicesInstalled
    , CAST(value_in_use AS INT) AS ExternalScriptsEnabled
    , COALESCE(SIGN(SUSER_ID(CONCAT (
                    CAST(SERVERPROPERTY('MachineName') AS NVARCHAR(128))
                    , '\SQLRUserGroup'
                    , CAST(serverproperty('InstanceName') AS NVARCHAR(128))
                    ))), 0) AS ImpliedAuthenticationEnabled
    , COALESCE((
            SELECT CAST(r.value_data AS INT)
            FROM sys.dm_server_registry AS r
            WHERE r.registry_key LIKE 'HKLM\Software\Microsoft\Microsoft SQL Server\%\SuperSocketNetLib\Tcp'
            AND r.value_name = 'Enabled'
            ), - 1) AS IsTcpEnabled
FROM sys.configurations
WHERE name = 'external scripts enabled';
```

A consulta retorna as colunas a seguir:

| coluna | Descrição |
|--------|-------------|
| IsMLServicesInstalled | Retornará 1 se os serviços de Machine Learning do SQL Server está instalado para a instância. Caso contrário, retornará 0. |
| ExternalScriptsEnabled | Retornará 1 se os scripts externos é habilitado para a instância. Caso contrário, retornará 0. |
| ImpliedAuthenticationEnabled | Retornará 1 se a autenticação implícita está habilitado. Caso contrário, retornará 0. A configuração de autenticação implícita é verificada, verificando se existe um logon para SQLRUserGroup. |
| IsTcpEnabled | Retornará 1 se o protocolo TCP/IP está habilitado para a instância. Caso contrário, retornará 0. Para obter mais informações, consulte [padrão a configuração de protocolo do SQL Server rede](../../database-engine/configure-windows/default-sql-server-network-protocol-configuration.md). |

## <a name="active-sessions"></a>Sessões ativas

Exiba sessões ativas em execução de scripts externos.

![Saída da consulta configurações ativas](media/dmv-active-sessions.png "de saída da consulta configurações ativas")

Execute a consulta abaixo para obter essa saída. Para obter mais informações sobre os modos de exibição de gerenciamento dinâmico usados, consulte [. DM exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md), [DM external_script_requests](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md), e [DM exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md).

```sql
SELECT r.session_id, r.blocking_session_id, r.status, DB_NAME(s.database_id) AS database_name
    , s.login_name, r.wait_time, r.wait_type, r.last_wait_type, r.total_elapsed_time, r.cpu_time
    , r.reads, r.logical_reads, r.writes, er.language, er.degree_of_parallelism, er.external_user_name
FROM sys.dm_exec_requests AS r
INNER JOIN sys.dm_external_script_requests AS er
ON r.external_script_request_id = er.external_script_request_id
INNER JOIN sys.dm_exec_sessions AS s
ON s.session_id = r.session_id;
```

A consulta retorna as colunas a seguir:

| coluna | Descrição |
|--------|-------------|
| session_id | Identifica a sessão associada a cada conexão primária ativa. |
| blocking_session_id | ID da sessão que está bloqueando a solicitação. Se esta coluna for NULL, a solicitação não estará bloqueada ou as informações da sessão de bloqueio não estarão disponíveis (ou não podem ser identificadas). |
| status | Status da solicitação. |
| database_name | Nome do banco de dados atual para cada sessão. |
| login_name | Nome de logon do SQL Server na qual a sessão está sendo executada. |
| wait_time | Se a solicitação estiver bloqueada, esta coluna retornará a duração, em milissegundos, da espera atual. Não permite valor nulo. |
| wait_type | Se a solicitação estiver bloqueada, esta coluna retornará o tipo de espera. Para obter informações sobre tipos de espera, consulte [DM os_wait_stats](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md). |
| last_wait_type | Se esta solicitação tiver sido previamente bloqueada, esta coluna retornará o tipo da última espera. |
| total_elapsed_time | Tempo total decorrido em milissegundos desde que a solicitação chegou. |
| cpu_time | Tempo da CPU, em milissegundos, usado pela solicitação. |
| reads | Número de leituras executadas por esta solicitação. |
| logical_reads | Número de leituras lógicas executadas pela solicitação. |
| writes | Número de gravações executadas por esta solicitação. |
| language | Palavra-chave que representa uma linguagem de script com suporte. |
| degree_of_parallelism | Número que indica o número de processos paralelos que foram criados. Esse valor pode ser diferente do número de processos paralelos solicitados. |
| external_user_name | A conta de trabalho do Windows na qual o script foi executado. |

## <a name="execution-statistics"></a>Estatísticas de execução

Exiba as estatísticas de execução para o tempo de execução externo para R e Python. Somente estatísticas de RevoScaleR, revoscalepy ou funções de pacote microsoftml estão disponíveis no momento.

![Saída da consulta de estatísticas de execução](media/dmv-execution-statistics.png "de saída da consulta de estatísticas de execução")

Execute a consulta abaixo para obter essa saída. Para obter mais informações sobre o modo de exibição de gerenciamento dinâmico usado, consulte [DM external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). A consulta retorna apenas as funções que foram executadas mais de uma vez.

```sql
SELECT language, counter_name, counter_value
FROM sys.dm_external_script_execution_stats
WHERE counter_value > 0
ORDER BY language, counter_name;
```

A consulta retorna as colunas a seguir:

| coluna | Descrição |
|--------|-------------|
| language | Nome da linguagem de script externo registrada. |
| counter_name | Nome de uma função de script externo registrada. |
| counter_value | Número total de instâncias nas quais a função de script externo registrada foi chamada no servidor. Esse valor é cumulativo, começando com a hora em que o recurso foi instalado na instância, e não pode ser redefinido. |

## <a name="performance-counters"></a>Contadores de desempenho

Exiba os contadores de desempenho relacionados à execução de scripts externos.

![Consulta de saída do desempenho do contadores](media/dmv-performance-counters.png "saída o desempenho de consulta de contadores")

Execute a consulta abaixo para obter essa saída. Para obter mais informações sobre o modo de exibição de gerenciamento dinâmico usado, consulte [DM os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md).

```sql
SELECT counter_name, cntr_value
FROM sys.dm_os_performance_counters 
WHERE object_name LIKE '%External Scripts%'
```

**DM os_performance_counters** gera os seguintes contadores de desempenho para scripts externos:

| Contador | Descrição |
|---------|-------------|
| Total de Execuções | Número de processos externos iniciados por chamadas locais ou remotas. |
| Execuções paralelas | Número de vezes que um script incluiu a _@parallel_ especificação e que [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] foi capaz de gerar e usar um plano de consulta paralela. |
| Execuções de streaming | Número de vezes que o recurso de streaming foi invocado. |
| Execuções de CC do SQL | Número de scripts externos executados em que a chamada foi instanciada remotamente e o SQL Server foi usado como o contexto de computação. |
| Autenticação Implícita. Logons | Número de vezes que foi feita uma chamada de loopback ODBC usando a autenticação implícita; ou seja, o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] executou a chamada em nome de usuário que está enviando a solicitação de script. |
| Tempo total de execução (ms) | Tempo decorrido entre a chamada e a conclusão da chamada. |
| Erros de Execução | Número de vezes que scripts relataram erros. Essa contagem não inclui erros de R ou Python. |

## <a name="memory-usage"></a>Uso de memória

Exibir informações sobre a memória usada pelo sistema operacional, do SQL Server e os pools externos.

![Saída da consulta de uso de memória](media/dmv-memory-usage.png "de saída da consulta de uso de memória")

Execute a consulta abaixo para obter essa saída. Para obter mais informações sobre os modos de exibição de gerenciamento dinâmico usados, consulte [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) e [DM os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md).

```sql
SELECT physical_memory_kb, committed_kb
    , (SELECT SUM(peak_memory_kb)
        FROM sys.dm_resource_governor_external_resource_pools AS ep
        ) AS external_pool_peak_memory_kb
FROM sys.dm_os_sys_info;
```

A consulta retorna as colunas a seguir:

| coluna | Descrição |
|--------|-------------|
| physical_memory_kb | A quantidade total de memória física no computador. |
| committed_kb | A memória confirmada em KB (quilobytes) no Gerenciador de memória. Não inclui a memória reservada no gerenciador de memória. |
| external_pool_peak_memory_kb | A soma da quantidade máxima de memória usada, em quilobytes, para todos os pools de recursos externos. |

## <a name="memory-configuration"></a>Configuração de memória

Exibir informações sobre a configuração máxima de memória em percentual do SQL Server e pools de recursos externos. Se o SQL Server está em execução com o valor padrão de `max server memory (MB)`, ele é considerado como 100% da memória do sistema operacional.

![Saída da consulta de configuração de memória](media/dmv-memory-configuration.png "de saída da consulta de configuração de memória")

Execute a consulta abaixo para obter essa saída. Para obter mais informações sobre as exibições usadas, consulte [sys. Configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) e [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md).

```sql
SELECT 'SQL Server' AS name
    , CASE CAST(c.value AS BIGINT)
        WHEN 2147483647 THEN 100
        ELSE (SELECT CAST(c.value AS BIGINT) / (physical_memory_kb / 1024.0) * 100 FROM sys.dm_os_sys_info)
        END AS max_memory_percent
FROM sys.configurations AS c
WHERE c.name LIKE 'max server memory (MB)'
UNION ALL
SELECT CONCAT ('External Pool - ', ep.name) AS pool_name, ep.max_memory_percent
FROM sys.dm_resource_governor_external_resource_pools AS ep;
```

A consulta retorna as colunas a seguir:

| coluna | Descrição |
|--------|-------------|
| nome | Nome do pool de recursos externos ou do SQL Server. |
| max_memory_percent | A memória máxima que pode usar o SQL Server ou o pool de recursos externos. |

## <a name="resource-pools"></a>Pools de recursos

Na [administrador de recursos do SQL Server](../../relational-databases/resource-governor/resource-governor.md), um [pool de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md) representa um subconjunto dos recursos físicos de uma instância. Você pode especificar os limites na quantidade de CPU, e/s física e memória que as solicitações recebidas de aplicativos, incluindo a execução de scripts externos, podem usar dentro do pool de recursos. Exiba os pools de recursos usados para o SQL Server e scripts externos.

![Saída do recurso de consulta de pools](media/dmv-resource-pools.png "pools de saída do recurso da consulta")

Execute a consulta abaixo para obter essa saída. Para obter mais informações sobre os modos de exibição de gerenciamento dinâmico usados, consulte [DM resource_governor_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md) e [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md).

```sql
SELECT CONCAT ('SQL Server - ', p.name) AS pool_name
    , p.total_cpu_usage_ms, p.read_io_completed_total, p.write_io_completed_total
FROM sys.dm_resource_governor_resource_pools AS p
UNION ALL
SELECT CONCAT ('External Pool - ', ep.name) AS pool_name
    , ep.total_cpu_user_ms, ep.read_io_count, ep.write_io_count
FROM sys.dm_resource_governor_external_resource_pools AS ep;
```

A consulta retorna as colunas a seguir:

| coluna | Descrição |
|--------|-------------|
| pool_name | Nome do pool de recursos. Pools de recursos do SQL Server são prefixados com `SQL Server` e pools de recursos externos são prefixados com `External Pool`.
| total_cpu_usage_hours | O uso de CPU cumulativo em milissegundos, desde que as estatísticas do administrador de recursos foram redefinidas. |
| read_io_completed_total | O total de E/S lidas concluídas desde que as estatísticas do Administrador de Recursos foram redefinidas. |
| write_io_completed_total | O total de E/Ss de gravação concluídas desde que as estatísticas do Administrador de Recursos foram redefinidas. |

## <a name="installed-packages"></a>Pacotes instalados

Você pode para exibir os pacotes de R e Python que estão instalados no SQL Server Machine Learning Services executando um script de R ou Python que gera esses.

### <a name="installed-packages-for-r"></a>Pacotes instalados para R

Exiba os pacotes de R instalados em serviços do SQL Server Machine Learning.

![Saída de pacotes instalados para consulta de R](media/dmv-installed-packages-r.png "os pacotes instalados para consulta de R de saída")

Execute a consulta abaixo para obter essa saída. A consulta usar um script de R para determinar os pacotes R instalados com o SQL Server.

```sql
EXEC sp_execute_external_script @language = N'R'
, @script = N'
OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
    , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
```

As colunas retornadas são:

| coluna | Descrição |
|--------|-------------|
| Pacote | Nome do pacote instalado. |
| Versão | Versão do pacote. |
| Depende | Lista o pacote (s) que depende do pacote instalado. |
| Licença | Licença para o pacote instalado. |
| LibPath | Diretório onde você pode encontrar o pacote. |

### <a name="installed-packages-for-python"></a>Pacotes instalados para Python

Exiba os pacotes do Python instalados no SQL Server Machine Learning Services.

![Saída de pacotes instalados para consulta de Python](media/dmv-installed-packages-python.png "os pacotes instalados para consulta de Python de saída")

Execute a consulta abaixo para obter essa saída. A consulta a usar um script de Python para determinar os pacotes do Python instalados com o SQL Server.

```sql
EXEC sp_execute_external_script @language = N'Python'
, @script = N'
import pip
OutputDataSet = pandas.DataFrame([(i.key, i.version, i.location) for i in pip.get_installed_distributions()])'
WITH result sets((Package NVARCHAR(128), Version NVARCHAR(128), Location NVARCHAR(1000)));
```

As colunas retornadas são:

| coluna | Descrição |
|--------|-------------|
| Pacote | Nome do pacote instalado. |
| Versão | Versão do pacote. |
| Location | Diretório onde você pode encontrar o pacote. |

## <a name="next-steps"></a>Próximas etapas

+ [Gerenciando e monitorando soluções de aprendizado de máquina](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)
+ [Eventos estendidos para o aprendizado de máquina](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md)
+ [Administrador de recursos relacionados a exibições de gerenciamento dinâmico](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)
+ [Exibições de gerenciamento dinâmico do sistema](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
+ [Monitorar o machine learning usando relatórios personalizados no Management Studio](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)