---
title: Banco de dados tempdb | Microsoft Docs
ms.custom: 
ms.date: 11/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- temporary tables [SQL Server], tempdb database
- tempdb database [SQL Server], about tempdb
- temporary stored procedures [SQL Server]
- tempdb database [SQL Server]
ms.assetid: ce4053fb-e37a-4851-b711-8e504059a780
caps.latest.revision: "66"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.openlocfilehash: 6d71dcbda413d604c2c6ac2e4d85a815a4aa3719
ms.sourcegitcommit: ef1fa818beea435f58986af3379853dc28f5efd8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="tempdb-database"></a>Banco de dados tempdb
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] O banco de dados do sistema **tempdb** é um recurso global disponível para todos os usuários conectados à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e é usado para manter o seguinte:  
  
- **Objetos de usuário** temporários criados explicitamente como: índices e tabelas temporárias globais ou locais, procedimentos armazenados temporários, variáveis de tabela, Tabelas retornadas em funções com valor de tabela ou cursores.  
- **Objetos internos** criados pelo [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Eles incluem:
  - Tabelas de trabalho para armazenar resultados intermediários para spools, cursores, classificações e armazenamento temporário LOB (objeto grande).
  - Arquivos de trabalho para operações de junção de hash ou de agregação de hash.
  - Resultados intermediários de classificação para operações como criar ou recriar índices (se SORT_IN_TEMPDB for especificado) ou determinadas consultas GROUP BY, ORDER BY ou UNION.

  > [!NOTE]
  > Cada objeto interno usa um mínimo de nove páginas; uma página IAM e uma extensão de oito páginas. Para obter mais informações sobre páginas e extensões, consulte [Páginas e extensões](../../relational-databases/pages-and-extents-architecture-guide.md#pages-and-extents).

- **Repositórios de versão**, que são uma coleção de páginas de dados que contém linhas de dados necessárias para dar suporte aos recursos que usam o controle de versão de linha. Existem dois armazenamentos de versão: um repositório de versão comum e um armazenamento de versão de criação de índice online. Os armazenamentos de versão contêm o seguinte:
  - Versões de linha geradas por transações de modificação de dados em um banco de dados que usa a leitura de confirmados usando transações de isolação de controle de versão de linha ou isolação de instantâneo.  
  - As versões de linhas geradas por meio de transações de modificação de dados para recursos como: operações de índice on-line, vários conjuntos de resultados ativos (MARS) e gatilhos AFTER.  
  
As operações em **tempdb** são registradas minimamente. Isso permite que transações sejam revertidas. **tempdb** é recriado cada vez que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado, de modo que o sistema sempre começa com uma cópia limpa do banco de dados. As tabelas temporárias e procedimentos armazenados são descartados automaticamente ou desconectados e nenhuma conexão fica ativa quando o sistema é desligado. Portanto, nunca há nada em **tempdb** a ser gravado de uma sessão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para outra. As operações de backup e restauração não são permitidas em **tempdb**.  
  
## <a name="physical-properties-of-tempdb"></a>Propriedades físicas de tempdb  
 A tabela a seguir lista os valores de configuração inicial dos arquivos de dados e de log do **tempdb**, que se baseiam nos padrões para o Modelo de banco de dados. Os tamanhos desses arquivos podem variar um pouco em diferentes edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Arquivo|Nome lógico|Nome físico|Tamanho inicial|Aumento do arquivo|  
|----------|------------------|-------------------|------------------|-----------------|  
|Dados primários|tempdev|tempdb.mdf|8 megabytes|Aumento automático de 64 MB até que o disco fique cheio|  
|Arquivos de dados secundários*|temp#|tempdb_mssql_#.ndf|8 megabytes|Aumento automático de 64 MB até que o disco fique cheio|  
|Log|templog|templog.ldf|8 megabytes|Aumento automático de 64 megabytes até um máximo de 2 terabytes|  
  
 \* O número de arquivos depende do número de processadores (lógicos) do computador. Como regra geral, se o número de processadores lógicos for menor ou igual a oito, use o mesmo número de processadores lógicos para os arquivos de dados. Se o número de processadores lógicos for maior que oito, use oito arquivos de dados e, se a contenção persistir, aumente o número de arquivos de dados em múltiplos de quatro até que a contenção seja reduzida a níveis aceitáveis ou faça alterações no código/carga de trabalho.

> [!NOTE]
> O valor padrão para o número de arquivos de dados baseia-se nas diretrizes gerais de [KB 2154845](http://support.microsoft.com/kb/2154845/).  
  
### <a name="moving-the-tempdb-data-and-log-files"></a>Movendo os arquivos de log e dados de tempdb  
 Para mover os dados e arquivos de log de **tempdb** , veja [Mover bancos de dados do sistema](../../relational-databases/databases/move-system-databases.md).  
  
### <a name="database-options"></a>Opções de banco de dados  
 A tabela a seguir lista o valor padrão de cada opção de banco de dados no banco de dados **tempdb** e se a opção pode ser modificada. Para exibir as configurações atuais dessas opções, use a exibição de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) .  
  
|Opção de banco de dados|Valor padrão|Pode ser modificado|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|Sim|  
|ANSI_NULL_DEFAULT|OFF|Sim|  
|ANSI_NULLS|OFF|Sim|  
|ANSI_PADDING|OFF|Sim|  
|ANSI_WARNINGS|OFF|Sim|  
|ARITHABORT|OFF|Sim|  
|AUTO_CLOSE|OFF|Não|  
|AUTO_CREATE_STATISTICS|ON|Sim|  
|AUTO_SHRINK|OFF|Não|  
|AUTO_UPDATE_STATISTICS|ON|Sim|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|Sim|  
|CHANGE_TRACKING|OFF|Não|  
|CONCAT_NULL_YIELDS_NULL|OFF|Sim|  
|CURSOR_CLOSE_ON_COMMIT|OFF|Sim|  
|CURSOR_DEFAULT|GLOBAL|Sim|  
|Opções de disponibilidade de banco de dados|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|Não<br /><br /> Não<br /><br /> Não|  
|DATE_CORRELATION_OPTIMIZATION|OFF|Sim|  
|DB_CHAINING|ON|Não|  
|ENCRYPTION|OFF|Não|  
|MIXED_PAGE_ALLOCATION|OFF|Não|  
|NUMERIC_ROUNDABORT|OFF|Sim|  
|PAGE_VERIFY|CHECKSUM para novas instalações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> NONE para atualizações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Sim|  
|PARAMETERIZATION|SIMPLE|Sim|  
|QUOTED_IDENTIFIER|OFF|Sim|  
|READ_COMMITTED_SNAPSHOT|OFF|Não|  
|RECOVERY|SIMPLE|Não|  
|RECURSIVE_TRIGGERS|OFF|Sim|  
|Opções do Service Broker|ENABLE_BROKER|Sim|  
|TRUSTWORTHY|OFF|Não|  
  
 Para obter uma descrição dessas opções de banco de dados, veja [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
## <a name="restrictions"></a>Restrições  
 As seguintes operações não podem ser executadas no banco de dados **tempdb** :  
  
- Adição de grupos de arquivos  
- Backup ou restauração de banco de dados.  
- Alteração de agrupamento. O agrupamento padrão é o agrupamento de servidor.  
- Alteração do proprietário do banco de dados. **tempdb** pertence a **sa**.  
- Criação de um instantâneo do banco de dados  
- Descartando o banco de dados.  
- Descartando o usuário **convidado** do banco de dados.  
- Habilitação do Change Data Capture.  
- Participação no espelhamento de banco de dados.  
- Remoção do grupo de arquivos primário, arquivo de dados primário ou arquivo de log.  
- Renomeação do banco de dados ou grupo de arquivos primário.  
- Execução de DBCC CHECKALLOC.  
- Execução de DBCC CHECKCATALOG.  
- Definindo o banco de dados como OFFLINE.  
- Definindo o banco de dados ou grupo de arquivos primário como READ_ONLY.  
  
## <a name="permissions"></a>Permissões  
 Qualquer usuário pode criar objetos temporários no tempdb. Os usuários podem acessar somente seus próprios objetos, a menos que recebam permissões adicionais. É possível revogar a permissão de conexão ao tempdb para impedir um usuário de usar tempdb, mas isto não é recomendado porque algumas operações rotineiras exigem o uso de tempdb.  

## <a name="optimizing-tempdb-performance"></a>Otimizando o desempenho do tempdb
 O tamanho e o posicionamento físico do banco de dados tempdb podem afetar o desempenho de um sistema. Por exemplo, se o tamanho definido para tempdb for muito pequeno, parte da carga de processamento do sistema poderá ser elevada com o crescimento automático de tempdb para o tamanho necessário para oferecer suporte à carga de trabalho toda vez que você reiniciar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

 Se possível, use a [inicialização instantânea de arquivo do banco de dados](../../relational-databases/databases/database-instant-file-initialization.md) para melhorar o desempenho das operações de crescimento de arquivo de dados.
 
 Aloque espaço antecipadamente para todos os arquivos do tempdb definindo o tamanho de arquivo com um valor grande o bastante para acomodar a carga de trabalho comum no ambiente. Isso impede que o tempdb seja expandido muito frequentemente, o que pode afetar o desempenho. O banco de dados tempdb deve ser definido como crescimento automático, mas isso deve ser usado para aumentar o espaço em disco para exceções não planejadas. 

 Os arquivos de dados devem ser de tamanho igual em cada [grupo de arquivos](../../relational-databases/databases/database-files-and-filegroups.md#filegroups), pois o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa um algoritmo de preenchimento proporcional que favorece alocações em arquivos com mais espaço livre. A divisão do tempdb em vários arquivos de dados de tamanho igual fornece um alto grau de eficiência paralela em operações que usam o tempdb. 
 
 Defina o incremento de crescimento do arquivo com um tamanho razoável para evitar que os arquivos do banco de dados tempdb cresçam com um valor muito pequeno. Se o crescimento do arquivo for muito pequeno, comparado à quantidade de dados que está sendo gravada no tempdb, o tempdb talvez tenha que se expandir constantemente. Isso afetará o desempenho.
 
 Para verificar o tamanho atual do tempdb e os parâmetros de crescimento, use a seguinte consulta:
 ```t-sql
 SELECT name AS FileName, 
    size*1.0/128 AS FileSizeinMB,
    CASE max_size 
        WHEN 0 THEN 'Autogrowth is off.'
        WHEN -1 THEN 'Autogrowth is on.'
        ELSE 'Log file will grow to a maximum size of 2 TB.'
    END,
    growth AS 'GrowthValue',
    'GrowthIncrement' = 
        CASE
            WHEN growth = 0 THEN 'Size is fixed and will not grow.'
            WHEN growth > 0 AND is_percent_growth = 0 
                THEN 'Growth value is in 8-KB pages.'
            ELSE 'Growth value is a percentage.'
        END
FROM tempdb.sys.database_files;
GO
```
 
 Coloque o banco de dados tempdb em um subsistema de E/S rápido. Use a distribuição de disco se houver muitos discos anexados diretamente. Arquivos de dados individuais ou grupos de arquivos de dados do tempdb não precisam necessariamente estar em discos ou eixos diferentes, a menos que você também esteja tendo gargalos de E/S.
 
 Coloque o banco de dados tempdb em discos diferentes dos usados por bancos de dados de usuários.

## <a name="performance-improvements-in-tempdb"></a>Melhorias de desempenho no tempdb  
 A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], o desempenho do **tempdb** é ainda mais otimizado das seguintes maneiras:  
  
- As tabelas temporárias e variáveis de tabela são armazenadas em cache. O armazenamento em cache permite que as operações de descarte e criação de objetos temporários sejam executadas rapidamente e reduz a contenção de alocação de página.  
- O protocolo de travamento da página de alocação é aprimorado. Isso reduz o número de travas de UP (atualização) usadas.  
- A sobrecarga de logging para **tempdb** é reduzida. Isso reduz o consumo de largura de banda de E/S do disco no arquivo de log **tempdb** .  
- A Instalação adiciona vários arquivos de dados tempdb durante uma nova instalação da instância. Essa tarefa pode ser realizada com o novo controle de entrada da interface do usuário na seção **Configuração do Mecanismo de Banco de Dados** e em um parâmetro de linha de comando /SQLTEMPDBFILECOUNT. Por padrão, a instalação adicionará um número de arquivos de dados do tempdb equivalente à contagem de processadores lógicos ou a 8, o que for menor.  
- Quando houver vários arquivos de dados **tempdb** , todos os arquivos aumentarão automaticamente e na mesma quantidade, dependendo das configurações de aumento. O sinalizador de rastreamento 1117 já não é necessário.  
- Além disso, todas as alocações em **tempdb** usam extensões uniformes. O [sinalizador de rastreamento 1118](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) não é mais necessário.  
- Para o grupo de arquivos primário, a propriedade AUTOGROW_ALL_FILES está ativada e não pode ser modificada. 

## <a name="capacity-planning-for-tempdb"></a>Planejamento de capacidade para tempdb
 A determinação do tamanho apropriado para o tempdb em um ambiente de produção depende de muitos fatores. Como previamente descrito neste tópico, esses fatores incluem a carga de trabalho existente e os recursos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizados. Recomendamos que você analise a carga de trabalho existente executando as seguintes tarefas em um ambiente de teste do SQL Server:
- Defina o crescimento automático como ativado para o tempdb.
- Execute consultas individuais ou arquivos de rastreamento de carga de trabalho e monitore o uso de espaço do tempdb.
- Execute operações de manutenção de índice, como recriação de índices e monitore o espaço do tempdb. 
- Use os valores de uso de espaço das etapas anteriores para prever o uso total da carga de trabalho; ajuste esse valor para atividades simultâneas projetadas e, em seguida, defina o tamanho do tempdb de acordo.

## <a name="how-to-monitor-tempdb-use"></a>Como monitorar o uso do tempdb
  O espaço em disco insuficiente no tempdb pode causar interrupções significativas no ambiente de produção do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e impedir que aplicativos que estão em execução concluam as operações. Use a exibição de gerenciamento dinâmico [sys.dm_db_file_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) para monitorar o espaço em disco utilizado nos arquivos do tempdb:
  
 ```t-sql
 -- Determining the Amount of Free Space in tempdb
 SELECT SUM(unallocated_extent_page_count) AS [free pages], 
  (SUM(unallocated_extent_page_count)*1.0/128) AS [free space in MB]
 FROM sys.dm_db_file_space_usage;
 ```
 
 ```t-sql
 -- Determining the Amount Space Used by the Version Store
 SELECT SUM(version_store_reserved_page_count) AS [version store pages used],
  (SUM(version_store_reserved_page_count)*1.0/128) AS [version store space in MB]
 FROM sys.dm_db_file_space_usage;
 ```
 
 ```t-sql
 -- Determining the Amount of Space Used by Internal Objects
 SELECT SUM(internal_object_reserved_page_count) AS [internal object pages used],
  (SUM(internal_object_reserved_page_count)*1.0/128) AS [internal object space in MB]
 FROM sys.dm_db_file_space_usage;
 ```
 
 ```t-sql
 -- Determining the Amount of Space Used by User Objects
 SELECT SUM(user_object_reserved_page_count) AS [user object pages used],
  (SUM(user_object_reserved_page_count)*1.0/128) AS [user object space in MB]
 FROM sys.dm_db_file_space_usage;
 ```
  
  Além disso, para monitorar a atividade de alocação ou desalocação de página no tempdb em nível de sessão ou tarefa, use as exibições de gerenciamento dinâmico [sys.dm_db_session_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) e [sys.dm_db_task_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md). Essas exibições podem ser usadas para identificar consultas grandes, tabelas temporárias ou variáveis de tabela que estão utilizando muito espaço em disco do tempdb. Também existem vários contadores que podem ser usados para monitorar o espaço livre disponível no tempdb e também os recursos que estão usando o tempdb. Para obter mais informações, consulte a próxima seção.

 ```t-sql
 -- Obtaining the space consumed by internal objects in all currently running tasks in each session
 SELECT session_id, 
  SUM(internal_objects_alloc_page_count) AS task_internal_objects_alloc_page_count,
  SUM(internal_objects_dealloc_page_count) AS task_internal_objects_dealloc_page_count 
 FROM sys.dm_db_task_space_usage 
 GROUP BY session_id;
 ```
 
 ```t-sql
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
 [Opção SORT_IN_TEMPDB para índices](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)  
 [Bancos de dados do sistema](../../relational-databases/databases/system-databases.md)  
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
 [Mover arquivos de banco de dados](../../relational-databases/databases/move-database-files.md)  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com tempdb no SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=81216)  
 [Solução de problemas de espaço em disco insuficiente no tempdb](http://msdn.microsoft.com/library/ms176029.aspx) 
