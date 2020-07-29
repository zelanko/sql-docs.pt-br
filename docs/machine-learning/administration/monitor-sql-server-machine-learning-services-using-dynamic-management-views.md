---
title: Monitorar scripts usando DMVs
description: Use DMVs (exibições de gerenciamento dinâmico) para monitorar a execução de script externo do Python e do R nos Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 09/17/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2313b13a009ea4c3fb5ec6a8dae6da75716f0b1b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85726583"
---
# <a name="monitor-sql-server-machine-learning-services-using-dynamic-management-views-dmvs"></a>Monitorar os Serviços de Machine Learning do SQL Server usando DMVs (exibições de gerenciamento dinâmico)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Use DMVs (exibições de gerenciamento dinâmico) para monitorar a execução de scripts externos (do Python e do R), os recursos usados, diagnosticar problemas e ajustar o desempenho no Serviços de Machine Learning do SQL Server.

Neste artigo, você encontrará as DMVs específicas para os Serviços de Machine Learning do SQL Server. Você também encontrará consultas de exemplo que mostram:

+ Opções de configuração e definições para aprendizado de máquina
+ Sessões ativas executando Python ou scripts externos
+ Estatísticas de execução para o runtime externo para Python e R
+ Contadores de desempenho para scripts externos
+ Uso de memória para o sistema operacional, o SQL Server e pools de recursos externos
+ Configuração de memória para o SQL Server e pools de recursos externos
+ Pools de recursos do Resource Governor, incluindo pools de recursos externos
+ Pacotes instalados para Python e R

Para obter mais informações gerais sobre DMVs, confira [Exibições de gerenciamento dinâmico do sistema](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).

> [!TIP]
> Use também os relatórios personalizados para monitorar Serviços de Machine Learning do SQL Server. Para obter mais informações, confira [Monitorar aprendizado de máquina usando relatórios personalizados no Management Studio](monitor-sql-server-machine-learning-services-using-custom-reports-management-studio.md).

## <a name="dynamic-management-views"></a>Exibições de gerenciamento dinâmico

As exibições de gerenciamento dinâmico a seguir podem ser usadas ao monitorar cargas de trabalho de aprendizado de máquina no SQL Server. Para consultar as DMVs, você precisará de permissão de `VIEW SERVER STATE` na instância.

| Exibição de gerenciamento dinâmico | Type | Descrição |
|-------------------------|------|-------------|
| [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) | Execução | Retorna uma linha para cada conta de trabalho ativa que executa um script externo. |
| [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) | Execução | Retorna uma linha para cada tipo de solicitação de script externo. |
| [sys.dm_os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md) | Execução | Retorna uma linha por contador de desempenho mantido pelo servidor. Caso use a condição de pesquisa `WHERE object_name LIKE '%External Scripts%'`, você pode usar essas informações para ver quantos scripts foram executados, quais scripts foram executados usando o modo de autenticação ou quantas chamadas de R ou Python foram emitidas na instância em geral. |
| [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) | Administrador de Recursos | Retorna informações sobre o estado atual do pool de recursos externo no Resource Governor, a configuração atual e as estatísticas do pool de recursos. |
| [sys.dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md) | Administrador de Recursos | Retorna informações de afinidade de CPU sobre a configuração atual do pool de recursos externos no Resource Governor. Retorna uma linha por agendador no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], onde cada agendador é mapeado para um processador individual. Use esta exibição para monitorar a condição de um agendador ou para identificar tarefas sem controle. |

Para obter informações sobre o monitoramento de instâncias [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], confira [Exibição de catálogo](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md) e [Exibições de gerenciamento dinâmico relacionadas ao Resource Governor](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md).

## <a name="settings-and-configuration"></a>Definições e configuração

Exiba as definições de instalação dos Serviços de Machine Learning e as opções de configuração.

![Saída da consulta de definições e configuração](media/dmv-settings-and-configuration.png "Saída da consulta de definições e configuração")

Execute a consulta abaixo para obter essa saída. Para obter mais informações sobre as exibições e funções usadas, confira [sys.dm_server_registry](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md), [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) e [SERVERPROPERTY](../../t-sql/functions/serverproperty-transact-sql.md).

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

