---
title: ALTER DATABASE SCOPED CONFIGURATION
description: Habilita várias definições de configuração de banco de dados no nível do banco de dados individual.
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 10/31/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- ALTER_DATABASE_SCOPED_CONFIGURATION
- ALTER_DATABASE_SCOPED_CONFIGURATION_TSQL
- DATABASE_SCOPED_CONFIGURATION_TSQL
- SCOPED_CONFIGURATION_TSQL
- SCOPED_TSQL
- ALTER_DATABASE_SCOPED_TSQL
- DATABASE_SCOPED_TSQL
helpviewer_keywords:
- ALTER DATABASE SCOPED CONFIGURATION statement
- configuration [SQL Server], ALTER DATABASE SCOPED CONFIGURATION statement
ms.assetid: 63373c2f-9a0b-431b-b9d2-6fa35641571a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: db98f5aa3cdec76b59e51f743200b24725231f95
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76831634"
---
# <a name="alter-database-scoped-configuration-transact-sql"></a>ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Essa instrução permite várias definições de configuração de banco de dados no nível do **banco de dados individual**. Essa instrução está disponível no [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)] e no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] começando pelo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Essas configurações são:

- Limpar o cache de procedimento.
- Definir o parâmetro MAXDOP para um valor arbitrário (1, 2,...) para o banco de dados primário com base naquilo que funciona melhor para esse banco de dados específico e definir um valor diferente (como 0) para todos os bancos de dados secundários usados (como para consultas de relatórios).
- Defina o modelo de estimativa de cardinalidade do otimizador de consulta independente do nível de compatibilidade do banco de dados.
- Habilitar ou desabilitar a detecção de parâmetro no nível do banco de dados.
- Habilitar ou desabilitar hotfixes de otimização de consulta no nível do banco de dados.
- Habilitar ou desabilitar o cache de identidade no nível do banco de dados.
- Habilitar ou desabilitar um stub de plano compilado para ser armazenado em cache quando um lote for compilado pela primeira vez.
- Habilite ou desabilite a coleta de estatísticas de execução para módulos T-SQL compilados nativamente.
- Habilitar ou desabilitar online pelas opções padrão para instruções DDL compatíveis com a sintaxe `ONLINE =`.
- Habilitar ou desabilitar retomáveis pelas opções padrão para instruções DDL compatíveis com a sintaxe `RESUMABLE =`.
- Habilite ou desabilite recursos de [processamento de consulta inteligente](../../relational-databases/performance/intelligent-query-processing.md).
- Habilitar ou desabilitar a imposição de plano acelerada.
- Habilitar ou desabilitar a funcionalidade de remoção automática de tabelas temporárias globais.
- Habilite ou desabilite a [infraestrutura de criação de perfil de consulta leve](../../relational-databases/performance/query-profiling-infrastructure.md).
- Habilitar ou desabilitar a nova mensagem de erro `String or binary data would be truncated`.
- Habilitar ou desabilitar a coleta do último plano de execução real em [sys.dm_exec_query_plan_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md).
- Especifique o número de minutos que uma operação de índice retomável em pausa permanece assim antes de ser anulada automaticamente pelo mecanismo do SQL Server.

![Ícone de link](../../database-engine/configure-windows/media/topic-link.gif "ícone de link") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>Sintaxe

```
ALTER DATABASE SCOPED CONFIGURATION
{
    { [ FOR SECONDARY] SET <set_options>}
}
| CLEAR PROCEDURE_CACHE [plan_handle]
| SET < set_options >
[;]

< set_options > ::=
{
    MAXDOP = { <value> | PRIMARY}
    | LEGACY_CARDINALITY_ESTIMATION = { ON | OFF | PRIMARY}
    | PARAMETER_SNIFFING = { ON | OFF | PRIMARY}
    | QUERY_OPTIMIZER_HOTFIXES = { ON | OFF | PRIMARY}
    | IDENTITY_CACHE = { ON | OFF }
    | INTERLEAVED_EXECUTION_TVF = { ON | OFF }
    | BATCH_MODE_MEMORY_GRANT_FEEDBACK = { ON | OFF }
    | BATCH_MODE_ADAPTIVE_JOINS = { ON | OFF }
    | TSQL_SCALAR_UDF_INLINING = { ON | OFF }
    | ELEVATE_ONLINE = { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED }
    | ELEVATE_RESUMABLE = { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED }
    | OPTIMIZE_FOR_AD_HOC_WORKLOADS = { ON | OFF }
    | XTP_PROCEDURE_EXECUTION_STATISTICS = { ON | OFF }
    | XTP_QUERY_EXECUTION_STATISTICS = { ON | OFF }
    | ROW_MODE_MEMORY_GRANT_FEEDBACK = { ON | OFF }
    | BATCH_MODE_ON_ROWSTORE = { ON | OFF }
    | DEFERRED_COMPILATION_TV = { ON | OFF }
    | ACCELERATED_PLAN_FORCING = { ON | OFF }
    | GLOBAL_TEMPORARY_TABLE_AUTODROP = { ON | OFF }
    | LIGHTWEIGHT_QUERY_PROFILING = { ON | OFF }
    | VERBOSE_TRUNCATION_WARNINGS = { ON | OFF }
    | LAST_QUERY_PLAN_STATS = { ON | OFF }
    | PAUSED_RESUMABLE_INDEX_ABORT_DURATION_MINUTES = <time>
    | ISOLATE_SECURITY_POLICY_CARDINALITY  = { ON | OFF }
}
```

