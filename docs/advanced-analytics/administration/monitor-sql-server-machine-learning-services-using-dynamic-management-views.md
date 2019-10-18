---
title: Monitorar a execução de script do Python e do R usando DMVs
description: Use DMVs (exibições de gerenciamento dinâmico) para monitorar a execução de script externo do Python e do R no SQL Server Serviços de Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8333da0bd3b5b4ad4f0b377edec110e30565c273
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2019
ms.locfileid: "71713186"
---
# <a name="monitor-sql-server-machine-learning-services-using-dynamic-management-views-dmvs"></a>Monitorar SQL Server Serviços de Machine Learning usando DMVs (exibições de gerenciamento dinâmico)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Use DMVs (exibições de gerenciamento dinâmico) para monitorar a execução de scripts externos (Python e R), os recursos usados, diagnosticar problemas e ajustar o desempenho no Serviços de Machine Learning SQL Server.

Neste artigo, você encontrará as DMVs específicas para SQL Server Serviços de Machine Learning. Você também encontrará consultas de exemplo que mostram:

+ Configurações e opções de configuração para o aprendizado de máquina
+ Sessões ativas executando Python ou scripts externos
+ Estatísticas de execução para o tempo de execução externo para Python e R
+ Contadores de desempenho para scripts externos
+ Uso de memória para o sistema operacional, SQL Server e pools de recursos externos
+ Configuração de memória para pools de recursos externos e SQL Server
+ Resource Governor pools de recursos, incluindo pools de recursos externos
+ Pacotes instalados para Python e R

Para obter mais informações gerais sobre DMVs, consulte [exibições de gerenciamento dinâmico do sistema](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).

> [!TIP]
> Você também pode usar os relatórios personalizados para monitorar SQL Server Serviços de Machine Learning. Para obter mais informações, consulte [monitorar o Machine Learning usando relatórios personalizados no Management Studio](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md).

## <a name="dynamic-management-views"></a>Exibições de gerenciamento dinâmico

As exibições de gerenciamento dinâmico a seguir podem ser usadas ao monitorar cargas de trabalho de Machine Learning no SQL Server. Para consultar as DMVs, você precisará de `VIEW SERVER STATE` permissão na instância.

| Exibição de gerenciamento dinâmico | Escreva | Description |
|-------------------------|------|-------------|
| [sys. dm _external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) | Chão | Retorna uma linha para cada conta de trabalho ativa que está executando um script externo. |
| [sys. dm _external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) | Chão | Retorna uma linha para cada tipo de solicitação de script externo. |
| [sys. dm _os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md) | Chão | Retorna uma linha por contador de desempenho mantida pelo servidor. Se você usar o critério de pesquisa `WHERE object_name LIKE '%External Scripts%'`, poderá usar essas informações para ver quantos scripts foram executados, quais scripts foram executado usando o modo de autenticação ou quantas chamadas de R ou Python foram emitidas na instância em geral. |
| [sys. dm _resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) | Administrador de Recursos | Retorna informações sobre o estado atual do pool de recursos externos no Resource Governor, a configuração atual de pools de recursos e as estatísticas do pool de recursos. |
| [sys. dm _resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md) | Administrador de Recursos | Retorna informações de afinidade de CPU sobre a configuração atual do pool de recursos externos no Resource Governor. Retorna uma linha por Agendador em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] onde cada Agendador é mapeado para um processador individual. Use esta exibição para monitorar a condição de um Agendador ou para identificar tarefas de fuga. |

Para obter informações sobre como monitorar instâncias de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], consulte [exibições de catálogo](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md) e [resource governor exibições de gerenciamento dinâmico relacionadas](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md).

## <a name="settings-and-configuration"></a>Configurações e configuração

Exiba a configuração de Serviços de Machine Learning instalação e as opções de configuração.

![Saída da consulta configurações e configuração](media/dmv-settings-and-configuration.png "Saída da consulta configurações e configuração")