A consulta retorna as seguintes colunas:

| Coluna | Descrição |
|--------|-------------|
| IsMLServicesInstalled | Retornará 1 se os Serviços de Machine Learning do SQL Server estiverem instalados na instância. Caso contrário, retornará 0. |
| ExternalScriptsEnabled | Retornará 1 se os scripts externos estiverem habilitados para a instância. Caso contrário, retornará 0. |
| ImpliedAuthenticationEnabled | Retornará 1 se a autenticação implícita estiver habilitada. Caso contrário, retornará 0. A configuração de autenticação implícita é confirmada ao verificar se há um logon para SQLRUserGroup. |
| IsTcpEnabled | Retornará 1 se o protocolo TCP/IP estiver habilitado para a instância. Caso contrário, retornará 0. Para obter mais informações, veja [Configuração de protocolo de rede padrão do SQL Server](../../database-engine/configure-windows/default-sql-server-network-protocol-configuration.md). |

## <a name="active-sessions"></a>Sessões ativas

Exiba as sessões ativas executando scripts externos.

![Saída da consulta de configurações ativas](media/dmv-active-sessions.png "Saída da consulta de configurações ativas")

Execute a consulta abaixo para obter essa saída. Para obter mais informações sobre as exibições de gerenciamento dinâmico usadas, confira [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md), [sys.dm_external_script_requests](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) e [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md).

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

A consulta retorna as seguintes colunas:

| Coluna | Descrição |
|--------|-------------|
| session_id | Identifica a sessão associada a cada conexão primária ativa. |
| blocking_session_id | ID da sessão que está bloqueando a solicitação. Se esta coluna for NULL, a solicitação não estará bloqueada ou as informações da sessão de bloqueio não estarão disponíveis (ou não podem ser identificadas). |
| status | Status da solicitação. |
| database_name | Nome do banco de dados atual para cada sessão. |
| login_name | Nome do logon do SQL Server no qual a sessão está sendo executada atualmente. |
| wait_time | Se a solicitação estiver bloqueada, esta coluna retornará a duração, em milissegundos, da espera atual. Não permite valor nulo. |
| wait_type | Se a solicitação estiver bloqueada, esta coluna retornará o tipo de espera. Para obter informações sobre tipos de espera, confira [sys.dm_os_wait_stats](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md). |
| last_wait_type | Se esta solicitação tiver sido previamente bloqueada, esta coluna retornará o tipo da última espera. |
| total_elapsed_time | Tempo total decorrido em milissegundos desde que a solicitação chegou. |
| cpu_time | Tempo da CPU, em milissegundos, usado pela solicitação. |
| reads | Número de leituras executadas por esta solicitação. |
| logical_reads | Número de leituras lógicas executadas pela solicitação. |
| writes | Número de gravações executadas por esta solicitação. |
| Linguagem | Palavra-chave que representa uma linguagem de script com suporte. |
| degree_of_parallelism | Número que indica o número de processos paralelos que foram criados. Esse valor pode ser diferente do número de processos paralelos solicitados. |
| external_user_name | A conta de trabalho do Windows na qual o script foi executado. |

## <a name="execution-statistics"></a>Estatísticas de execução

Exiba as estatísticas de execução para o runtime externo para R e Python. Somente as estatísticas de funções de pacote do RevoScaleR, revoscalepy ou microsoftml estão disponíveis no momento.

![Saída da consulta de estatísticas de execução](media/dmv-execution-statistics.png "Saída da consulta de estatísticas de execução")

Execute a consulta abaixo para obter essa saída. Para obter mais informações sobre a exibição de gerenciamento dinâmico usada, confira [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). A consulta retorna apenas as funções que foram executadas mais de uma vez.

```sql
SELECT language, counter_name, counter_value
FROM sys.dm_external_script_execution_stats
WHERE counter_value > 0
ORDER BY language, counter_name;
```

A consulta retorna as seguintes colunas:

| Coluna | Descrição |
|--------|-------------|
| Linguagem | Nome da linguagem de script externo registrada. |
| counter_name | Nome de uma função de script externo registrada. |
| counter_value | Número total de instâncias nas quais a função de script externo registrada foi chamada no servidor. Esse valor é cumulativo, começando com a hora em que o recurso foi instalado na instância, e não pode ser redefinido. |