> [!IMPORTANT]
> Começando com [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e em [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], alguns nomes de opções foram alterados:      
> -  `DISABLE_INTERLEAVED_EXECUTION_TVF` foi alterado para `INTERLEAVED_EXECUTION_TVF`
> -  `DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK` foi alterado para `BATCH_MODE_MEMORY_GRANT_FEEDBACK`
> -  `DISABLE_BATCH_MODE_ADAPTIVE_JOINS` foi alterado para `BATCH_MODE_ADAPTIVE_JOINS`

## <a name="arguments"></a>Argumentos

FOR SECONDARY

Especifica as definições para bancos de dados secundários (todos os bancos de dados secundários precisam ter valores idênticos).

CLEAR PROCEDURE_CACHE [plan_handle]

Limpa o cache do procedimento (plano) para o banco de dados e pode ser executado tanto no primário quanto no secundário.

Especifique um identificador de plano de consulta para limpar um único plano de consulta do cache do plano.

**APLICA-SE A**: Especificar um identificador de plano de consulta está disponível no Banco de Dados SQL do Azure e no SQL Server 2019 ou superior.

MAXDOP **=** {\<value> | PRIMARY } **\<value>**

Especifica a configuração **MAXDOP (grau máximo de paralelismo)** padrão que deve ser usada nas instruções. 0 é o valor padrão e indica que a configuração do servidor será usada. O MAXDOP no escopo do banco de dados (a menos que esteja definido como 0) substitui o **max degree of parallelism** definido no nível do servidor por sp_configure. As dicas de consulta ainda podem substituir o MAXDOP no escopo do banco de dados para ajustar consultas específicas que precisem de uma configuração diferente. Todas essas configurações são limitadas pelo MAXDOP definido para o [Grupo de carga de trabalho](create-workload-group-transact-sql.md).

É possível usar a opção MAXDOP para limitar o número de processadores a serem usados na execução paralela do plano. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera os planos de execução paralela para consultas, operações DDL (linguagem de definição de dados), inserção paralela, alteração online de coluna, coleta de estatísticas paralela e população de cursor estático e controlado por conjunto de chaves.

> [!NOTE]
> O limite de **MAXDOP (grau máximo de paralelismo)** é definido por [tarefa](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md). Não é um limite por [solicitação](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) ou por consulta. Isso significa que, durante uma execução de consulta paralela, uma solicitação única pode gerar várias tarefas que são atribuídas a um [agendador](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md). Para saber mais, confira o [Guia de arquitetura de threads e tarefas](../../relational-databases/thread-and-task-architecture-guide.md). 

Para definir essa opção no nível da instância, confira [Configurar a opção max degree of parallelism de configuração do servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).

> [!NOTE]
> No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], a configuração de **grau máximo de paralelismo** em nível de servidor é sempre definida como 0. MAXDOP pode ser configurado para cada banco de dados, conforme descrito no artigo atual. Para obter recomendações sobre como configurar o MAXDOP de forma ideal, consulte a seção [Recursos Adicionais](#additional-resources).

> [!TIP]
> Para fazer isso no nível da consulta, use o **MAXDOP**, [dica de consulta](../../t-sql/queries/hints-transact-sql-query.md).    
> Para fazer isso no nível do servidor, use o **MAXDOP (grau máximo de paralelismo)** na [opção de configuração do servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).     
> Para fazer isso no nível de carga de trabalho, use a [opção de configuração de grupo de carga de trabalho do Resource Governor](../../t-sql/statements/create-workload-group-transact-sql.md) **MAX_DOP**.    

PRIMARY

Só pode ser definida para os secundários, enquanto o banco de dados está no primário e indica que a configuração será a definida para o primário. Se a configuração do primário for alterada, o valor nos secundários será alterado da maneira apropriada sem precisar ser definido explicitamente. **PRIMARY** é a configuração padrão dos secundários.

LEGACY_CARDINALITY_ESTIMATION **=** { ON | **OFF** | PRIMARY }

Permite que você defina o modelo de estimativa de cardinalidade do otimizador de consulta para o SQL Server 2012 e versões anteriores independentemente do nível de compatibilidade do banco de dados. O padrão é **OFF**, que define o modelo de estimativa de cardinalidade do otimizador de consulta com base no nível de compatibilidade do banco de dados. Configurar LEGACY_CARDINALITY_ESTIMATION como **ON** equivale a habilitar [Sinalizador de Rastreamento 9481](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).

> [!TIP]
> Para fazer isso no nível da consulta, adicione a [dica de consulta](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) do **QUERYTRACEON**.
> Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1, para fazer isso no nível da consulta, adicione a [dica de consulta](../../t-sql/queries/hints-transact-sql-query.md#use_hint) **USE HINT** em vez de usar o sinalizador de rastreamento.

PRIMARY

Esse valor só é válido nos secundários enquanto o banco de dados está no primário e especifica que a configuração do modelo de estimativa de cardinalidade do otimizador de consulta em todos os secundários será o valor definido para o primário. Se a configuração no primário para o modelo de estimativa de cardinalidade do otimizador de consulta for alterado, o valor nos secundários será alterado da maneira adequada. **PRIMARY** é a configuração padrão dos secundários.

PARAMETER_SNIFFING **=** { **ON** | OFF | PRIMARY}

Habilita ou desabilita a [detecção de parâmetro](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing). O padrão é ON. Configurar PARAMETER_SNIFFING como OFF equivale a habilitar [Sinalizador de Rastreamento 4136](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).

> [!TIP]
> Para fazer isso no nível da consulta, confira a [dica de consulta](../../t-sql/queries/hints-transact-sql-query.md) **OPTIMIZE FOR UNKNOWN**.
> Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1, para fazer isso no nível da consulta, a [dica de consulta](../../t-sql/queries/hints-transact-sql-query.md#use_hint) **USE HINT** também está disponível.

PRIMARY

Esse valor só é válido nos secundários enquanto o banco de dados está no primário e especifica que o valor dessa configuração em todos os secundários será o valor definido para o primário. Se a configuração do primário para o uso de [detecção de parâmetro](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing) fora alterada, o valor nos secundários será alterado da maneira apropriada sem a necessidade de definir o valor dos secundários explicitamente. PRIMARY é a configuração padrão dos secundários.

<a name="qo_hotfixes"></a> QUERY_OPTIMIZER_HOTFIXES **=** { ON | **OFF** | PRIMARY }

Habilita ou desabilita os hotfixes de otimização de consulta, independentemente do nível de compatibilidade do banco de dados. O padrão é **OFF**, que desabilita os hotfixes de otimização de consulta que foram lançados depois que o nível de compatibilidade mais alto disponível foi introduzido para uma versão específica de (pós-RTM). Definir como **ON** equivale a habilitar o [sinalizador de rastreamento 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).

> [!TIP]
> Para fazer isso no nível da consulta, adicione a [dica de consulta](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) do **QUERYTRACEON**.
> Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1, para fazer isso no nível da consulta, adicione a [dica de consulta](../../t-sql/queries/hints-transact-sql-query.md#use_hint) USE HINT em vez de usar o sinalizador de rastreamento.

PRIMARY

Esse valor só é válido nos secundários enquanto o banco de dados está no primário e especifica que o valor dessa configuração em todos os secundários será o valor definido para o primário. Se a configuração do primário for alterada, o valor nos secundários será alterado da maneira apropriada sem precisar ser definido explicitamente. PRIMARY é a configuração padrão dos secundários.

IDENTITY_CACHE **=** { **ON** | OFF }

**APLICA-SE A**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

Habilita ou desabilita o cache de identidade no nível do banco de dados. O padrão é **ON**. O cache de identidade é usado para melhorar o desempenho de INSERT em tabelas com colunas de identidade. Para evitar lacunas nos valores de uma coluna de identidade em casos em que o servidor é reiniciado inesperadamente ou efetua failover para um servidor secundário, desabilite a opção IDENTITY_CACHE. Essa opção é semelhante ao [sinalizador de rastreamento 272](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) existente, exceto que ela pode ser definida no nível do banco de dados em vez de apenas no nível do servidor.

> [!NOTE]
> Essa opção só pode ser definida para o primário. Para obter mais informações, confira [colunas de identidade](create-table-transact-sql-identity-property.md).

INTERLEAVED_EXECUTION_TVF **=** { **ON** | OFF }

**APLICA-SE A**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

Permite habilitar ou desabilitar a execução intercalada para funções com valor de tabela com várias instruções no escopo do banco de dados ou da instrução, mantendo o nível de compatibilidade do banco de dados como 140 e superior. A execução intercalada é um recurso que faz parte do processamento de consulta adaptável em [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Para saber mais, confira [Processamento de consulta inteligente](../../relational-databases/performance/intelligent-query-processing.md).

> [!NOTE]
> Para o nível de compatibilidade do banco de dados 130 ou menor, esta configuração com escopo de banco de dados não tem nenhum efeito.
>
> Somente no SQL Server 2017 (14.x), a opção INTERLEAVED_EXECUTION_TVF tinha o nome mais antigo **DISABLE**_INTERLEAVED_EXECUTION_TVF.

BATCH_MODE_MEMORY_GRANT_FEEDBACK **=** { **ON** | OFF}

**APLICA-SE A**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

Permite habilitar ou desabilitar Comentários de concessão de memória de modo de lote no escopo do banco de dados, mantendo o nível de compatibilidade do banco de dados como 140 e superior. Os comentários de concessão de memória de modo de lote é um recurso que faz parte do [Processamento de consulta inteligente](../../relational-databases/performance/intelligent-query-processing.md) introduzido no [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)].

> [!NOTE]
> Para o nível de compatibilidade do banco de dados 130 ou menor, esta configuração com escopo de banco de dados não tem nenhum efeito.

BATCH_MODE_ADAPTIVE_JOINS **=** { **ON** | OFF}

**APLICA-SE A**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

Permite habilitar ou desabilitar junções adaptáveis do modo de lote no escopo do banco de dados, mantendo o nível de compatibilidade do banco de dados como 140 e superior. As junções adaptáveis do modo de lote é um recurso que faz parte do [Processamento de consulta inteligente](../../relational-databases/performance/intelligent-query-processing.md) introduzido no [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)].

> [!NOTE]
> Para o nível de compatibilidade do banco de dados 130 ou menor, esta configuração com escopo de banco de dados não tem nenhum efeito.

TSQL_SCALAR_UDF_INLINING **=** { **ON** | OFF }

**APLICA-SE A**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando pelo [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (o recurso está em versão prévia pública)

Permite habilitar ou desabilitar o inlining UDF do T-SQL Scalar no escopo do banco de dados, mantendo o nível de compatibilidade do banco de dados como 150 e superior. O inlining UDF Escalar do T-SQL faz parte da família de recursos de [Processamento de consulta inteligente](../../relational-databases/performance/intelligent-query-processing.md).

> [!NOTE]
> Para o nível de compatibilidade do banco de dados 140 ou menor, esta configuração com escopo de banco de dados não tem nenhum efeito.

ELEVATE_ONLINE = { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED }

**APLICA-SE A**: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] (o recurso está na versão prévia pública)

Permite que você selecione as opções para fazer com que o mecanismo eleve automaticamente operações com suporte para online. O padrão é OFF, o que significa que as operações não serão elevadas para online, a menos que especificado na instrução. [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) reflete o valor atual de ELEVATE_ONLINE. Essas opções serão aplicadas somente a operações que têm suporte para online.

FAIL_UNSUPPORTED

Este valor eleva todas as operações DDL com suporte para ONLINE. Operações que não oferecem suporte à execução online falharão e gerarão um aviso.

WHEN_SUPPORTED

Este valor eleva operações que dão suporte a ONLINE. As operações sem suporte online serão executadas offline.

> [!NOTE]
> Você pode substituir a configuração padrão ao enviar uma instrução com a opção ONLINE especificada.

ELEVATE_RESUMABLE= { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED }

**APLICA-SE A**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando pelo [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (o recurso está em versão prévia pública)

Permite que você selecione as opções para fazer com que o mecanismo eleve automaticamente operações com suporte para retomáveis. O padrão é OFF, o que significa que as operações não serão elevadas para retomáveis, a menos que especificado na instrução. [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) reflete o valor atual de ELEVATE_RESUMABLE. Essas opções serão aplicadas somente a operações que têm suporte para retomável.

FAIL_UNSUPPORTED

Este valor eleva todas as operações DDL com suporte para RESUMABLE. Operações que não oferecem suporte à execução retomável falharão e gerarão um aviso.

WHEN_SUPPORTED

Este valor eleva operações que dão suporte a RESUMABLE. As operações que não dão suporte a retomáveis são executadas de modo não retomável.

> [!NOTE]
> Você pode substituir a configuração padrão ao enviar uma instrução com a opção RESUMABLE especificada.

OPTIMIZE_FOR_AD_HOC_WORKLOADS **=** { ON | **OFF** }

**APLICA-SE A**: [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]

Habilita ou desabilita um stub de plano compilado para ser armazenado em cache quando um lote é compilado pela primeira vez. O padrão é OFF. Quando a configuração no escopo do banco de dados OPTIMIZE_FOR_AD_HOC_WORKLOADS estiver habilitada para um banco de dados, um stub de plano compilado será armazenado em cache quando um lote for compilado pela primeira vez. Os stubs de plano têm um volume de memória menor em comparação com o tamanho do plano compilado completo. Se um lote for compilado ou executado novamente, o stub de plano compilado será removido e substituído por um plano compilado completo.

XTP_PROCEDURE_EXECUTION_STATISTICS **=** { ON | **OFF** }

**APLICA-SE A**: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]

Habilita ou desabilita a coleta de estatísticas de execução no nível do módulo para módulos T-SQL compilados nativamente no banco de dados atual. O padrão é OFF. As estatísticas de execução são refletidas em [sys.dm_exec_procedure_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md).

As estatísticas de execução de nível de módulo para módulos T-SQL compilados nativamente serão coletadas se esta opção estiver ATIVADA ou se a coleta de estatísticas for habilitada por meio de [sp_xtp_control_proc_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md).

XTP_QUERY_EXECUTION_STATISTICS **=** { ON | **OFF** }

**APLICA-SE A**: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]

Habilita ou desabilita a coleta de estatísticas de execução no nível de instrução para módulos T-SQL compilados nativamente no banco de dados atual. O padrão é OFF. As estatísticas de execução são refletidas em [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) e no [Repositório de Consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).

As estatísticas de execução de nível de instrução para módulos T-SQL compilados nativamente serão coletadas se esta opção estiver ATIVADA ou se a coleta de estatísticas for habilitada por meio de [sp_xtp_control_query_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md).

Para obter mais informações sobre monitoramento de desempenho de módulos [!INCLUDE[tsql](../../includes/tsql-md.md)] compilados nativamente, confira [Monitorando o desempenho de procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/monitoring-performance-of-natively-compiled-stored-procedures.md).

ROW_MODE_MEMORY_GRANT_FEEDBACK **=** { **ON** | OFF}

**APLICA-SE A**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando pelo [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (o recurso está em versão prévia pública)

Permite habilitar ou desabilitar Comentários de concessão de memória de modo de linha no escopo do banco de dados, mantendo o nível de compatibilidade do banco de dados como 150 e superior. Os comentários de concessão de memória são um recurso que faz parte do [Processamento de consulta inteligente](../../relational-databases/performance/intelligent-query-processing.md) introduzido no [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] (o modo de linha é compatível com [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]).

> [!NOTE]
> Para o nível de compatibilidade do banco de dados 140 ou menor, esta configuração com escopo de banco de dados não tem nenhum efeito.

BATCH_MODE_ON_ROWSTORE **=** { **ON** | OFF}

**APLICA-SE A**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando pelo [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (o recurso está em versão prévia pública)

Permite habilitar ou desabilitar o modo de lote em rowstore no escopo do banco de dados, mantendo o nível de compatibilidade do banco de dados como 150 e superior. O modo de lote em rowstore é um recurso que faz parte da família de recursos de [Processamento de consulta inteligente](../../relational-databases/performance/intelligent-query-processing.md).

> [!NOTE]
> Para o nível de compatibilidade do banco de dados 140 ou menor, esta configuração com escopo de banco de dados não tem nenhum efeito.

DEFERRED_COMPILATION_TV **=** { **ON** | OFF}

**APLICA-SE A**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando pelo [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (o recurso está em versão prévia pública)

Permite habilitar ou desabilitar a compilação adiada de variável de tabela no escopo do banco de dados, mantendo o nível de compatibilidade do banco de dados como 150 e superior. Compilação adiada de variável de tabela é um recurso que faz parte da família de recursos [Processamento de consulta inteligente](../../relational-databases/performance/intelligent-query-processing.md).

> [!NOTE]
> Para o nível de compatibilidade do banco de dados 140 ou menor, esta configuração com escopo de banco de dados não tem nenhum efeito.

ACCELERATED_PLAN_FORCING **=** { **ON** | OFF }

**Aplica-se ao**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)])

Habilita um mecanismo otimizado para a imposição de plano de consulta, aplicável a todas as formas de imposição de plano, tais como o [Plano de Imposição do Repositório de Consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#Regressed), o [Ajuste Automático](../../relational-databases/automatic-tuning/automatic-tuning.md#automatic-plan-correction) ou a dica de consulta [USE PLAN](../../t-sql/queries/hints-transact-sql-query.md#use-plan). O padrão é ON.

> [!NOTE]
> Não é recomendável desabilitar a imposição de plano acelerada.

GLOBAL_TEMPORARY_TABLE_AUTODROP **=** { **ON** | OFF }

**APLICA-SE A**: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] (o recurso está na versão prévia pública)

Permite configurar a funcionalidade de soltar automaticamente para [tabelas temporárias globais](../../t-sql/statements/create-table-transact-sql.md#temporary-tables). O padrão é ON, o que significa que as tabelas temporárias globais são descartadas automaticamente quando não estão em uso por qualquer sessão. Quando definido como OFF, as tabelas temporárias globais precisarão ser descartadas explicitamente usando uma instrução DROP TABLE, ou serão removidas automaticamente na reinicialização do servidor.

- Com bancos de dados únicos e pools elásticos do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], essa opção pode ser definida nos bancos de dados de usuários individuais do servidor do Banco de Dados SQL.
- Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e na instância gerenciada [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], essa opção é definida em `TempDB` e a configuração dos bancos de dados de usuário individuais não tem nenhum efeito.

<a name="lqp"></a>

LIGHTWEIGHT_QUERY_PROFILING **=** { **ON** | OFF}

**APLICA-SE A**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

Permite que você habilite ou desabilite a [infraestrutura de criação de perfil de consulta leve](../../relational-databases/performance/query-profiling-infrastructure.md). A LWP (infraestrutura de criação de perfil de consulta leve) fornece dados de desempenho de consulta de maneira mais eficiente do que os mecanismos de criação de perfil padrão e é habilitada por padrão.

<a name="verbose-truncation"></a>

VERBOSE_TRUNCATION_WARNINGS **=** { **ON** | OFF}

**APLICA-SE A**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

Permite habilitar ou desabilitar a nova mensagem de erro `String or binary data would be truncated`. O [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] apresenta uma mensagem de erro nova e mais específica (2628) para esse cenário:

`String or binary data would be truncated in table '%.*ls', column '%.*ls'. Truncated value: '%.*ls'.`

Quando essa opção é definida como ON no nível de compatibilidade do banco de dados 150, os erros de truncamento acionam a nova mensagem de erro 2628 para fornecer mais contexto e simplificar o processo de solução de problemas.

Quando essa opção é definida como OFF no nível de compatibilidade do banco de dados 150, os erros de truncamento acionam a mensagem de erro anterior 8152.

Para o nível de compatibilidade do banco de dados 140 ou inferior, a mensagem de erro 2628 permanece uma mensagem de erro de aceitação que exige a habilitação do [sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 460 e essa configuração no escopo do banco de dados não tem nenhum efeito.

LAST_QUERY_PLAN_STATS **=** { ON | **OFF**}

**APLICA-SE A**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (A partir do [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]) (o recurso está em versão prévia pública)

Permite habilitar ou desabilitar a coleta das últimas estatísticas de plano de consulta (equivalente a um plano de execução real) em [sys.dm_exec_query_plan_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md).

PAUSED_RESUMABLE_INDEX_ABORT_DURATION_MINUTES

**APLICA-SE A**: Banco de Dados SQL do Azure somente

A opção `PAUSED_RESUMABLE_INDEX_ABORT_DURATION_MINUTES` determina por quanto tempo (em minutos) o índice retomável ficará em pausa antes de ser anulado automaticamente pelo mecanismo.

- O valor padrão é definido como 1 dia (1.440 minutos)
- A duração mínima é definida como 1 minuto
- A duração máxima é de 71.582 minutos
- Quando definido como 0, uma operação em pausa nunca será anulada automaticamente

O valor atual da opção é exibido em [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md).

ISOLATE_SECURITY_POLICY_CARDINALITY **=** { ON | **OFF**}

**APLICA-SE A**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

Permite que você controle se um predicado da [RLS](../../relational-databases/security/row-level-security.md) (Segurança em Nível de Linha) é afetado pela cardinalidade do plano de execução da consulta geral do usuário. Quando ISOLATE_SECURITY_POLICY_CARDINALITY está ON, um predicado RLS não afeta a cardinalidade de um plano de execução. Por exemplo, considere uma tabela que contém 1 milhão linhas e um predicado RLS que restringe o resultado a 10 linhas para um usuário específico que emite a consulta. Com essa configuração com escopo de banco de dados definida como OFF, a estimativa de cardinalidade desse predicado será 10. Quando essa configuração com escopo do banco de dados estiver definida como ON, a otimização de consulta estimará 1 milhão linhas. É recomendável usar o valor padrão para a maioria das cargas de trabalho.

## <a name="Permissions"></a> Permissões

Requer `ALTER ANY DATABASE SCOPE CONFIGURATION` no banco de dados. Essa permissão pode ser concedida por um usuário com a permissão CONTROL em um banco de dados.

## <a name="general-remarks"></a>Comentários gerais

Embora seja possível configurar bancos de dados secundários para com definições de configuração de escopo diferentes do primário, todos os bancos de dados secundários usam a mesma configuração. As configurações diferentes não podem ser configuradas para secundários individuais.

Executar essa instrução limpa o cache de procedimento no banco de dados atual, que significa que todas as consultas precisarão ser recompiladas.

Para consultas de nome de três partes, as configurações da conexão de banco de dados atual da consulta são cumpridas, já para os módulos SQL (como procedimentos, funções e gatilhos), que são compilados no contexto atual do banco de dados, são usadas as opções do banco de dados no qual eles residem.

O evento `ALTER_DATABASE_SCOPED_CONFIGURATION` é adicionado como um evento DDL que pode ser usado para acionar um gatilho DDL e é um filho do grupo do gatilho `ALTER_DATABASE_EVENTS`.

Definições de configuração no escopo do banco de dados serão transferidas para o banco de dados, o que significa que, quando um determinado banco de dados é restaurado ou anexado, as definições de configuração existentes permanecem.

Começando com [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e em [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], alguns nomes de opções foram alterados:      
-  `DISABLE_INTERLEAVED_EXECUTION_TVF` foi alterado para `INTERLEAVED_EXECUTION_TVF`
-  `DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK` foi alterado para `BATCH_MODE_MEMORY_GRANT_FEEDBACK`
-  `DISABLE_BATCH_MODE_ADAPTIVE_JOINS` foi alterado para `BATCH_MODE_ADAPTIVE_JOINS`

## <a name="limitations-and-restrictions"></a>Limitações e Restrições

### <a name="maxdop"></a>MAXDOP

As configurações granulares podem substituir as globais e o Resource Governor pode limitar a todas as outras configurações de MAXDOP. A lógica para a configuração de MAXDOP é a seguinte:

- A dica de consulta substitui tanto `sp_configure` quanto a configuração no escopo do banco de dados. Se o grupo de recursos MAXDOP estiver definido para o grupo de carga de trabalho:

  - Se a dica de consulta for definida como zero (0), ela será substituída pela configuração do Resource Governor.

  - Se a dica de consulta não for zero (0), ela será limitada pela configuração do Resource Governor.

- A configuração no escopo do banco de dados (a menos que seja zero) substitui a configuração `sp_configure`, a menos que haja uma dica de consulta e seja limitada pela configuração do Resource Governor.

- A configuração de `sp_configure` substituída pela configuração do Resource Governor.

### <a name="query_optimizer_hotfixes"></a>QUERY_OPTIMIZER_HOTFIXES

Quando a dica `QUERYTRACEON` é usada para habilitar o otimizador de consulta padrão do SQL Server 7.0 por meio de versões do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou hotfixes do otimizador de consulta, ela é uma condição OR entre a dica de consulta e a definição de configuração de banco de dados com escopo, o que significa que se qualquer uma for habilitada, ambas as configurações de banco de dados com escopo se aplicarão.

### <a name="geo-dr"></a>DR de área geográfica

Bancos de dados secundários legíveis (Grupos de Disponibilidade Always On e bancos de dados com replicação geográfica do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]) usam o valor secundário verificando o estado do banco de dados. Embora a recompilação não ocorra no failover e tecnicamente o novo primário tenha consultas que usam as configurações do secundário, a ideia é que a configuração entre o primário e o secundário apenas varie quando a carga de trabalho for diferente e, portanto, as consultas armazenadas em cache estiverem usando as configurações ideais, enquanto as novas consultas estarão selecionando as novas configurações apropriadas para elas.

### <a name="dacfx"></a>DacFx

Uma vez que `ALTER DATABASE SCOPED CONFIGURATION` é um novo recurso no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando pelo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) que afeta o esquema de banco de dados, exportações do esquema (com ou sem dados) não podem ser importadas para uma versão mais antiga do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. Por exemplo, uma exportação para um [DACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_3) ou um [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) de um [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ou de um banco de dados do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] que tiver usado esse novo recurso não poderá ser importada em um servidor de nível inferior.

### <a name="elevate_online"></a>ELEVATE_ONLINE

Essa opção é aplicável somente a instruções DDL com suporte a `WITH (ONLINE = <syntax>)`. Índices XML não são afetados.

### <a name="elevate_resumable"></a>ELEVATE_RESUMABLE

Essa opção é aplicável somente a instruções DDL com suporte a `WITH (RESUMABLE = <syntax>)`. Índices XML não são afetados.

## <a name="metadata"></a>Metadados

O Modo de Exibição do Sistema [sys.database_scoped_configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) fornece informações sobre as configurações no escopo em um banco de dados. As opções de configuração no escopo do banco de dados só aparecem em sys.database_scoped_configurations porque elas são substituições das configurações padrão de todo o servidor. O Modo de Exibição do Sistema [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) mostra apenas as configurações de todo o servidor.

## <a name="examples"></a>Exemplos

Esses exemplos demonstram o uso de ALTER DATABASE SCOPED CONFIGURATION

### <a name="a-grant-permission"></a>a. Conceder permissão

Este exemplo concede a permissão necessária para executar ALTER DATABASE SCOPED CONFIGURATION ao usuário José.

```sql
GRANT ALTER ANY DATABASE SCOPED CONFIGURATION to [Joe] ;
```

### <a name="b-set-maxdop"></a>B. Definir MAXDOP

Este exemplo define MAXDOP = 1 para um banco de dados primário e MAXDOP = 4 para um banco de dados secundário em um cenário de replicação geográfica.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET MAXDOP = 1 ;
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP = 4 ;
```

Este exemplo define MAXDOP para um banco de dados secundário como o mesmo que está definido para seu banco de dados primário em um cenário de replicação geográfica.

```sql
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP = PRIMARY ;
```

### <a name="c-set-legacy_cardinality_estimation"></a>C. Definir LEGACY_CARDINALITY_ESTIMATION

Este exemplo define LEGACY_CARDINALITY_ESTIMATION como ON para um banco de dados secundário em um cenário de replicação geográfica.

```sql
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION = ON ;
```

Este exemplo define LEGACY_CARDINALITY_ESTIMATION para um banco de dados secundário como o mesmo que está definido para seu banco de dados primário em um cenário de replicação geográfica.

```sql
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION = PRIMARY ;
```

### <a name="d-set-parameter_sniffing"></a>D. Definir PARAMETER_SNIFFING

Este exemplo define PARAMETER_SNIFFING como OFF para um banco de dados primário em um cenário de replicação geográfica.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET PARAMETER_SNIFFING = OFF ;
```

Este exemplo define PARAMETER_SNIFFING como OFF para um banco de dados secundário em um cenário de replicação geográfica.

```sql
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING = OFF ;
```

Este exemplo define PARAMETER_SNIFFING para um banco de dados secundário como o mesmo que está definido em seu banco de dados primário em um cenário de replicação geográfica.

```sql
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING = PRIMARY ;
```

### <a name="e-set-query_optimizer_hotfixes"></a>E. Definir QUERY_OPTIMIZER_HOTFIXES

Defina QUERY_OPTIMIZER_HOTFIXES como ON para um banco de dados primário em um cenário de replicação geográfica.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET QUERY_OPTIMIZER_HOTFIXES = ON ;
```

### <a name="f-clear-procedure-cache"></a>F. Limpar o cache de procedimento

Este exemplo limpa o cache de procedimento (é possível somente para um banco de dados primário).

```sql
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
```

### <a name="g-set-identity_cache"></a>G. Definir IDENTITY_CACHE

**APLICA-SE A**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando pelo [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (o recurso está em versão prévia pública)

Este exemplo desabilita o cache de identidade.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET IDENTITY_CACHE = OFF ;
```

### <a name="h-set-optimize_for_ad_hoc_workloads"></a>H. Definir OPTIMIZE_FOR_AD_HOC_WORKLOADS

**APLICA-SE A**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

Este exemplo habilita um stub de plano compilado para ser armazenado em cache quando um lote é compilado pela primeira vez.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET OPTIMIZE_FOR_AD_HOC_WORKLOADS = ON;
```

### <a name="i-set-elevate_online"></a>I. Definir ELEVATE_ONLINE

**APLICA-SE A**: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] (o recurso está na versão prévia pública)

Este exemplo define ELEVATE_ONLINE como FAIL_UNSUPPORTED.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ELEVATE_ONLINE = FAIL_UNSUPPORTED ;
```

### <a name="j-set-elevate_resumable"></a>J. Definir ELEVATE_RESUMABLE

**APLICA-SE A**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e [!INCLUDE[ssNoVersion](../../includes/sssqlv15-md.md)] (o recurso está na versão prévia pública)

Este exemplo define ELEVATE_RESUMABLE como WHEN_SUPPORTED.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ELEVATE_RESUMABLE = WHEN_SUPPORTED ;
```

### <a name="k-clear-a-query-plan-from-the-plan-cache"></a>K. Apagar um plano de consulta do cache do plano

**APLICA-SE A**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

Este exemplo limpa um plano específico do cache de procedimento

```sql
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE 0x06000500F443610F003B7CD12C02000001000000000000000000000000000000000000000000000000000000;
```

### <a name="l-set-paused-duration"></a>L. Definir duração da pausa

**APLICA-SE A**: Banco de Dados SQL do Azure somente

Este exemplo define a duração da pausa do índice retomável como 60 minutos.

```sql
ALTER DATABASE SCOPED CONFIGURATION
SET PAUSED_RESUMABLE_INDEX_ABORT_DURATION_MINUTES = 60
```

## <a name="additional-resources"></a>Recursos adicionais

### <a name="maxdop-resources"></a>Recursos de MAXDOP

- [Grau de paralelismo](../../relational-databases/query-processing-architecture-guide.md#DOP)
- [Recomendações e diretrizes para a opção de configuração “max degree of parallelism” no SQL Server](https://support.microsoft.com/kb/2806535)

### <a name="legacy_cardinality_estimation-resources"></a>Recursos de LEGACY_CARDINALITY_ESTIMATION

- [Estimativa de cardinalidade (SQL Server)](../../relational-databases/performance/cardinality-estimation-sql-server.md)
- [Otimizar os planos de consulta com o avaliador de cardinalidade do SQL Server 2014](https://msdn.microsoft.com/library/dn673537.aspx)

### <a name="parameter_sniffing-resources"></a>Recursos de PARAMETER_SNIFFING

- [Detecção de parâmetros](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)
- ["I smell a parameter!"](https://blogs.msdn.microsoft.com/queryoptteam/2006/03/31/i-smell-a-parameter/) (Sinto cheiro de parâmetro!)

### <a name="query_optimizer_hotfixes-resources"></a>Recursos de QUERY_OPTIMIZER_HOTFIXES

- [Sinalizadores de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
- [Modelo de serviço do sinalizador de rastreamento 4199 de hotfix do otimizador de consulta do SQL Server](https://support.microsoft.com/kb/974006)

### <a name="elevate_online-resources"></a>Recursos ELEVATE_ONLINE

[Diretrizes para operações de índice online](../../relational-databases/indexes/guidelines-for-online-index-operations.md)

### <a name="elevate_resumable-resources"></a>Recursos ELEVATE_RESUMABLE

[Diretrizes para operações de índice online](../../relational-databases/indexes/guidelines-for-online-index-operations.md)

## <a name="more-information"></a>Mais informações   
 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)      
 [Recomendações e diretrizes para a opção de configuração "grau máximo de paralelismo" do SQL Server](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)      
 [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)    
 [Exibições de catálogo de bancos de dados e de arquivos](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)    
 [Opções de configuração de servidor](../../database-engine/configure-windows/server-configuration-options-sql-server.md)    
 [Como funcionam as operações de índice online](../../relational-databases/indexes/how-online-index-operations-work.md)    
 [Executar operações de índice online](../../relational-databases/indexes/perform-index-operations-online.md)    
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)    
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)    