Execute a consulta abaixo para obter essa saída. Para obter mais informações sobre as exibições e funções usadas, consulte [Sys. dm _server_registry](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md), [Sys. Configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)e [ServerProperty](../../t-sql/functions/serverproperty-transact-sql.md).

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

| Pilha | Description |
|--------|-------------|
| IsMLServicesInstalled | Retornará 1 se SQL Server Serviços de Machine Learning for instalado para a instância. Caso contrário, retornará 0. |
| ExternalScriptsEnabled | Retornará 1 se scripts externos estiverem habilitados para a instância. Caso contrário, retornará 0. |
| ImpliedAuthenticationEnabled | Retornará 1 se a autenticação implícita estiver habilitada. Caso contrário, retornará 0. A configuração de autenticação implícita é verificada verificando se existe um logon para SQLRUserGroup. |
| IsTcpEnabled | Retornará 1 se o protocolo TCP/IP estiver habilitado para a instância. Caso contrário, retornará 0. Para obter mais informações, consulte [padrão SQL Server configuração do protocolo de rede](../../database-engine/configure-windows/default-sql-server-network-protocol-configuration.md). |

## <a name="active-sessions"></a>Sessões ativas

Exibir as sessões ativas que executam scripts externos.

![Saída da consulta de configurações ativas](media/dmv-active-sessions.png "Saída da consulta de configurações ativas")

Execute a consulta abaixo para obter essa saída. Para obter mais informações sobre as exibições de gerenciamento dinâmico usadas, consulte [Sys. dm _exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md), [Sys. dm _external_script_requests](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)e [Sys. dm _exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md).

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

| Pilha | Description |
|--------|-------------|
| session_id | Identifica a sessão associada a cada conexão primária ativa. |
| blocking_session_id | ID da sessão que está bloqueando a solicitação. Se esta coluna for nula, a solicitação não será bloqueada ou as informações de sessão da sessão de bloqueio não estarão disponíveis (ou não poderão ser identificadas). |
| Estado | Status da solicitação. |
| database_name | Nome do banco de dados atual para cada sessão. |
| login_name | SQL Server nome de logon sob o qual a sessão está em execução no momento. |
| wait_time | Se a solicitação estiver bloqueada no momento, essa coluna retornará a duração em milissegundos da espera atual. Não permite valor nulo. |
| wait_type | Se a solicitação estiver bloqueada no momento, essa coluna retornará o tipo de espera. Para obter informações sobre os tipos de esperas, consulte [Sys. dm _os_wait_stats](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md). |
| last_wait_type | Se essa solicitação tiver sido bloqueada anteriormente, essa coluna retornará o tipo da última espera. |
| total_elapsed_time | Tempo total decorrido em milissegundos desde a chegada da solicitação. |
| cpu_time | Tempo de CPU em milissegundos que é usado pela solicitação. |
| pareça | Número de leituras executadas por essa solicitação. |
| logical_reads | Número de leituras lógicas que foram executadas pela solicitação. |
| registra | Número de gravações executadas por essa solicitação. |
| idioma | Palavra-chave que representa uma linguagem de script com suporte. |
| degree_of_parallelism | Número que indica o número de processos paralelos que foram criados. Esse valor pode ser diferente do número de processos paralelos que foram solicitados. |
| external_user_name | A conta de trabalho do Windows sob a qual o script foi executado. |

## <a name="execution-statistics"></a>Estatísticas de execução

Exiba as estatísticas de execução para o tempo de execução externo para R e Python. Somente as estatísticas de funções de pacote RevoScaleR, revoscalepy ou microsoftml estão disponíveis no momento.

![Saída da consulta de estatísticas de execução](media/dmv-execution-statistics.png "Saída da consulta de estatísticas de execução")

Execute a consulta abaixo para obter essa saída. Para obter mais informações sobre a exibição de gerenciamento dinâmico usada, consulte [Sys. dm _external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). A consulta retorna apenas as funções que foram executadas mais de uma vez.

```sql
SELECT language, counter_name, counter_value
FROM sys.dm_external_script_execution_stats
WHERE counter_value > 0
ORDER BY language, counter_name;
```