## <a name="performance-counters"></a>Contadores de desempenho

Exiba os contadores de desempenho relacionados à execução de scripts externos.

![Saída da consulta de contadores de desempenho](media/dmv-performance-counters.png "Saída da consulta de contadores de desempenho")

Execute a consulta abaixo para obter essa saída. Para obter mais informações sobre a exibição de gerenciamento dinâmico usada, confira [sys.dm_os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md).

```sql
SELECT counter_name, cntr_value
FROM sys.dm_os_performance_counters 
WHERE object_name LIKE '%External Scripts%'
```

**sys.dm_os_performance_counters** gera os seguintes contadores de desempenho para scripts externos:

| Contador | Descrição |
|---------|-------------|
| Total de Execuções | Número de processos externos iniciados por chamadas locais ou remotas. |
| Execuções paralelas | Número de vezes que um script incluiu a especificação _\@parallel_ e que o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] foi capaz de gerar e usar um plano de consulta paralela. |
| Execuções de streaming | Número de vezes que o recurso de streaming foi invocado. |
| Execuções de CC do SQL | Número execuções de scripts externos em que a chamada foi instanciada remotamente e em que o SQL Server foi usado como contexto de computação. |
| Autenticação Implícita. Logons | Número de vezes que foi feita uma chamada de loopback de ODBC usando a autenticação implícita, ou seja, o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] executou a chamada em nome do usuário que estava enviando a solicitação de script. |
| Tempo total de execução (ms) | Tempo decorrido entre a chamada e a conclusão da chamada. |
| Erros de Execução | Número de vezes que os scripts relataram erros. Essa contagem não inclui erros de R ou Python. |

## <a name="memory-usage"></a>Uso de memória

Exiba informações sobre a memória usada pelo sistema operacional, o SQL Server e os pools externos.

![Saída da consulta de uso de memória](media/dmv-memory-usage.png "Saída da consulta de uso de memória")

Execute a consulta abaixo para obter essa saída. Para obter mais informações sobre as exibições de gerenciamento dinâmico usadas, confira [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) e [sys.dm_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md).

```sql
SELECT physical_memory_kb, committed_kb
    , (SELECT SUM(peak_memory_kb)
        FROM sys.dm_resource_governor_external_resource_pools AS ep
        ) AS external_pool_peak_memory_kb
FROM sys.dm_os_sys_info;
```

A consulta retorna as seguintes colunas:

| Coluna | Descrição |
|--------|-------------|
| physical_memory_kb | A quantidade total de memória física no computador. |
| committed_kb | A memória comprometida, em KB (quilobytes), no gerenciador de memória. Não inclui a memória reservada no gerenciador de memória. |
| external_pool_peak_memory_kb | A soma da quantidade máxima de memória usada, em quilobytes, para todos os pools de recursos externos. |

## <a name="memory-configuration"></a>Configuração de memória

Exiba informações sobre a configuração de memória máxima em percentual, do SQL Server e dos pools de recursos externos. Se o SQL Server estiver sendo executado com o valor padrão de `max server memory (MB)`, ele será considerado como 100% da memória do sistema operacional.

![Saída da consulta de configuração de memória](media/dmv-memory-configuration.png "Saída da consulta de configuração de memória")

Execute a consulta abaixo para obter essa saída. Para obter mais informações sobre as exibições usadas, confira [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) e [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md).

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

A consulta retorna as seguintes colunas:

| Coluna | Descrição |
|--------|-------------|
| name | Nome do pool de recursos externos ou do SQL Server. |
| max_memory_percent | A memória máxima que SQL Server ou o pool de recursos externos pode usar. |

## <a name="resource-pools"></a>Pools de recursos

No [Resource Governor do SQL Server](../../relational-databases/resource-governor/resource-governor.md), um [pool de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md) representa um subconjunto dos recursos físicos de uma instância. Você pode especificar limites de quantidade de CPU, E/S física e memória que as solicitações recebidas de aplicativos podem usar, incluindo a execução de scripts externos, dentro do pool de recursos. Exiba os pools de recursos usados para SQL Server e scripts externos.

