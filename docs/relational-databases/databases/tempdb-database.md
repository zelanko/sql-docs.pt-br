---
title: Banco de dados tempdb | Microsoft Docs
description: Este tópico fornece detalhes sobre a configuração e o uso do banco de dados tempdb no SQL Server e no Banco de Dados SQL do Azure
ms.custom: P360
ms.date: 08/21/2019
ms.prod: sql
ms.prod_service: database-engine
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- temporary tables [SQL Server], tempdb database
- tempdb database [SQL Server], about tempdb
- temporary stored procedures [SQL Server]
- tempdb database [SQL Server]
ms.assetid: ce4053fb-e37a-4851-b711-8e504059a780
author: stevestein
ms.author: sstein
ms.reviewer: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 46807e551052ca6da38fde744d9a1e9dd7c794b0
ms.sourcegitcommit: ba44730f5cc33295ae2ed1f281186dd266bad4ef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2019
ms.locfileid: "74190148"
---
# <a name="tempdb-database"></a>Banco de dados TempDB

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

O banco de dados do sistema **TempDB** é um recurso global disponível para todos os usuários conectados à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou ao Banco de Dados SQL. O Tempdb é usado para manter:  
  
- **Objetos de usuário** temporários criados explicitamente como: índices e tabelas temporárias globais ou locais, procedimentos armazenados temporários, variáveis de tabela, Tabelas retornadas em funções com valor de tabela ou cursores.  
- **Objetos internos** criados pelo mecanismo de banco de dados. Eles incluem:
  - Tabelas de trabalho para armazenar resultados intermediários para spools, cursores, classificações e armazenamento temporário LOB (objeto grande).
  - Arquivos de trabalho para operações de junção de hash ou de agregação de hash.
  - Resultados intermediários de classificação para operações como criar ou recriar índices (se SORT_IN_TEMPDB for especificado) ou determinadas consultas GROUP BY, ORDER BY ou UNION.

  > [!NOTE]
  > Cada objeto interno usa um mínimo de nove páginas: uma página de IAM e uma extensão de oito páginas. Para obter mais informações sobre páginas e extensões, consulte [Páginas e extensões](../../relational-databases/pages-and-extents-architecture-guide.md#pages-and-extents).
  > [!IMPORTANT]
  > Os bancos de dados individuais e pools elásticos do Banco de Dados SQL do Azure dão suporte a tabelas temporárias globais e a procedimentos armazenados temporários globais armazenados no TempDB e que estão no escopo do nível do banco de dados. As tabelas temporárias globais e os procedimentos armazenados temporários globais são compartilhados entre todas as sessões de usuários no mesmo Banco de Dados SQL do Azure. As sessões de usuário de outros bancos de dados SQL do Azure não podem acessar tabelas temporárias globais. Para obter mais informações, consulte [Tabelas temporárias globais no escopo do banco de dados (Banco de Dados SQL do Azure)](../../t-sql/statements/create-table-transact-sql.md#database-scoped-global-temporary-tables-azure-sql-database). A [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) oferece suporte aos mesmos objetos temporários que o SQL Server.
  > Para os bancos de dados individuais e pools elásticos do Banco de Dados SQL do Azure, apenas o banco de dados mestre e o banco de dados TempDB se aplicam. Para saber mais, confira [O que é um servidor do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-servers-databases#what-is-an-azure-sql-database-server). Para obter uma discussão sobre o TempDB no contexto de bancos de dados individuais e pools elásticos do Banco de Dados SQL do Azure, confira [Banco de dados TempDB nos bancos de dados individuais e pools elásticos do Banco de Dados SQL do Azure](#tempdb-database-in-sql-database). Para a Instância Gerenciada do Banco de Dados SQL do Azure, Todos os bancos de dados do sistema se aplicam.

- **Repositórios de versão**, que são uma coleção de páginas de dados que contém linhas de dados necessárias para dar suporte aos recursos que usam o controle de versão de linha. Existem dois armazenamentos de versão: um repositório de versão comum e um armazenamento de versão de criação de índice online. Os armazenamentos de versão contêm:
  - Versões de linha geradas por transações de modificação de dados em um banco de dados que usa a leitura de confirmados usando transações de isolação de controle de versão de linha ou isolação de instantâneo.  
  - As versões de linhas geradas por meio de transações de modificação de dados para recursos como: operações de índice on-line, vários conjuntos de resultados ativos (MARS) e gatilhos AFTER.  
  
As operações no **TempDB** são registradas minimamente em log para que as transações possam ser revertidas. **TempDB** é recriado a cada vez que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado, de modo que o sistema sempre começa com uma cópia limpa do banco de dados. As tabelas temporárias e procedimentos armazenados são descartados automaticamente ou desconectados e nenhuma conexão fica ativa quando o sistema é desligado. Portanto, nunca há nada em **TempDB** a ser gravado de uma sessão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para outra. As operações de backup e restauração não são permitidas em **TempDB**.  

## <a name="physical-properties-of-tempdb-in-sql-server"></a>Propriedades físicas do TempDB no SQL Server

A tabela a seguir lista os valores de configuração iniciais dos arquivos de dados e de log do **TempDB** no SQL Server, que se baseiam nos padrões do Modelo de banco de dados. Os tamanhos desses arquivos podem variar um pouco em diferentes edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Arquivo|Nome lógico|Nome físico|Tamanho inicial|Aumento do arquivo|  
|----------|------------------|-------------------|------------------|-----------------|  
|Dados primários|tempdev|tempdb.mdf|8 megabytes|Aumento automático de 64 MB até que o disco fique cheio|  
|Arquivos de dados secundários*|temp#|tempdb_mssql_#.ndf|8 megabytes|Aumento automático de 64 MB até que o disco fique cheio|  
|Log|templog|templog.ldf|8 megabytes|Aumento automático de 64 megabytes até um máximo de 2 terabytes|  
  
\* O número de arquivos depende do número de processadores (lógicos) do computador. Como regra geral, se o número de processadores lógicos for menor ou igual a oito, use o mesmo número de processadores lógicos para os arquivos de dados. Se o número de processadores lógicos for maior que oito, use oito arquivos de dados e, se a contenção persistir, aumente o número de arquivos de dados em múltiplos de quatro até que a contenção seja reduzida a níveis aceitáveis ou faça alterações no código/carga de trabalho.

> [!NOTE]
> O valor padrão para o número de arquivos de dados baseia-se nas diretrizes gerais de [KB 2154845](https://support.microsoft.com/kb/2154845/).  
  
### <a name="moving-the-tempdb-data-and-log-files-in-sql-server"></a>Mover os arquivos de log e de dados de TempDB no SQL Server

Para mover os arquivos de log e de dados de **TempDB**, confira [Mover bancos de dados do sistema](../../relational-databases/databases/move-system-databases.md).  
  
### <a name="database-options-for-tempdb-in-sql-server"></a>Opções de banco de dados para TempDB no SQL Server

A tabela a seguir lista o valor padrão de cada opção do banco de dados **TempDB** e se a opção pode ser modificada. Para exibir as configurações atuais dessas opções, use a exibição de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) .  
  
|Opção de banco de dados|Valor padrão|Pode ser modificado|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|Sim|  
|ANSI_NULL_DEFAULT|OFF|Sim|  
|ANSI_NULLS|OFF|Sim|  
|ANSI_PADDING|OFF|Sim|  
|ANSI_WARNINGS|OFF|Sim|  
|ARITHABORT|OFF|Sim|  
|AUTO_CLOSE|OFF|Não|  
|AUTO_CREATE_STATISTICS|ATIVADO|Sim|  
|AUTO_SHRINK|OFF|Não|  
|AUTO_UPDATE_STATISTICS|ATIVADO|Sim|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|Sim|  
|CHANGE_TRACKING|OFF|Não|  
|CONCAT_NULL_YIELDS_NULL|OFF|Sim|  
|CURSOR_CLOSE_ON_COMMIT|OFF|Sim|  
|CURSOR_DEFAULT|GLOBAL|Sim|  
|Opções de disponibilidade de banco de dados|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|Não<br /><br /> Não<br /><br /> Não|  
|DATE_CORRELATION_OPTIMIZATION|OFF|Sim|  
|DB_CHAINING|ATIVADO|Não|  
|ENCRYPTION|OFF|Não|  
|MIXED_PAGE_ALLOCATION|OFF|Não|  
|NUMERIC_ROUNDABORT|OFF|Sim|  
|PAGE_VERIFY|CHECKSUM para novas instalações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> NONE para atualizações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Sim|  
|PARAMETERIZATION|SIMPLES|Sim|  
|QUOTED_IDENTIFIER|OFF|Sim|  
|READ_COMMITTED_SNAPSHOT|OFF|Não|  
|RECOVERY|SIMPLES|Não|  
|RECURSIVE_TRIGGERS|OFF|Sim|  
|Opções do Service Broker|ENABLE_BROKER|Sim|  
|TRUSTWORTHY|OFF|Não|  
  
Para obter uma descrição dessas opções de banco de dados, consulte [Opções ALTER DATABASE SET (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
## <a name="tempdb-database-in-sql-database"></a>Banco de dados TempDB no Banco de Dados SQL

### <a name="tempdb-sizes-for-dtu-based-service-tiers"></a>Tamanhos de TempDB para as camadas de serviço baseadas em DTU

|SLO|Tamanho máximo do arquivo de dados TempDB (GBs)|Nº de arquivos de dados do TempDB|Tamanho máximo de dados do TempDB (GB)|
|---|---:|---:|---:|
|Basic|13|1|13|
|S0|13|1|13|
|S1|13|1|13|
|S2|13|1|13|
|S3|32|1|32
|S4|32|2|64|
|S6|32|3|96|
|S7|32|6|192|
|S9|32|12|384|
|S12|32|12|384|
|P1|13|12|156|
|P2|13|12|156|
|P4|13|12|156|
|P6|13|12|156|
|P11|13|12|156|
|P15|13|12|156|
|Pools Elásticos Premium (todas as configurações de DTU)|13|12|156|
|Pools Elásticos Padrão (S0-S2)|13|12|156|
|Pools Elásticos Padrão (S3 e superiores) |32|12|384|
|Pools Elásticos Básicos (todas as configurações de DTU)|13|12|156|
||||

### <a name="tempdb-sizes-for-vcore-based-service-tiers"></a>Tamanhos de TempDB para as camadas de serviço baseadas em vCore

Consulte [Limites de recursos baseados em vCore](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits)

## <a name="restrictions"></a>Restrições

As seguintes operações não podem ser executadas no banco de dados **TempDB**:  
  
- Adição de grupos de arquivos
- Backup ou restauração de banco de dados
- Alteração de ordenação. A ordenação padrão é a do servidor
- Alteração do proprietário do banco de dados. **TempDB** pertence a **sa**
- Criando um instantâneo do banco de dados
- Descartando o banco de dados
- Descartar o usuário **convidado** do banco de dados
- Habilitação da captura de dados de alterações
- Participação no espelhamento de banco de dados
- Remoção do grupo de arquivos primário, arquivo de dados primário ou arquivo de log
- Renomeação do banco de dados ou grupo de arquivos primário
- Execução de DBCC CHECKALLOC
- Execução de DBCC CHECKCATALOG
- Definição do banco de dados como OFFLINE
- Definição do banco de dados ou grupo de arquivos primário como READ_ONLY
  
## <a name="permissions"></a>Permissões

Qualquer usuário pode criar objetos temporários no TempDB. Os usuários podem acessar somente seus próprios objetos, a menos que recebam permissões adicionais. É possível revogar a permissão de conexão ao TempDB para impedir um usuário de usar o TempDB, mas isso não é recomendado porque algumas operações de rotina exigem o uso do TempDB.  

## <a name="optimizing-tempdb-performance-in-sql-server"></a>Otimizar o desempenho do TempDB no SQL Server
O tamanho e o posicionamento físico do banco de dados TempDB podem afetar o desempenho de um sistema. Por exemplo, se o tamanho definido para TempDB for muito pequeno, parte da carga de processamento do sistema poderá ser elevada com o crescimento automático de TempDB para o tamanho necessário para dar suporte à carga de trabalho toda vez que você reiniciar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Se possível, use a [inicialização instantânea de arquivo do banco de dados](../../relational-databases/databases/database-instant-file-initialization.md) para melhorar o desempenho das operações de crescimento de arquivo de dados.

Aloque espaço antecipadamente para todos os arquivos do TempDB definindo o tamanho de arquivo com um valor grande o bastante para acomodar a carga de trabalho comum no ambiente. A pré-alocação impede que o TempDB seja expandido com muita frequência, o que afeta o desempenho. O banco de dados TempDB deve ser definido para crescimento automático, mas isso deve ser usado a fim de aumentar o espaço em disco para exceções não planejadas.

Os arquivos de dados devem ser de tamanho igual em cada [grupo de arquivos](../../relational-databases/databases/database-files-and-filegroups.md#filegroups), pois o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa um algoritmo de preenchimento proporcional que favorece alocações em arquivos com mais espaço livre. A divisão do TempDB em vários arquivos de dados de tamanho igual fornece um alto grau de eficiência paralela em operações que usam o TempDB.

Defina o incremento de crescimento do arquivo com um tamanho razoável para evitar que os arquivos do banco de dados TempDB cresçam com um valor muito pequeno. Se o aumento do arquivo for muito pequeno comparado à quantidade de dados que está sendo gravada no TempDB, talvez o TempDB precise se expandir constantemente e afetar o desempenho.

Para verificar o tamanho atual do TempDB e os parâmetros de crescimento, use a seguinte consulta:

```sql
 SELECT name AS FileName,
    size*1.0/128 AS FileSizeInMB,
    CASE max_size
        WHEN 0 THEN 'Autogrowth is off.'
        WHEN -1 THEN 'Autogrowth is on.'
        ELSE 'Log file grows to a maximum size of 2 TB.'
    END,
    growth AS 'GrowthValue',
    'GrowthIncrement' =
        CASE
            WHEN growth = 0 THEN 'Size is fixed.'
            WHEN growth > 0 AND is_percent_growth = 0
                THEN 'Growth value is in 8-KB pages.'
            ELSE 'Growth value is a percentage.'
        END
FROM tempdb.sys.database_files;
GO
```

Coloque o banco de dados TempDB em um subsistema de E/S rápido. Use a distribuição de disco se houver muitos discos anexados diretamente. Arquivos de dados individuais ou grupos de arquivos de dados do TempDB não precisam necessariamente estar em discos ou eixos diferentes, a menos que você também esteja com gargalos de E/S.

Coloque o banco de dados TempDB em discos diferentes dos usados por bancos de dados de usuários.

## <a name="performance-improvements-in-tempdb-for-sql-server"></a>Melhorias de desempenho no TempDB para o SQL Server
A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], o desempenho do **TempDB** é ainda mais otimizado das seguintes maneiras:  
  
- As tabelas temporárias e variáveis de tabela são armazenadas em cache. O armazenamento em cache permite que as operações de descarte e criação de objetos temporários sejam executadas rapidamente e reduz a contenção de alocação de página.  
- O protocolo de travamento da página de alocação foi aprimorado para reduzir o número de travas (atualização) de UP utilizadas.  
- A sobrecarga de log para o **TempDB** foi reduzida para diminuir o consumo de largura de banda de E/S de disco no arquivo de log do **TempDB**.  
- A Instalação adiciona vários arquivos de dados TempDB durante uma nova instalação da instância. Essa tarefa pode ser realizada com o novo controle de entrada da interface do usuário na seção **Configuração do Mecanismo de Banco de Dados** e em um parâmetro de linha de comando `/SQLTEMPDBFILECOUNT`. Por padrão, a instalação adiciona um número de arquivos de dados do TempDB equivalente à contagem de processadores lógicos ou a oito, o que for menor.  
- Quando houver vários arquivos de dados do **TempDB**, todos os arquivos aumentarão automaticamente ao mesmo tempo e na mesma quantidade, dependendo das configurações de aumento. O [sinalizador de rastreamento 1117](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) não é mais necessário.  
- Além disso, todas as alocações em **TempDB** usam extensões uniformes. O [sinalizador de rastreamento 1118](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) não é mais necessário.  
- Para o grupo de arquivos primário, a propriedade AUTOGROW_ALL_FILES está ativada e não pode ser modificada.

Para obter mais informações sobre as melhorias no desempenho em TempDB, confira o artigo de blog a seguir:

[TEMPDB – Files and Trace Flags and Updates, Oh My!](https://blogs.msdn.microsoft.com/sql_server_team/tempdb-files-and-trace-flags-and-updates-oh-my/) (TEMPDB – arquivos, sinalizadores de rastreamento e atualizações, uau!)

## <a name="memory-optimized-tempdb-metadata"></a>Metadados do TempDB com otimização de memória
Historicamente, a contenção de metadados do TempDB tem sido um gargalo para a escalabilidade em muitas cargas de trabalho em execução no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] apresenta um novo recurso que faz parte da família de recursos do [Banco de dados em memória](../in-memory-database.md), os metadados do TempDB com otimização de memória, que efetivamente remove esse gargalo e possibilita um novo nível de escalabilidade para cargas de trabalho com uso intenso do TempDB. No [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], as tabelas do sistema envolvidas no gerenciamento dos metadados da tabela temporária podem ser movidas para tabelas com otimização de memória não duráveis e livres de travas.

Assista a este vídeo de sete minutos para obter uma visão geral de como e quando usar os metadados TempDB otimizados para memória:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/How-and-When-To-Memory-Optimized-TempDB-Metadata/player?WT.mc_id=dataexposed-c9-niner]


Para aceitar esse novo recurso, use o seguinte script:

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED TEMPDB_METADATA = ON 
```

Essa alteração de configuração exige uma reinicialização do serviço para entrar em vigor.

Existem algumas limitações nessa implementação que são importantes a serem observadas:

1. A ativação/desativação do recurso não é dinâmica. Devido às alterações intrínsecas que precisam ser feitas na estrutura do TempDB, uma reinicialização é necessária para habilitar ou desabilitar o recurso.

2. Uma única transação pode não acessar tabelas com otimização de memória em mais de um banco de dados.  Isso significa que todas as transações que envolvem uma tabela com otimização de memória em um banco de dados de usuário não poderão acessar as exibições do sistema do TempDB na mesma transação.  Se você tentar acessar as exibições do sistema do TempDB na mesma transação como uma tabela com otimização de memória em um banco de dados de usuário, você receberá o seguinte erro:
    
    ```
    A user transaction that accesses memory optimized tables or natively compiled modules cannot access more than one user database or databases model and msdb, and it cannot write to master.
    ```
    
    Exemplo:
    
    ```sql
    BEGIN TRAN
    SELECT *
    FROM tempdb.sys.tables  -----> Creates a user In-Memory OLTP Transaction on Tempdb
    INSERT INTO <user database>.<schema>.<mem-optimized table>
    VALUES (1)  ----> Attempts to create user In-Memory OLTP transaction but will fail
    COMMIT TRAN
    ```
    
3. As consultas nas tabelas com otimização de memória não dão suporte a dicas de bloqueio e isolamento; portanto, as consultas nas exibições de catálogo do TempDB com otimização de memória não respeitarão as dicas de bloqueio e isolamento. Como ocorre com outras exibições de catálogo do sistema no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], todas as transações nas exibições do sistema serão feitas no isolamento READ COMMITTED (ou, neste caso, READ COMMITTED SNAPSHOT).

4. Os [índices columnstore](../indexes/columnstore-indexes-overview.md) não poderão ser criados em tabelas temporárias quando os metadados do TempDB com otimização de memória forem habilitados.

5. Devido à limitação em índices columnstore, não há suporte para o uso do procedimento armazenado do sistema sp_estimate_data_compression_savings com o parâmetro de compactação de dados COLUMNSTORE ou COLUMNSTORE_ARCHIVE quando os metadados do TempDB com otimização de memória estão habilitados.

> [!NOTE] 
> Essas limitações se aplicam somente ao referenciar as exibições do sistema do TempDB; você poderá criar uma tabela temporária na mesma transação ao acessar uma tabela com otimização de memória em um banco de dados de usuário, se desejado.

Você pode verificar se o TempDB tem otimização de memória ou não usando o seguinte comando T-SQL:
```
SELECT SERVERPROPERTY('IsTempdbMetadataMemoryOptimized')
```

Se o servidor não conseguir iniciar por qualquer motivo depois de habilitar os metadados de TempDB com otimização de memória, você poderá ignorar o recurso iniciando o SQL Server com a [configuração mínima](../../database-engine/configure-windows/start-sql-server-with-minimal-configuration.md) usando a opção de inicialização **-f**. Isso permitirá que você desabilite o recurso e, em seguida, reinicie o SQL Server no modo normal.

## <a name="capacity-planning-for-tempdb-in-sql-server"></a>Planejamento de capacidade do TempDB no SQL Server
A determinação do tamanho apropriado para o TempDB em um ambiente de produção [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] depende de muitos fatores. Conforme descrito anteriormente neste artigo, esses fatores incluem a carga de trabalho existente e os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizados. Recomendamos que você analise a carga de trabalho existente executando as seguintes tarefas em um ambiente de teste do SQL Server:

- Defina o crescimento automático como ativado para o TempDB.
- Execute consultas individuais ou arquivos de rastreamento de carga de trabalho e monitore o uso de espaço do TempDB.
- Execute operações de manutenção de índice, como recriação de índices, e monitore o espaço do TempDB.
- Use os valores de uso de espaço das etapas anteriores para prever o uso total da carga de trabalho; ajuste esse valor para atividades simultâneas projetadas e, em seguida, defina o tamanho do TempDB de acordo com isso.

## <a name="how-to-monitor-tempdb-use"></a>Como monitorar o uso do TempDB
O espaço em disco insuficiente no TempDB pode causar interrupções significativas no ambiente de produção do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e impedir que aplicativos que estão em execução concluam as operações. Use a exibição de gerenciamento dinâmico [sys.dm_db_file_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) para monitorar o espaço em disco utilizado nos arquivos do TempDB:

```sql
 -- Determining the Amount of Free Space in TempDB
SELECT SUM(unallocated_extent_page_count) AS [free pages],
  (SUM(unallocated_extent_page_count)*1.0/128) AS [free space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the Amount Space Used by the Version Store
SELECT SUM(version_store_reserved_page_count) AS [version store pages used],
  (SUM(version_store_reserved_page_count)*1.0/128) AS [version store space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the Amount of Space Used by Internal Objects
SELECT SUM(internal_object_reserved_page_count) AS [internal object pages used],
  (SUM(internal_object_reserved_page_count)*1.0/128) AS [internal object space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the Amount of Space Used by User Objects
SELECT SUM(user_object_reserved_page_count) AS [user object pages used],
  (SUM(user_object_reserved_page_count)*1.0/128) AS [user object space in MB]
FROM sys.dm_db_file_space_usage;
 ```

Além disso, para monitorar a atividade de alocação ou desalocação de página no TempDB em nível de sessão ou tarefa, use as exibições de gerenciamento dinâmico [sys.dm_db_session_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) e [sys.dm_db_task_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md). Essas exibições podem ser usadas para identificar consultas grandes, tabelas temporárias ou variáveis de tabela que estão utilizando muito espaço em disco do TempDB. Também existem vários contadores que podem ser usados para monitorar o espaço livre disponível no TempDB e também os recursos que estão usando o TempDB. Para obter mais informações, consulte a próxima seção.

```sql
-- Obtaining the space consumed by internal objects in all currently running tasks in each session
SELECT session_id,
  SUM(internal_objects_alloc_page_count) AS task_internal_objects_alloc_page_count,
  SUM(internal_objects_dealloc_page_count) AS task_internal_objects_dealloc_page_count
FROM sys.dm_db_task_space_usage
GROUP BY session_id;

-- Obtaining the space consumed by internal objects in the current session for both running and completed tasks
SELECT R2.session_id,
  R1.internal_objects_alloc_page_count
  + SUM(R2.internal_objects_alloc_page_count) AS session_internal_objects_alloc_page_count,
  R1.internal_objects_dealloc_page_count
  + SUM(R2.internal_objects_dealloc_page_count) AS session_internal_objects_dealloc_page_count
FROM sys.dm_db_session_space_usage AS R1
INNER JOIN sys.dm_db_task_space_usage AS R2 ON R1.session_id = R2.session_id
GROUP BY R2.session_id, R1.internal_objects_alloc_page_count,
  R1.internal_objects_dealloc_page_count;;
```

## <a name="related-content"></a>Conteúdo relacionado
[Opção SORT_IN_TEMPDB para índices](../../relational-databases/indexes/sort-in-TempDB-option-for-indexes.md)    
[Bancos de dados do sistema](../../relational-databases/databases/system-databases.md)    
[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)    
[sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)    
[Mover arquivos de banco de dados](../../relational-databases/databases/move-database-files.md)    
  