A consulta retorna as seguintes colunas:

| Pilha | Description |
|--------|-------------|
| idioma | Nome da linguagem de script externo registrada. |
| counter_name | Nome de uma função de script externo registrada. |
| counter_value | Número total de instâncias em que a função de script externo registrada foi chamada no servidor. Esse valor é cumulativo, começando com a hora em que o recurso foi instalado na instância do e não pode ser redefinido. |

## <a name="performance-counters"></a>Contadores de desempenho

Exiba os contadores de desempenho relacionados à execução de scripts externos.

![Saída da consulta de contadores de desempenho](media/dmv-performance-counters.png "Saída da consulta de contadores de desempenho")

Execute a consulta abaixo para obter essa saída. Para obter mais informações sobre a exibição de gerenciamento dinâmico usada, consulte [Sys. dm _os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md).

```sql
SELECT counter_name, cntr_value
FROM sys.dm_os_performance_counters 
WHERE object_name LIKE '%External Scripts%'
```

**Sys. dm _os_performance_counters** gera os seguintes contadores de desempenho para scripts externos:

| Neutraliza | Description |
|---------|-------------|
| Total de execuções | Número de processos externos iniciados por chamadas locais ou remotas. |
| Execuções paralelas | Número de vezes que um script incluiu a especificação de _\@parallel_ e que [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] foi capaz de gerar e usar um plano de consulta paralelo. |
| Execuções de streaming | Número de vezes que o recurso de streaming foi invocado. |
| Execuções de SQL CC | Número de scripts externos executados onde a chamada foi instanciada remotamente e SQL Server foi usada como o contexto de computação. |
| Autorizações implícitas. logons | Número de vezes que uma chamada de loopback ODBC foi feita usando a autenticação implícita; ou seja, a [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] executou a chamada em nome do usuário que está enviando a solicitação de script. |
| Tempo total de execução (MS) | Tempo decorrido entre a chamada e a conclusão da chamada. |
| Erros de execução | Número de vezes que os scripts relataram erros. Essa contagem não inclui erros de R ou Python. |

## <a name="memory-usage"></a>Uso de memória

Exiba informações sobre a memória usada pelo sistema operacional, SQL Server e os pools externos.

![Saída da consulta de uso de memória](media/dmv-memory-usage.png "Saída da consulta de uso de memória")

Execute a consulta abaixo para obter essa saída. Para obter mais informações sobre as exibições de gerenciamento dinâmico usadas, consulte [Sys. dm _resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) e [Sys. dm _os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md).

```sql
SELECT physical_memory_kb, committed_kb
    , (SELECT SUM(peak_memory_kb)
        FROM sys.dm_resource_governor_external_resource_pools AS ep
        ) AS external_pool_peak_memory_kb
FROM sys.dm_os_sys_info;
```

A consulta retorna as seguintes colunas:

| Pilha | Description |
|--------|-------------|
| physical_memory_kb | A quantidade total de memória física no computador. |
| committed_kb | A memória confirmada em kilobytes (KB) no Gerenciador de memória. Não inclui memória reservada no Gerenciador de memória. |
| external_pool_peak_memory_kb | A soma da quantidade máxima de memória usada, em quilobytes, para todos os pools de recursos externos. |

## <a name="memory-configuration"></a>Configuração de memória

Exiba informações sobre a configuração de memória máxima em porcentagem de SQL Server e pools de recursos externos. Se SQL Server estiver sendo executado com o valor padrão de `max server memory (MB)`, ele será considerado como 100% da memória do sistema operacional.

![Saída da consulta de configuração de memória](media/dmv-memory-configuration.png "Saída da consulta de configuração de memória")

Execute a consulta abaixo para obter essa saída. Para obter mais informações sobre as exibições usadas, consulte [Sys. Configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) e [Sys. dm _resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md).

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

| Pilha | Description |
|--------|-------------|
| Nomes | Nome do pool de recursos externo ou SQL Server. |
| max_memory_percent | A memória máxima que SQL Server ou o pool de recursos externos pode usar. |