![Saída da consulta de pools de recursos](media/dmv-resource-pools.png "Saída da consulta de pools de recursos")

Execute a consulta abaixo para obter essa saída. Para obter mais informações sobre as exibições de gerenciamento dinâmico usadas, confira [sys.dm_resource_governor_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md) e [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md).

```sql
SELECT CONCAT ('SQL Server - ', p.name) AS pool_name
    , p.total_cpu_usage_ms, p.read_io_completed_total, p.write_io_completed_total
FROM sys.dm_resource_governor_resource_pools AS p
UNION ALL
SELECT CONCAT ('External Pool - ', ep.name) AS pool_name
    , ep.total_cpu_user_ms, ep.read_io_count, ep.write_io_count
FROM sys.dm_resource_governor_external_resource_pools AS ep;
```

A consulta retorna as seguintes colunas:

| Coluna | Descrição |
|--------|-------------|
| pool_name | Nome do pool de recursos. Os pools de recursos do SQL Server são prefixados com `SQL Server` e os pools de recursos externos são prefixados com `External Pool`.
| total_cpu_usage_hours | O uso cumulativo de CPU em milissegundos desde que as estatísticas do Resource Governor foram redefinidas. |
| read_io_completed_total | O total de E/S lidas concluídas desde que as estatísticas do Administrador de Recursos foram redefinidas. |
| write_io_completed_total | O total de E/Ss de gravação concluídas desde que as estatísticas do Administrador de Recursos foram redefinidas. |

## <a name="installed-packages"></a>Pacotes instalados

Você pode exibir os pacotes de R e Python que estão instalados nos Serviços de Machine Learning do SQL Server executando um script de R ou Python, exibindo-os como saída.

### <a name="installed-packages-for-r"></a>Pacotes instalados para o R

Exiba os pacotes de R instalados nos Serviços de Machine Learning do SQL Server.

![Saída da consulta de pacotes instalados para R](media/dmv-installed-packages-r.png "Saída da consulta de pacotes instalados para R")

Execute a consulta abaixo para obter essa saída. A consulta usa um script de R para determinar os pacotes de R instalados com SQL Server.

```sql
EXEC sp_execute_external_script @language = N'R'
, @script = N'
OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
    , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
```

As colunas retornadas são:

| Coluna | Descrição |
|--------|-------------|
| Pacote | Nome do pacote instalado. |
| Versão | Versão do pacote. |
| Depende | Lista os pacotes dos quais o pacote instalado depende. |
| Licença | Licença para o pacote instalado. |
| LibPath | Diretório em que você encontra o pacote. |

### <a name="installed-packages-for-python"></a>Pacotes instalados para Python

Exiba os pacotes do Python instalados nos Serviços de Machine Learning do SQL Server.

![Saída da consulta de pacotes instalados para Python](media/dmv-installed-packages-python.png "Saída da consulta de pacotes instalados para Python")

Execute a consulta abaixo para obter essa saída. A consulta usa um script de Python para determinar os pacotes de Python instalados com SQL Server.

```sql
EXEC sp_execute_external_script @language = N'Python'
, @script = N'
import pip
OutputDataSet = pandas.DataFrame([(i.key, i.version, i.location) for i in pip.get_installed_distributions()])'
WITH result sets((Package NVARCHAR(128), Version NVARCHAR(128), Location NVARCHAR(1000)));
```

As colunas retornadas são:

| Coluna | Descrição |
|--------|-------------|
| Pacote | Nome do pacote instalado. |
| Versão | Versão do pacote. |
| Location | Diretório em que você encontra o pacote. |

## <a name="next-steps"></a>Próximas etapas

+ [Eventos estendidos para aprendizado de máquina](extended-events.md)
+ [Exibições de gerenciamento dinâmico relacionadas ao Resource Governor](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)
+ [Exibições de gerenciamento dinâmico do sistema](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
+ [Monitorar o aprendizado de máquina usando relatórios personalizados no Management Studio](monitor-sql-server-machine-learning-services-using-custom-reports-management-studio.md)
