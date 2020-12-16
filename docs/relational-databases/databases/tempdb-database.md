---
title: Banco de dados tempdb | Microsoft Docs
description: Este tópico fornece detalhes sobre a configuração e o uso do banco de dados tempdb no SQL Server e no Banco de Dados SQL do Azure.
ms.custom: P360
ms.date: 09/16/2020
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
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 345c02a175643967a509900ab415b90708a3d9e7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478297"
---
# <a name="tempdb-database"></a>banco de dados tempdb

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

O banco de dados do sistema `tempdb` é um recurso global disponível para todos os usuários conectados à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou ao Banco de Dados SQL do Azure. `tempdb` contém:  
  
- *Objetos de usuário* temporários que são explicitamente criados. Eles incluem tabelas e índices globais ou locais temporários, procedimentos armazenados temporários, variáveis de tabela, tabelas retornadas em funções com valor de tabela e cursores.  
- *Objetos internos* que o mecanismo de banco de dados cria. Entre elas estão:
  - Tabelas de trabalho para armazenar resultados intermediários para spools, cursores, classificações e armazenamento temporário LOB (objeto grande).
  - Arquivos de trabalho para operações de junção de hash ou de agregação de hash.
  - Resultados de classificação intermediários para operações como criação ou reconstrução de índices (se `SORT_IN_TEMPDB` for especificado) ou certas consultas `GROUP BY`, `ORDER BY` ou `UNION`.

  Cada objeto interno usa um mínimo de nove páginas: uma página de IAM e uma extensão de oito páginas. Para saber mais sobre páginas e extensões, confira [Páginas e extensões](../../relational-databases/pages-and-extents-architecture-guide.md#pages-and-extents).

  > [!IMPORTANT]
  > Os bancos de dados individuais e pools elásticos do Banco de Dados SQL do Azure dão suporte a tabelas temporárias globais e a procedimentos armazenados temporários globais armazenados no `tempdb` e que estão no escopo do nível do banco de dados. 
  >
  > As tabelas temporárias globais e os procedimentos armazenados temporários globais são compartilhados entre todas as sessões de usuários no mesmo banco de Dados SQL. As sessões de usuário de outros bancos de dados SQL não podem acessar tabelas temporárias globais. Para obter mais informações, consulte [Tabelas temporárias globais no escopo do banco de dados (Banco de Dados SQL do Azure)](../../t-sql/statements/create-table-transact-sql.md#database-scoped-global-temporary-tables-azure-sql-database). A [Instância Gerenciada de SQL do Azure](/azure/sql-database/sql-database-managed-instance) dá suporte aos mesmos objetos temporários do SQL Server.
  >
  > Para os bancos de dados individuais e pools elásticos do Banco de Dados SQL do Azure, apenas o banco de dados mestre e o banco de dados `tempdb` se aplicam. Para saber mais, confira [O que é um servidor do Banco de Dados SQL do Azure?](/azure/sql-database/sql-database-servers-databases#what-is-an-azure-sql-database-server). Para ver uma discussão sobre o `tempdb` no contexto de bancos de dados individuais e pools elásticos do Banco de Dados SQL do Azure, confira [Banco de dados tempdb em bancos de dados individuais e pools elásticos do Banco de Dados SQL do Azure](#tempdb-database-in-sql-database). 
  >
  > Para a Instância Gerenciada de SQL do Azure, todos os bancos de dados do sistema se aplicam.

- *Repositórios de versão*, que são coleções de páginas de dados que contêm as linhas de dados que dão suporte a recursos para controle de versão de linha. Existem dois tipos de repositório de versão: um comum e um de criação de índice online. Os armazenamentos de versão contêm:
  - Versões de linha geradas por transações de modificação de dados em um banco de dados que usa `READ COMMITTED` por meio transações de isolamento de instantâneo ou isolamento de controle de versão de linha.  
  - Versões de linhas geradas por meio de transações de modificação de dados para recursos, como operações de índice online, MARS (conjunto de resultados ativos múltiplos) e gatilhos `AFTER`.  
  
As operações no `tempdb` são registradas minimamente em log para que as transações possam ser revertidas. `tempdb` é recriado a cada vez que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado, de modo que o sistema sempre começa com uma cópia limpa do banco de dados. As tabelas temporárias e procedimentos armazenados são descartados automaticamente ou desconectados e nenhuma conexão fica ativa quando o sistema é desligado. 

Nunca há nada em `tempdb` a ser salvo de uma sessão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para outra. As operações de backup e restauração não são permitidas em `tempdb`.  

## <a name="physical-properties-of-tempdb-in-sql-server"></a>Propriedades físicas do tempdb no SQL Server

A tabela a seguir lista os valores de configuração inicial dos dados de `tempdb` e arquivos de log no SQL Server. Os valores são baseados nos padrões para o banco de dados `model`. Os tamanhos desses arquivos podem variar um pouco em diferentes edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Arquivo|Nome lógico|Nome físico|Tamanho inicial|Aumento do arquivo|  
|----------|------------------|-------------------|------------------|-----------------|  
|Dados primários|tempdev|tempdb.mdf|8 megabytes|Aumento automático de 64 MB até que o disco fique cheio|  
|Arquivos de dados secundários|temp#|tempdb_mssql_#.ndf|8 megabytes|Aumento automático de 64 MB até que o disco fique cheio|  
|Log|templog|templog.ldf|8 megabytes|Aumento automático de 64 megabytes até um máximo de 2 terabytes|  
  
O número de arquivos de dados secundários depende do número de processadores (lógicos) no computador. Como regra geral, se o número de processadores lógicos for menor ou igual a oito, use o mesmo número de processadores lógicos para os arquivos de dados. Se o número de processadores lógicos for maior que oito, use oito arquivos de dados. Se, após isso, a contenção continuar, aumente o número de arquivos de dados em múltiplos de quatro até que a contenção diminua para níveis aceitáveis ou faça alterações na carga de trabalho/no código.

> [!NOTE]
> O valor padrão para o número de arquivos de dados baseia-se nas diretrizes gerais de [KB 2154845](https://support.microsoft.com/kb/2154845/).  
  
### <a name="moving-the-tempdb-data-and-log-files-in-sql-server"></a>Movendo os arquivos de log e de dados do tempdb no SQL Server

Para mover os arquivos de log e dados de `tempdb`, confira [Mover bancos de dados do sistema](../../relational-databases/databases/move-system-databases.md).  
  
### <a name="database-options-for-tempdb-in-sql-server"></a>Opções de banco de dados para tempdb no SQL Server

A tabela a seguir lista o valor padrão de cada opção de banco de dados no banco de dados `tempdb` e se a opção pode ser modificada. Para exibir as configurações atuais dessas opções, use a exibição de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) .  
  
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
|PAGE_VERIFY|CHECKSUM para novas instalações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> NONE para atualizações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Sim|  
|PARAMETERIZATION|SIMPLES|Sim|  
|QUOTED_IDENTIFIER|OFF|Sim|  
|READ_COMMITTED_SNAPSHOT|OFF|Não|  
|RECOVERY|SIMPLES|Não|  
|RECURSIVE_TRIGGERS|OFF|Sim|  
|Opções do Service Broker|ENABLE_BROKER|Sim|  
|TRUSTWORTHY|OFF|Não|  
  
Para obter uma descrição dessas opções de banco de dados, consulte [Opções ALTER DATABASE SET (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
## <a name="tempdb-database-in-sql-database"></a>Banco de dados tempdb no Banco de Dados SQL

### <a name="tempdb-sizes-for-dtu-based-service-tiers"></a>Tamanhos de tempdb para as camadas de serviço baseadas em DTU

<!-- tempdb being larger for Basic and 50 eDTU pools than for 100-400 eDTU pools reflects actual config (historical reasons) --> 

|Objetivo no nível do serviço|Tamanho máximo do arquivo de dados de `tempdb` (GB)|Número de arquivos de dados de `tempdb`|Tamanho máximo dos dados de `tempdb` (GB)|
|---|---:|---:|---:|
|Basic|13,9|1|13,9|
|S0|13,9|1|13,9|
|S1|13,9|1|13,9|
|S2|13,9|1|13,9|
|S3|32|1|32
|S4|32|2|64|
|S6|32|3|96|
|S7|32|6|192|
|S9|32|12|384|
|S12|32|12|384|
|P1|13,9|12|166,7|
|P2|13,9|12|166,7|
|P4|13,9|12|166,7|
|P6|13,9|12|166,7|
|P11|13,9|12|166,7|
|P15|13,9|12|166,7|
|Pools Elásticos Básicos (todas as configurações de DTU)|13,9|12|166,7|
|Pools Elásticos Standard (50 eDTUs)|13,9|12|166,7|
|Pools Elásticos Standard (100 eDTUs)|32|1|32|
|Pools Elásticos Standard (200 eDTUs)|32|2|64|
|Pools Elásticos Standard (300 eDTUs)|32|3|96|
|Pools Elásticos Standard (400 eDTUs)|32|3|96|
|Pools Elásticos Standard (800 eDTUs)|32|6|192|
|Pools Elásticos Standard (1200 eDTUs)|32|10|320|
|Pools Elásticos Standard (1600 – 3000 eDTUs)|32|12|384|
|Pools Elásticos Premium (todas as configurações de DTU)|13,9|12|166,7|
||||

### <a name="tempdb-sizes-for-vcore-based-service-tiers"></a>Tamanhos de tempdb para as camadas de serviço baseadas em vCore

Confira [Limites de recursos baseados em vCore](/azure/sql-database/sql-database-vcore-resource-limits).

## <a name="restrictions"></a>Restrições

As seguintes operações não podem ser executadas no banco de dados `tempdb`:  
  
- Adição de grupos de arquivos
- Backup ou restauração de banco de dados.
- Alteração de ordenação. A ordenação padrão é a ordenação do servidor.
- Alteração do proprietário do banco de dados. `tempdb` pertence a *sa*.
- Criação de um instantâneo do banco de dados
- Descartando o banco de dados.
- Descartando o usuário *convidado* do banco de dados.
- Habilitação da captura de dados de alterações.
- Participação no espelhamento de banco de dados.
- Remoção do grupo de arquivos primário, arquivo de dados primário ou arquivo de log.
- Renomeação do banco de dados ou grupo de arquivos primário.
- Execução de `DBCC CHECKALLOC`.
- Execução de `DBCC CHECKCATALOG`.
- Definição do banco de dados para `OFFLINE`.
- Definição do banco de dados ou do grupo de arquivos primário para `READ_ONLY`.
  
## <a name="permissions"></a>Permissões

Qualquer usuário pode criar objetos temporários no `tempdb`. Os usuários podem acessar somente seus próprios objetos, a menos que recebam permissões adicionais. É possível revogar a permissão de conexão para `tempdb` a fim de impedir que um usuário use `tempdb`. Não recomendamos fazer isso porque algumas operações rotineiras exigem o uso de `tempdb`.  

## <a name="optimizing-tempdb-performance-in-sql-server"></a>Otimizando o desempenho do tempdb no SQL Server
O tamanho e o posicionamento físico do banco de dados `tempdb` podem afetar o desempenho de um sistema. Por exemplo, se o tamanho definido para `tempdb` for muito pequeno, parte da carga de processamento do sistema poderá ser elevada com o aumento automático de `tempdb` para o tamanho necessário, de modo a oferecer suporte à carga de trabalho toda vez que você reiniciar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Se possível, use a [inicialização instantânea de arquivo](../../relational-databases/databases/database-instant-file-initialization.md) para melhorar o desempenho das operações de aumento em arquivos de dados.

Aloque espaço antecipadamente para todos os arquivos do `tempdb` definindo o tamanho do arquivo com um valor grande o bastante para acomodar a carga de trabalho comum no ambiente. A pré-alocação impede que o `tempdb` seja expandido com muita frequência, o que afeta o desempenho. O banco de dados `tempdb` deve ser definido para aumento automático, a fim de ampliar o espaço em disco para exceções não planejadas.

Os arquivos de dados devem ser de tamanho igual em cada [grupo de arquivos](../../relational-databases/databases/database-files-and-filegroups.md#filegroups), pois o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa um algoritmo de preenchimento proporcional que favorece alocações em arquivos com mais espaço livre. A divisão do `tempdb` em vários arquivos de dados de tamanho igual fornece um alto grau de eficiência paralela em operações que usam o `tempdb`.

Defina o incremento do aumento de arquivo para um tamanho razoável a fim de evitar que os arquivos de banco de dados `tempdb` aumentem com um valor muito pequeno. Caso o aumento do arquivo seja muito pequeno em comparação à quantidade de dados que está sendo gravada no `tempdb`, o `tempdb` talvez tenha que se expandir constantemente. Isso afetará o desempenho.

Para verificar o tamanho atual e os parâmetros de aumento do `tempdb`, use a seguinte consulta:

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

Coloque o banco de dados `tempdb` em um subsistema de E/S rápido. Use a distribuição de disco se houver muitos discos anexados diretamente. Arquivos de dados individuais ou grupos de arquivos de dados do `tempdb` não precisam necessariamente estar em discos ou eixos diferentes, a menos que você também esteja com gargalos de E/S.

Coloque o banco de dados `tempdb` em discos diferentes dos usados pelos bancos de dados do usuário.

## <a name="performance-improvements-in-tempdb-for-sql-server"></a>Melhorias de desempenho no tempdb para o SQL Server
De [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] em diante, o desempenho do `tempdb` é ainda mais otimizado das seguintes maneiras:  
  
- As tabelas temporárias e variáveis de tabela são armazenadas em cache. O armazenamento em cache permite que as operações de descarte e criação de objetos temporários sejam executadas muito rapidamente. O armazenamento em cache também reduz a alocação de páginas e a contenção de metadados.  
- O protocolo de travamento da página de alocação foi aprimorado para reduzir o número de travas (atualização) de `UP` utilizadas.  
- A sobrecarga de log para o `tempdb` foi reduzida para diminuir o consumo de largura de banda de E/S de disco no arquivo de log do `tempdb`.  
- A Instalação adiciona vários arquivos de dados `tempdb` durante uma nova instalação da instância. É possível realizar essa tarefa usando o novo controle de entrada da IU na seção **Configuração do Mecanismo de Banco de Dados** e o parâmetro de linha de comando `/SQLTEMPDBFILECOUNT`. Por padrão, a instalação adiciona um número de arquivos de dados do `tempdb` equivalente à contagem de processadores lógicos ou a oito, o que for menor.  
- Quando houver vários arquivos de dados do `tempdb`, todos os arquivos aumentarão automaticamente ao mesmo tempo e na mesma quantidade, dependendo das configurações de aumento. O [sinalizador de rastreamento 1117](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) não é mais necessário.  
- Além disso, todas as alocações em `tempdb` usam extensões uniformes. O [sinalizador de rastreamento 1118](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) não é mais necessário.  
- No caso do grupo de arquivos primário, a propriedade `AUTOGROW_ALL_FILES` é ativada e não pode ser modificada.

Para saber mais sobre melhorias de desempenho em `tempdb`, confira o artigo do blog [TEMPDB – Arquivos, atualizações e sinalizadores de rastreamento. O que fazer?!](/archive/blogs/sql_server_team/tempdb-files-and-trace-flags-and-updates-oh-my).

## <a name="memory-optimized-tempdb-metadata"></a>Metadados do tempdb com otimização de memória
Historicamente, a contenção de metadados do `tempdb` tem sido um gargalo para a escalabilidade em muitas cargas de trabalho em execução no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] apresenta um novo recurso que faz parte da família de recursos do [banco de dados em memória](../in-memory-database.md): metadados de tempdb com otimização de memória. 

Esse recurso remove efetivamente esse gargalo e desbloqueia um novo nível de escalabilidade para cargas de trabalho pesadas de tempdb. No [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], as tabelas do sistema envolvidas no gerenciamento dos metadados da tabela temporária podem ser movidas para tabelas com otimização de memória não duráveis e livres de travas.

Assista a este vídeo de sete minutos para ter uma visão geral de como e quando usar os metadados tempdb com otimização de memória:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/How-and-When-To-Memory-Optimized-TempDB-Metadata/player?WT.mc_id=dataexposed-c9-niner]


### <a name="configuring-and-using-memory-optimized-tempdb-metadata"></a>Como configurar e usar metadados de tempdb com otimização de memória

Para aceitar esse novo recurso, use o seguinte script:

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED TEMPDB_METADATA = ON;
```

Essa alteração de configuração exige uma reinicialização do serviço para entrar em vigor.

Você pode verificar se o `tempdb` tem otimização de memória ou não usando o seguinte comando T-SQL:

```sql
SELECT SERVERPROPERTY('IsTempdbMetadataMemoryOptimized');
```

Se a inicialização do servidor falhar por qualquer motivo depois que você habilitar os metadados de `tempdb` com otimização de memória, você poderá ignorar o recurso iniciando a instância do SQL Server com [configuração mínima](../../database-engine/configure-windows/start-sql-server-with-minimal-configuration.md) por meio da opção de inicialização **-f**. Você pode desabilitar o recurso e reiniciar o SQL Server no modo normal.

Para proteger o servidor contra possíveis condições de memória insuficiente, você pode associar `tempdb` a um [pool de recursos](../in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md). Isso é feito por meio do comando [`ALTER SERVER`](../../t-sql/statements/alter-server-configuration-transact-sql.md), em vez das etapas que você normalmente seguiria para associar um pool de recursos a um banco de dados.

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED TEMPDB_METADATA = ON (RESOURCE_POOL = 'pool_name');
```

Essa alteração também requer uma reinicialização para entrar em vigor, mesmo que os metadados de tempdb com otimização de memória já estejam habilitados.

### <a name="memory-optimized-tempdb-limitations"></a>Limitações de tempdb com otimização de memória

- A ativação/desativação do recurso não é dinâmica. Devido às alterações intrínsecas que precisam ser feitas na estrutura do `tempdb`, uma reinicialização é necessária para habilitar ou desabilitar o recurso.

- Uma única transação não tem permissão para acessar tabelas com otimização de memória em mais de um banco de dados. Transações que envolvam uma tabela com otimização de memória em um banco de dados de usuário não poderão acessar as exibições do sistema do `tempdb` na mesma transação. Se você tentar acessar as exibições do sistema do `tempdb` na mesma transação como uma tabela com otimização de memória em um banco de dados de usuário, receberá o seguinte erro:
    
  ```
  A user transaction that accesses memory optimized tables or natively compiled modules cannot access more than one user database or databases model and msdb, and it cannot write to master.
  ```
    
  Exemplo:
    
  ```sql
  BEGIN TRAN;
  
  SELECT *
  FROM tempdb.sys.tables;  -----> Creates a user in-memory OLTP transaction in tempdb
  
  INSERT INTO <user database>.<schema>.<mem-optimized table>
  VALUES (1); ----> Tries to create a user in-memory OLTP transaction in the user database but will fail
  
  COMMIT TRAN;
  ```
    
- As consultas nas tabelas com otimização de memória não dão suporte a dicas de bloqueio e isolamento; portanto, as consultas nas exibições do catálogo do `tempdb` com otimização de memória não seguirão as dicas de bloqueio e isolamento. Assim como acontece com outras exibições do catálogo do sistema no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], todas as transações nas exibições do sistema serão feitas no isolamento `READ COMMITTED` (ou, neste caso, `READ COMMITTED SNAPSHOT`).

- Os [índices columnstore](../indexes/columnstore-indexes-overview.md) não poderão ser criados em tabelas temporárias quando os metadados com otimização de memória `tempdb` estiverem habilitados.

- Devido à limitação de índices columnstore, não há suporte para uso do procedimento armazenado do sistema `sp_estimate_data_compression_savings` com o parâmetro de compactação de dados `COLUMNSTORE` ou `COLUMNSTORE_ARCHIVE` quando metadados `tempdb` com otimização de memória estão ativados.

> [!NOTE] 
> Essas limitações se aplicam apenas quando você faz referência a exibições do sistema do `tempdb`. Você poderá criar uma tabela temporária na mesma transação ao acessar uma tabela com otimização de memória em um banco de dados do usuário, se desejar.

## <a name="capacity-planning-for-tempdb-in-sql-server"></a>Planejamento de capacidade do tempdb no SQL Server
A determinação do tamanho apropriado para o `tempdb` em um ambiente de produção [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] depende de muitos fatores. Conforme descrito anteriormente, esses fatores incluem a carga de trabalho existente e os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que são usados. Recomendamos que você analise a carga de trabalho existente executando as seguintes tarefas em um ambiente de teste do SQL Server:

- Defina o crescimento automático como ativado para o `tempdb`.
- Execute consultas individuais ou arquivos de rastreamento de carga de trabalho e monitore o uso de espaço do `tempdb`.
- Execute operações de manutenção de índice, como reconstrução de índices, e monitore o espaço do `tempdb`.
- Use os valores de uso de espaço das etapas anteriores para prever o uso total da carga de trabalho. Ajuste esse valor para a atividade simultânea projetada e defina o tamanho de `tempdb` de acordo com isso.

## <a name="monitoring-tempdb-use"></a>Monitorar o uso de tempdb
Ficar sem espaço em disco em `tempdb` pode causar interrupções significativas no ambiente de produção do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso também pode impedir os aplicativos em execução de concluir as operações. Use a exibição de gerenciamento dinâmico [sys.dm_db_file_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) para monitorar o espaço em disco utilizado nos arquivos do `tempdb`:

```sql
 -- Determining the amount of free space in tempdb
SELECT SUM(unallocated_extent_page_count) AS [free pages],
  (SUM(unallocated_extent_page_count)*1.0/128) AS [free space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the amount of space used by the version store
SELECT SUM(version_store_reserved_page_count) AS [version store pages used],
  (SUM(version_store_reserved_page_count)*1.0/128) AS [version store space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the amount of space used by internal objects
SELECT SUM(internal_object_reserved_page_count) AS [internal object pages used],
  (SUM(internal_object_reserved_page_count)*1.0/128) AS [internal object space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the amount of space used by user objects
SELECT SUM(user_object_reserved_page_count) AS [user object pages used],
  (SUM(user_object_reserved_page_count)*1.0/128) AS [user object space in MB]
FROM sys.dm_db_file_space_usage;
 ```

Para monitorar a atividade de alocação ou desalocação de página no `tempdb` no nível da sessão ou tarefa, use as exibições de gerenciamento dinâmico [sys.dm_db_session_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) e [sys.dm_db_task_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md). Essas exibições podem ajudar a identificar consultas grandes, tabelas temporárias ou variáveis de tabela que estão utilizando muito espaço em disco do `tempdb`. Você também pode usar vários contadores para monitorar o espaço livre disponível em `tempdb` e os recursos que estão usando o `tempdb`.

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