## <a name="resource-pools"></a>Pools de recursos

No [SQL Server Resource Governor](../../relational-databases/resource-governor/resource-governor.md), um [pool de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md) representa um subconjunto dos recursos físicos de uma instância. Você pode especificar limites na quantidade de CPU, e/s física e memória que as solicitações de aplicativos de entrada, incluindo a execução de scripts externos, podem usar dentro do pool de recursos. Exiba os pools de recursos usados para SQL Server e scripts externos.

![Saída da consulta de pools de recursos](media/dmv-resource-pools.png "Saída da consulta de pools de recursos")

Execute a consulta abaixo para obter essa saída. Para obter mais informações sobre as exibições de gerenciamento dinâmico usadas, consulte [Sys. dm _resource_governor_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md) e [Sys. dm _resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md).

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

| Pilha | Description |
|--------|-------------|
| pool_name | Nome do pool de recursos. SQL Server pools de recursos são prefixados com `SQL Server` e os pools de recursos externos são prefixados com `External Pool`.
| total_cpu_usage_hours | O uso de CPU cumulativo em milissegundos desde que as estatísticas de administrador de recursos foram redefinidas. |
| read_io_completed_total | O total de leitura do IOs foi concluído desde que as estatísticas de administrador de recurso foram redefinidas. |
| write_io_completed_total | O IOs de gravação total foi concluído desde que as estatísticas de administrador de recurso foram redefinidas. |

## <a name="installed-packages"></a>Pacotes instalados

Você pode exibir os pacotes R e Python que estão instalados em SQL Server Serviços de Machine Learning executando um script R ou Python que os gera.

### <a name="installed-packages-for-r"></a>Pacotes instalados para o R

Exiba os pacotes do R instalados no Serviços de Machine Learning SQL Server.

![Saída dos pacotes instalados para consulta de R](media/dmv-installed-packages-r.png "Saída dos pacotes instalados para consulta de R")

Execute a consulta abaixo para obter essa saída. A consulta usa um script R para determinar pacotes de R instalados com SQL Server.

```sql
EXEC sp_execute_external_script @language = N'R'
, @script = N'
OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
    , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
```

As colunas retornadas são:

| Pilha | Description |
|--------|-------------|
| Agrupa | Nome do pacote instalado. |
| Versão | Versão do pacote. |
| Dependem | Lista os pacotes dos quais o pacote instalado depende. |
| carteira | Licença para o pacote instalado. |
| LibPath | Diretório onde você pode encontrar o pacote. |

### <a name="installed-packages-for-python"></a>Pacotes instalados para Python

Exiba os pacotes do Python instalados no SQL Server Serviços de Machine Learning.

![Saída dos pacotes instalados para a consulta do Python](media/dmv-installed-packages-python.png "Saída dos pacotes instalados para a consulta do Python")

Execute a consulta abaixo para obter essa saída. A consulta usa um script Python para determinar os pacotes do Python instalados com o SQL Server.

```sql
EXEC sp_execute_external_script @language = N'Python'
, @script = N'
import pip
OutputDataSet = pandas.DataFrame([(i.key, i.version, i.location) for i in pip.get_installed_distributions()])'
WITH result sets((Package NVARCHAR(128), Version NVARCHAR(128), Location NVARCHAR(1000)));
```

As colunas retornadas são:

| Pilha | Description |
|--------|-------------|
| Agrupa | Nome do pacote instalado. |
| Versão | Versão do pacote. |
| Local | Diretório onde você pode encontrar o pacote. |

## <a name="next-steps"></a>Próximas etapas

+ [Gerenciando e monitorando soluções de aprendizado de máquina](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)
+ [Eventos estendidos para o aprendizado de máquina](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md)
+ [Resource Governor exibições de gerenciamento dinâmico relacionadas](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)
+ [Exibições de gerenciamento dinâmico do sistema](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
+ [Monitorar o Machine Learning usando relatórios personalizados no Management Studio](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)
