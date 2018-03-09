---
title: "Novidades no mecanismo de banco de dados – SQL Server 2016 | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: database-engine
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- what's new [SQL Server Database Engine]
- Database Engine [SQL Server], what's new
ms.assetid: 8f625d5a-763c-4440-97b8-4b823a6e2439
caps.latest.revision: "431"
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Active
ms.openlocfilehash: 0e5018b6b111790d2ff0415180e0608798da44ac
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="whats-new-in-database-engine---sql-server-2016"></a>Novidades no mecanismo de banco de dados – SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Este tópico resume os aperfeiçoamentos introduzidos na versão [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)].  Os novos recursos e aprimoramentos aumentam o poder e a produtividade de arquitetos, desenvolvedores e administradores que criam, desenvolvem e mantêm sistemas de armazenamento de dados.

Para examinar quais são as novidades em outros componentes do SQL Server, veja [Novidades no SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md).

> [!NOTE]
>  [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] é um aplicativo de 64 bits. A instalação de 32 bits foi descontinuada, embora alguns elementos sejam executados como componentes de 32 bits.

#### <a name="try-it-out"></a>Experimente

- Para baixar o [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], acesse  **[Centro de Avaliação](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**![baixar](../analysis-services/media/download.png "download").

- Tem uma conta do Azure?  Então, acesse **[aqui](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/)** para executar uma máquina virtual com o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] já instalado.

> [!NOTE]
> Para obter as notas de versão atuais, veja [Notas de versão do SQL Server 2016](../sql-server/sql-server-2016-release-notes.md).
  
## <a name="sql-server-2016-service-pack-1-sp1"></a>SQL Server 2016 Service Pack 1 (SP1)  
-  `CREATE OR ALTER <object>` sintaxe agora está disponível para [procedimentos](../t-sql/statements/create-procedure-transact-sql.md), [exibições](../t-sql/statements/create-view-transact-sql.md)e [funções](../t-sql/statements/create-function-transact-sql.md)e [gatilhos](../t-sql/statements/create-trigger-transact-sql.md).
-   Foi adicionado suporte a um modelo mais genérico de dicas de consulta: `OPTION (USE HINT('<hint1>', '<hint2>'))`. Para obter mais informações, veja [Dicas de consulta (Transact-SQL)](../t-sql/queries/hints-transact-sql-query.md).  
- A DMV [sys.dm_exec_valid_use_hints](../relational-databases/system-dynamic-management-views/sys-dm-exec-valid-use-hints-transact-sql.md) foi adicionada às dicas de lista.  
- A DMV [sys.dm_exec_query_statistics_xml](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md) foi adicionada para retornar estatísticas transitórias de plano de execução XML.  
- A DMV [sys.dm_db_incremental_stats_properties](../relational-databases/system-dynamic-management-views/sys-dm-db-incremental-stats-properties-transact-sql.md) foi adicionada para estatísticas incrementais para a tabela especificada.  
- A coluna `instant_file_initialization_enabled` foi adicionada à [sys.dm_server_services](../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md).  
- A coluna de    `estimated_read_row_count` foi adicionada à [sys.dm_exec_query_profiles](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md).  
-  As colunas `sql_memory_model` e `sql_memory_model_desc` foram adicionadas à [sys.dm_os_sys_info](../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) para fornecer informações sobre o modelo de bloqueio de páginas de memória.
-  As edições que oferecem suporte a uma série de recursos foram expandidas. Isso inclui a adição de segurança em nível de linha, Always Encrypted, máscara de dados dinâmicos, auditoria de banco de dados, OLTP na memória e vários outros recursos para todas as edições. Para obter mais informações, consulte [Edições e Recursos com suporte para o SQL Server 2016](../sql-server/editions-and-supported-features-for-sql-server-2016.md).   
-  [sp_refresh_parameter_encryption](../relational-databases/system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md) permite que a criptografia AlwaysOn atualize metadados, quando os objetos são criptografados usando AlwaysOn são redefinidos.  


##  <a name="Feature"></a> SQL Server 2016 RTM
Esta seção contém as seguintes subseções:

-   [Índices columnstore](#columnstore)
-   [Configurações no Escopo do Banco de Dados](#scopedconfiguration)
-   [OLTP na memória](#InMemory)
-   [Otimizador de consulta](#QueryOptimizer)
-   [Estatísticas de consulta dinâmica](#LiveStats)
-   [Repositório de Consultas](#QueryStore)
-   [Tabelas temporais](#TT)
-   [Backups distribuídos para o Armazenamento de Blobs do Microsoft Azure](#StripedBackupToAzure)
-   [Backups de instantâneos de arquivos para o Armazenamento de Blobs do Microsoft Azure](#FileSnapshotBackup)
-   [Backup Gerenciado](#ManagedBackup)
-   [Banco de dados TempDB](#multipleTempDB)
-   [Suporte interno a JSON](#ForJson)
-   [PolyBase](#bkPolyBase)
-   [Stretch Database](#stretch)
-   [Suporte a UTF-8](#UTF8)
-   [Novos valores padrão de tamanho do banco de dados e de aumento automático](#DefaultDB)
-   [Aprimoramentos de Transact-SQL](#TSQL)
-   [Aprimoramentos do Modo de Exibição do Sistema](#SystemTable)
-   [Aprimoramentos de segurança](#Security)
-   [Aprimoramentos de Alta disponibilidade](#HighAvailability)
-   [Aprimoramentos de Replicação](#Repl)
-   [Aprimoramentos de ferramentas](#Tools)

####  <a name="columnstore"></a> Índices columnstore

Esta versão oferece melhorias para índices columnstore, incluindo índices columnstore não clusterizados atualizáveis, índices columnstore em tabelas na memória e muitos outros novos recursos para análise operacional.

- Um índice columnstore não clusterizado somente leitura é atualizável após a atualização.  Não é necessário recompilar o índice para torná-la atualizável.

- Existem aprimoramentos de desempenho para consultas de análise em índices columnstore, especialmente para agregações e predicados de cadeia de caracteres.

- DMVs e XEvents têm aprimoramentos de capacidade de suporte.

Para obter mais detalhes, confira estes tópicos na seção [Guia de índices columnstore](../relational-databases/indexes/columnstore-indexes-overview.md) dos Manuais Online:

- [Resumo de recursos dos índices columnstore](~/relational-databases/indexes/columnstore-indexes-what-s-new.md) – inclui as novidades.

- [Carregamento de dados dos índices columnstore](../relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)

- [Desempenho de consultas de índices columnstore](~/relational-databases/indexes/columnstore-indexes-query-performance.md)

- [Introdução ao Columnstore para análise operacional em tempo real](../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)

- [Índices columnstore para Data Warehousing](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)

- [Desfragmentação de índices columnstore](~/relational-databases/indexes/columnstore-indexes-defragmentation.md)


####  <a name="scopedconfiguration"></a> Configurações no escopo do banco de dados


A nova instrução [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) fornece controle de determinadas configurações de um banco de dados específico. As definições de configuração afetam o comportamento do aplicativo.

A nova instrução está disponível no [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] e [!INCLUDE[sqldbesa](../includes/sqldbesa-md.md)].



####  <a name="InMemory"></a> OLTP na memória


##### <a name="storage-format-change"></a>Alteração do formato de armazenamento

O formato de armazenamento para tabelas com otimização de memória foi alterado entre o SQL Server 2014 e o 2016. Para atualização e anexação/restauração do SQL Server 2014, o novo formato de armazenamento é serializado e o banco de dados é reiniciado uma vez durante a recuperação de banco de dados.

- [Atualizar para o SQL Server 2016](../database-engine/install-windows/upgrade-sql-server.md)


##### <a name="alter-table-is-log-optimized-and-runs-in-parallel"></a>ALTER TABLE é otimizado para log e executado em paralelo

Agora, quando você executa uma instrução ALTER TABLE em uma tabela com otimização de memória, apenas as alterações de metadados são gravadas no log. Isso reduz significativamente a E/S de log. Além disso, a maioria dos cenários de ALTER TABLE agora são executadas em paralelo, o que pode reduzir significativamente a duração da instrução.

- Para exceções não paralelas, incluindo LOBs, veja [Alterando tabelas com otimização de memória](../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md).



##### <a name="statistics"></a>Estatísticas

As[estatísticas para tabelas com otimização de memória](../relational-databases/in-memory-oltp/statistics-for-memory-optimized-tables.md) agora são atualizadas automaticamente. Além disso, a amostragem agora é um método com suporte para a coleta de estatísticas, permitindo evitar o método fullscan mais caro.


##### <a name="parallel-and-heap-scan-for-memory-optimized-tables"></a>Verificação paralela e de heap para tabelas com otimização de memória

Tabelas com otimização de memória e índices em tabelas com otimização de memória agora dão suporte à verificação paralela. Isso melhora o desempenho de consultas analíticas.

Além disso, a verificação de heap tem suporte e pode ser executada em paralelo. No caso de uma tabela com otimização de memória, uma verificação de heap faz referência à verificação de todas as linhas de uma tabela usando a estrutura de dados de heap na memória usada para armazenar as linhas. Para uma verificação completa da tabela, a verificação de heap é mais eficiente do que usar um índice.

##### <a name="transact-sql-improvements-for-memory-optimized-tables"></a>Melhorias do Transact-SQL para tabelas com otimização de memória

Há vários elementos do Transact-SQL que não tinham suporte em tabelas com otimização de memória no SQL Server 2014, que agora têm suporte no SQL Server 2016:


- Há suporte para os índices e restrições UNIQUE.


- Há suporte para referências FOREIGN KEY entre tabelas com otimização de memória.
  - Essas chaves estrangeiras podem fazer referência a apenas uma chave primária e não podem fazer referência a uma chave exclusiva.


- Há suporte para restrições CHECK.

- Um índice não exclusivo pode permitir valores NULL em sua chave.

- Há suporte para TRIGGERs em tabelas com otimização de memória.
  - Somente gatilhos AFTER têm suporte. Gatilhos INSTEADOF não têm suporte.
  - Qualquer gatilho em uma tabela com otimização de memória deve usar WITH NATIVE_COMPILATION.

- Suporte completo para todas as páginas de código do SQL Server e agrupamentos com índices e outros artefatos em tabelas com otimização de memória e módulos compilados nativamente do T-SQL.


- Suporte para [Alteração de tabelas com otimização de memória](../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md):
  - Índices ADD e DROP. Alterar bucket_count de índices de hash.
  - Fazer alterações de esquema: adicionar/cancelar/alterar colunas; adicionar/remover restrições.

- Uma tabela com otimização de memória agora pode ter várias colunas cujos tamanhos combinados são maiores do que o tamanho da página de 8.060 bytes. Um exemplo é uma tabela que contém três colunas do tipo `nvarchar(4000)`. Em exemplos como esse, algumas colunas agora são armazenadas fora da linha. Felizmente, as consultas não reconhecem se uma coluna está na linha ou fora da linha.

- [Tipos de LOB (objeto grande)](../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md) `varbinary(max)`, `nvarchar(max)`e `varchar(max)` agora têm suporte em tabelas com otimização de memória.


Para obter informações gerais, veja:

- [Construções do Transact-SQL sem suporte pelo OLTP na memória](../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)
- [Recursos do SQL Server sem suporte para OLTP na Memória](~/relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md)


##### <a name="transact-sql-improvements-for-natively-compiled-modules"></a>Melhorias do Transact-SQL para módulos compilados de modo nativo

Há alguns elementos do Transact-SQL que não tinham suporte em módulos compilados de modo nativo no SQL Server 2014, que agora têm suporte no SQL Server 2016:


- Construções de consulta:
  - UNION e UNION ALL
  - SELECT DISTINCT
  - OUTER JOIN
  - Subconsultas em SELECT


- Instruções INSERT, UPDATE e DELETE agora podem incluir a [cláusula OUTPUT](../t-sql/queries/output-clause-transact-sql.md).

- LOBs agora podem ser usados das seguintes maneiras em um procedimento nativo:
  - Declaração de variáveis.
  - Parâmetros de entrada recebidos.
  - Parâmetros passados para funções de cadeia de caracteres, como em LTrim ou Substring, em um procedimento nativo.


- TVFs (funções com valor de tabela) embutidas (em outras palavras, instrução única) agora podem ser compiladas de modo nativo.

- UDFs (funções definidas pelo usuário) escalares agora podem ser compiladas de modo nativo.

- Maior suporte para um processo nativo para a chamada de:
  - [Funções de segurança](../t-sql/functions/security-functions-transact-sql.md)internas.
  - [Funções matemáticas](../t-sql/functions/mathematical-functions-transact-sql.md)internas.
  - Função interna `@@SPID`.


- EXECUTE AS CALLER agora tem suporte, o que significa que a cláusula EXECUTE não é mais necessária durante a criação de um módulo do T-SQL compilado nativamente.


Para obter informações gerais, veja:

- [Recursos com suporte para módulos T-SQL compilados nativamente](../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)
- [Alterar módulos T-SQL compilados nativamente](../relational-databases/in-memory-oltp/altering-natively-compiled-t-sql-modules.md)


##### <a name="performance-and-scaling-improvements"></a>Melhorias no desempenho e dimensionamento

- Não há mais nenhuma limitação para o tamanho dos dados. Consulte [Estimar requisitos de memória para tabelas com otimização de memória](~/relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md).

- Agora, há vários threads simultâneos responsáveis por [manter em disco as alterações às tabelas com otimização de memória](../relational-databases/in-memory-oltp/scalability.md).

- Suporte a plano paralelo para [acesso a tabelas com otimização de memória usando o Transact-SQL interpretado](../relational-databases/in-memory-oltp/accessing-memory-optimized-tables-using-interpreted-transact-sql.md).


##### <a name="enhancements-in-sql-server-management-studio"></a>Melhorias no SQL Server Management Studio

- A opção [Determinando se uma tabela ou um procedimento armazenado deve ser movido para o OLTP in-memory](../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md) não exige mais a configuração de coletores de dados nem de data warehouse de gerenciamento. O relatório agora pode ser executado diretamente em um banco de dados de produção.

- [Cmdlet do PowerShell para avaliação de migração](../relational-databases/in-memory-oltp/powershell-cmdlet-for-migration-evaluation.md) para avaliar a adequação de migração de vários objetos em um banco de dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .

- Gere listas de verificação de migração clicando com o botão direito do mouse em um banco de dados e selecionando Tarefas > Gerar listas de verificação de migração do OLTP in-memory.

##### <a name="cross-feature-support"></a>Suporte entre recursos

- Suporte para uso de determinação de versão do sistema temporal com OLTP in-memory. Para obter mais informações, veja [Tabelas temporais com controle de versão do sistema com tabelas com otimização de memória](../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)

- Suporte ao repositório de consultas para código nativo compilado de cargas de trabalho OLTP in-memory. Para obter mais informações, veja [Usando o repositório de consultas com o OLTP in-memory](../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md).

- [Segurança em nível de linha em tabelas com otimização de memória](../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md#rls)

- As conexões [Usando MARS &#40;Multiple Active Result Sets&#41;](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) agora podem acessar tabelas com otimização de memória e procedimentos armazenados compilados nativamente.

- Suporte à [TDE](../relational-databases/security/encryption/transparent-data-encryption.md) (Transparent Data Encryption). Se um banco de dados estiver configurado para ENCRYPTION, os arquivos no [Grupo de arquivos com otimização de memória](../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md) também serão criptografados agora.

Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).


####  <a name="QueryOptimizer"></a> Otimizador de consulta
##### <a name="compatibility-level-guarantees"></a>Garantias de nível de compatibilidade
Quando você atualizar seu banco de dados para o SQL Server 2016, não haverá nenhuma alteração de plano se você permanecer nos níveis de compatibilidade mais antigos que estava usando (por exemplo, 120 ou 110). Novos recursos e aprimoramentos relacionados ao otimizador de consultas estarão disponíveis somente no nível de compatibilidade mais recente. 
##### <a name="trace-flag-4199"></a>Sinalizador de rastreamento 4199
Em geral, não é necessário usar o sinalizador de rastreamento 4199 no SQL Server 2016, já que a maioria dos comportamentos de otimizador de consulta controlados por este sinalizador de rastreamento está habilitada incondicionalmente no nível de compatibilidade mais recente (130) no SQL Server 2016.
##### <a name="new-referential-integrity-operator"></a>Novo operador de integridade referencial
Uma tabela pode fazer referência a no máximo 253 outras tabelas e colunas como chaves estrangeiras (referências de saída). [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] aumenta de 253 para 10.000 o limite para o número de outras tabelas e colunas que podem fazer referência a colunas em uma única tabela (referências de entrada). Para restrições, consulte [Create Foreign Key Relationships](../relational-databases/tables/create-foreign-key-relationships.md). Foi introduzido um novo operador de integridade referencial (no nível de compatibilidade 130) que executa as verificações de integridade referencial em vigor. Isso melhora o desempenho geral de operações UPDATE e DELETE em tabelas que têm um grande número de referências de entrada, tornando possível ter um grande número de referências de entrada. Para obter mais informações, consulte [Query Optimizer Additions in SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/23/query-optimizer-additions-in-sql-server/)(Acréscimos do otimizador de consultas no SQL Server 2016)
##### <a name="parallel-update-of-sampled-statistics"></a>Atualização paralela de estatísticas por amostra
A amostragem de dados para criar estatísticas agora é feita em paralelo (no nível de compatibilidade 130) para melhorar o desempenho da coleta de estatísticas. Para obter mais informações, consulte [Atualizar estatísticas](../t-sql/statements/update-statistics-transact-sql.md).
#### <a name="sublinear-threshold-for-update-of-statistics"></a>Limite sublinear para atualização de estatísticas
A atualização automática de estatísticas agora é mais agressiva em tabelas grandes (no nível de compatibilidade 130). O limite para disparar a atualização automática de estatísticas é 20%, a partir do SQL Server 2016, para tabelas maiores. Esse limite começará a diminuir (ainda uma porcentagem) conforme o número de linhas na tabela aumentar. Você não precisará mais definir o sinalizador de rastreamento 2371 para reduzir o limite. 
##### <a name="other-enhancements"></a>Outros aprimoramentos
O Insert em uma instrução Insert-select tem vários threads ou pode ter um plano paralelo (no nível de compatibilidade 130). Para obter um plano paralelo, INSIRA… A instrução SELECT deve usar a dica TABLOCK. Para obter mais informações, consulte [Selecionar inserção paralela](https://blogs.msdn.microsoft.com/sqlcat/2016/07/06/sqlsweet16-episode-3-parallel-insert-select/)

####  <a name="LiveStats"></a> Estatísticas de consulta dinâmica
 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] fornece a capacidade de exibir o plano de execução ao vivo de uma consulta ativa. Esse plano de consulta ao vivo fornece visões em tempo real sobre o processo de execução da consulta, conforme os controles são transmitidos de um operador de plano de consulta para outro. Para obter mais informações, consulte [Estatísticas de consulta em tempo real](../relational-databases/performance/live-query-statistics.md).

####  <a name="QueryStore"></a> Repositório de Consultas
O repositório de consultas é um novo recurso que fornece aos DBAs informações sobre escolha e desempenho do plano de consulta. Ele simplifica a solução de problemas, permitindo que você localize rapidamente diferenças de desempenho causadas por alterações nos planos de consulta. O recurso captura automaticamente um histórico de consultas, planos e estatísticas de tempo de execução e os mantém para sua análise. Ele separa os dados por janelas de tempo, permitindo que você veja os padrões de uso do banco de dados e entenda quando as alterações aos planos de consulta ocorreram no servidor. O repositório de consultas apresenta informações usando uma caixa de diálogo [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] , e permite que você force a consulta para um dos planos de consulta selecionados. Para saber mais, consulte [Monitoring Performance By Using the Query Store](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).


####  <a name="TT"></a> Tabelas temporais
[!INCLUDE[ssSQL15](../includes/sssql15-md.md)] agora dá suporte a tabelas temporais com controle de versão do sistema. Uma tabela temporal é um novo tipo de tabela que fornece as informações corretas sobre fatos armazenados em qualquer ponto no tempo. Cada tabela temporal consiste na verdade em duas tabelas, uma para os dados atuais e outra para os dados históricos. O sistema garante que, quando ocorrerem alterações nos dados da tabela com os dados atuais, os valores anteriores serão armazenados na tabela de histórico. Construções de consulta são fornecidas para ocultar essa complexidade dos usuários. Para saber mais, veja [Temporal Tables](../relational-databases/tables/temporal-tables.md).

####  <a name="StripedBackupToAzure"></a> Backups distribuídos para o Armazenamento de Blobs do Microsoft Azure
No [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], o backup em URL do SQL Server com o uso do serviço de armazenamento de Blobs do Microsoft Azure agora dá suporte a conjuntos de backups distribuídos usando blobs de blocos para dar suporte a um tamanho máximo de backup de 12,8 TB. Para obter exemplos, consulte [Code Examples](../relational-databases/backup-restore/sql-server-backup-to-url.md#Examples).

####  <a name="FileSnapshotBackup"></a> Backups de instantâneos de arquivos para o Armazenamento de Blobs do Microsoft Azure
 No [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], o backup em URL do SQL Server agora dá suporte ao uso de instantâneos do Azure para fazer backup de bancos de dados em que todos os arquivos de bancos de dados são armazenados usando o serviço de armazenamento de Blobs do Microsoft Azure. Para obter mais informações, consulte [Backups de instantâneo de arquivo para arquivos de banco de dados no Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).

####  <a name="ManagedBackup"></a> Backup Gerenciado
No [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] , o Backup Gerenciado do SQL Server no Microsoft Azure usa o novo armazenamento de blobs de blocos para arquivos de backup. Há também várias alterações e aprimoramentos no Backup Gerenciado.

-   Há suporte tanto para agendamento automatizado quanto personalizado de backups.

-   Há suporte para backups para bancos de dados do sistema.

-   Há suporte para bancos de dados que usem o Modelo de recuperação simples.

 Para obter mais informações, consulte [SQL Server Managed Backup to Microsoft Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md).

> [!NOTE]
>  Para o [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], esses novos recursos de backup gerenciados ainda não têm suporte à interface do usuário correspondente no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].

####  <a name="multipleTempDB"></a> Banco de dados TempDB
 Há várias aprimoramentos para TempDB:

-   Os sinalizadores de rastreamento 1117 e 1118 não são mais necessários para tempdb. Se houver vários arquivos de banco de dados tempdb, todos os arquivos aumentarão ao mesmo tempo, dependendo das configurações de aumento. Além disso, todas as alocações em tempdb usarão extensões uniformes.

-   Por padrão, a instalação adiciona um número de arquivos tempdb equivalente à contagem de CPU ou a 8, o que for menor.

-   Durante a instalação, você pode configurar o número de arquivos de banco de dados tempdb, o tamanho inicial, o aumento automático e o posicionamento em diretório usando o novo controle de entrada da interface do usuário na seção Configuração do Mecanismo de Banco de Dados - TempDB do Assistente de Instalação do SQL Server.

-   O tamanho inicial padrão é 8 MB e o aumento automático padrão é 64 MB.

-   Você pode especificar vários volumes para arquivos de banco de dados tempdb. Se vários diretórios forem especificados, arquivos de dados tempdb serão espalhados pelos diretórios de forma round robin.

####  <a name="ForJson"></a> Suporte interno a JSON
O SQL Server 2016 adiciona suporte interno para importação e exportação de JSON e trabalho com cadeias de caracteres JSON. Esse suporte interno inclui as instruções e funções a seguir.

-   Formate os resultados da consulta como JSON, ou exporte o JSON, adicionando a cláusula **FOR JSON** a uma instrução **SELECT** . Use a cláusula **FOR JSON**, por exemplo, para delegar a formatação da saída JSON de aplicativos cliente ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Formatar resultados da consulta como JSON com FOR JSON &#40;SQL Server&#41;](../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).

-   Converta dados JSON em linhas e colunas, ou importe o JSON, chamando a função de provedor de conjunto de linhas **OPENJSON**. Use **OPENJSON** para importar dados JSON para o SQL Server, ou converter dados JSON em linhas e colunas para um aplicativo ou serviço que atualmente não pode consumir JSON diretamente. Para obter mais informações, veja [Converter dados JSON em linhas e colunas com OPENJSON &#40;SQL Server&#41;](../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md).

-   A função **ISJSON** testa se uma cadeia de caracteres contém JSON válido. Para obter mais informações, veja [ISJSON &#40;Transact-SQL&#41;](../t-sql/functions/isjson-transact-sql.md)

-   A função **JSON_VALUE** extrai um valor escalar de uma cadeia de caracteres JSON. Para obter mais informações, veja [JSON_VALUE &#40;Transact-SQL&#41;](../t-sql/functions/json-value-transact-sql.md).

-   A função **JSON_QUERY** extrai um objeto ou uma matriz de uma cadeia de caracteres JSON. Para obter mais informações, veja [JSON_QUERY &#40;Transact-SQL&#41;](../t-sql/functions/json-query-transact-sql.md).

-   A função **JSON_MODIFY** atualiza o valor de uma propriedade em uma cadeia de caracteres JSON e retorna a cadeia de caracteres JSON atualizada. Para obter mais informações, veja [JSON_MODIFY &#40;Transact-SQL&#41;](../t-sql/functions/json-modify-transact-sql.md).

####  <a name="bkPolyBase"></a> PolyBase
 O PolyBase permite que você use instruções T-SQL para acessar dados armazenados no Hadoop ou no armazenamento de Blobs do Azure e consultá-los ad hoc. Ele também permite consultar dados semiestruturados e associar os resultados com conjuntos de dados relacionais armazenados no SQL Server. O PolyBase é otimizado para o armazenamento de cargas de trabalho em data warehouses e destinado a cenários de consulta analítica.

 Para obter mais informações, veja [Guia do PolyBase](../relational-databases/polybase/polybase-guide.md).

####  <a name="stretch"></a> Stretch Database
 O Stretch Database é um novo recurso do [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] que migra seus dados históricos de forma transparente e segura para a nuvem do Microsoft Azure. Acesse os dados do SQL Server diretamente, independentemente de ele ser local ou estendido para a nuvem. Você define a política que determina onde os dados são armazenados e o SQL Server trata a movimentação de dados em segundo plano. A tabela inteira está sempre online e é passível de consulta. Além disso, o Stretch Database não exige nenhuma mudança para aplicativos ou consultas existentes – o local dos dados é completamente transparente para o aplicativo. Para obter mais informações, consulte [Stretch Database](../sql-server/stretch-database/stretch-database.md).
 
####  <a name="UTF8"></a> Suporte a UTF-8
[O Utilitário bcp](../tools/bcp-utility.md), [BULK INSERT](../t-sql/statements/bulk-insert-transact-sql.md) e [OPENROWSET](../t-sql/functions/openrowset-transact-sql.md) agora dão suporte à página de código UTF-8. Para obter mais informações, confira esses tópicos e [Criar um arquivo de formato XML &#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md).

####  <a name="DefaultDB"></a> Novos valores padrão de tamanho do banco de dados e de aumento automático
Novos valores para o modelo de banco de dados modelo e valores padrão para novos bancos de dados (que são baseados no modelo). O tamanho inicial dos arquivos de log e de dados é agora de 8 MB. O aumento automático padrão dos arquivos de log e de dados é agora de 64 MB.


###  <a name="TSQL"></a> Aprimoramentos de Transact-SQL
Várias melhorias dão suporte aos recursos descritos nas outras seções deste tópico. Os aprimoramentos adicionais a seguir estão disponíveis.
- A instrução TRUNCATE TABLE agora permite o truncamento de partições especificadas. Para obter mais informações, veja [TRUNCATE TABLE &#40;Transact-SQL&#41;](../t-sql/statements/truncate-table-transact-sql.md).
- [ALTER TABLE &#40;Transact-SQL&#41;](../t-sql/statements/alter-table-transact-sql.md) agora permite que muitas ações de coluna sejam executadas enquanto a tabela permanece disponível.
- O índice de texto completo DMV [sys.dm_fts_index_keywords_position_by_document &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-position-by-document-transact-sql.md) retorna o local das palavras-chave em documentos. Essa DMV também foi adicionada no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] SP2 e [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP1.
- Uma nova dica de consulta **NO_PERFORMANCE_SPOOL** pode impedir que um operador de spool seja adicionado a planos de consulta. Isso pode melhorar o desempenho quando várias consultas simultâneas estiverem executando com operações de spool. Para obter mais informações, veja [Dicas de consulta &#40;Transact-SQL&#41;](../t-sql/queries/hints-transact-sql-query.md).
- A instrução [FORMATMESSAGE &#40;Transact-SQL&#41;](../t-sql/functions/formatmessage-transact-sql.md) foi aprimorada para aceitar um argumento msg_string.
- O tamanho máximo de chave de índice para índices NONCLUSTERED foi aumentado para 1700 bytes.
- Uma nova sintaxe DROP IF foi adicionada para as instruções drop relacionadas a AGGREGATE, ASSEMBLY, COLUMN, CONSTRAINT, DATABASE, DEFAULT, FUNCTION, INDEX, PROCEDURE, ROLE, RULE, SCHEMA, SECURITY POLICY, SEQUENCE, SYNONYM, TABLE, TRIGGER, TYPE, USER e VIEW. Consulte os tópicos individuais de sintaxe para conhecer a sintaxe.
- A opção MAXDOP foi adicionada a [DBCC CHECKTABLE &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checktable-transact-sql.md), [DBCC CHECKDB &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) e a [DBCC CHECKFILEGROUP &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md) para especificar o grau de paralelismo.
- Agora é possível definir SESSION_CONTEXT. Inclui as funções [SESSION_CONTEXT &#40;Transact-SQL&#41;](../t-sql/functions/session-context-transact-sql.md) e [CURRENT_TRANSACTION_ID &#40;Transact-SQL&#41;](../t-sql/functions/current-transaction-id-transact-sql.md), bem como o procedimento [sp_set_session_context &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md).
- As Extensões de Análise Avançada permitem que os usuários executem scripts escritos em uma linguagem com suporte, como o R. O [!INCLUDE[tsql](../includes/tsql-md.md)] dá suporte ao R introduzindo o procedimento armazenado [sp_execute_external_script &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) e a [Opção de Configuração de Servidor habilitada para scripts externos](../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md). Para obter mais informações, consulte [SQL Server R Services](../advanced-analytics/r-services/sql-server-r-services.md).
- Suporte adicional para R: a capacidade de criar um pool de recursos externos. Para obter mais informações, veja [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../t-sql/statements/create-external-resource-pool-transact-sql.md).  Novas exibições de catálogo e DMVs ([sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md) e [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)). Argumentos adicionais estão disponíveis para [sp_execute_external_script &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) e [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../t-sql/statements/create-workload-group-transact-sql.md). Colunas adicionais são adicionadas a algumas das DMVs e modos de exibição do catálogo do administrador de recursos existentes.
- A sintaxe [CREATE USER](../t-sql/statements/create-user-transact-sql.md) foi aprimorada com a opção ALLOW_ENCRYPTED_VALUE_MODIFICATIONS para dar suporte ao recurso Sempre Criptografado. Para obter mais informações, veja [Migrar dados confidenciais protegidos pelo Sempre Criptografado](../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md).
- As funções [COMPRESS &#40;Transact-SQL&#41;](../t-sql/functions/compress-transact-sql.md) e [DECOMPRESS &#40;Transact-SQL&#41;](../t-sql/functions/decompress-transact-sql.md) convertem valores no e do algoritmo GZIP.
- As funções [DATEDIFF_BIG &#40;Transact-SQL&#41;](../t-sql/functions/datediff-big-transact-sql.md) e [AT TIME ZONE &#40;Transact-SQL&#41;](../t-sql/queries/at-time-zone-transact-sql.md) e a exibição [sys.time_zone_info &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-time-zone-info-transact-sql.md) foram adicionadas para dar suporte a interações de data e hora.
- Uma credencial agora pode ser criada no nível do banco de dados (além da credencial de nível do servidor que estava disponível anteriormente). Para obter mais informações, veja [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../t-sql/statements/create-database-scoped-credential-transact-sql.md).
- Oito novas propriedades foram adicionadas a [SERVERPROPERTY &#40;Transact-SQL&#41;](../t-sql/functions/serverproperty-transact-sql.md): InstanceDefaultDataPath, InstanceDefaultLogPath, ProductBuild, ProductBuildType, ProductMajorVersion, ProductMinorVersion, ProductUpdateLevel e ProductUpdateReference.
- O limite de tamanho de entrada de 8.000 bytes para a função [HASHBYTES &#40;Transact-SQL&#41;](../t-sql/functions/hashbytes-transact-sql.md) foi removido.
- Novas funções de cadeia de caracteres [STRING_SPLIT &#40;Transact-SQL&#41;](../t-sql/functions/string-split-transact-sql.md) e [STRING_ESCAPE &#40;Transact-SQL&#41;](../t-sql/functions/string-escape-transact-sql.md) foram adicionadas.
- Opções de expansão automática: o sinalizador de rastreamento 1117 foi substituído pelas opções AUTOGROW_SINGLE_FILE e AUTOGROW_ALL_FILES de ALTER DATABASE, e o sinalizador de rastreamento 1117 passou a não ter nenhum efeito. Para obter mais informações, veja [Opções de arquivo e grupos de arquivos ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md) e a nova coluna is_autogrow_all_files de [sys.filegroups &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md).
- Alocação de extensões mistas: para bancos de dados do usuário, a alocação padrão para as 8 primeiras páginas de um objeto deixará de usar extensões de página mistas e passará a usar extensões uniformes. O sinalizador de rastreamento 1118 foi substituído pela opção SET MIXED_PAGE_ALLOCATION de ALTER DATABASE, e o sinalizador de rastreamento 1118 passou a não ter nenhum efeito. Para obter mais informações, veja [Opções de ALTER DATABASE SET &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-set-options.md) e a nova coluna `is_mixed_page_allocation_on` de [sys.databases &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-databases-transact-sql.md).


###  <a name="SystemTable"></a> Aprimoramentos do Modo de Exibição do Sistema
- Duas novas exibições dão suporte à segurança em nível de linha. Para obter mais informações, veja [sys.security_predicates &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md) e [sys.security_policies &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md).
- Sete novos modos de exibição dão suporte ao recurso Repositório de Consultas. Para obter mais informações, veja [Exibições de catálogo do repositório de consultas &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md).
- 24 novas colunas que fornecem informações sobre concessões de memória foram adicionadas ao [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md).
- Duas novas dicas de consulta (MIN_GRANT_PERCENT e MAX_GRANT_PERCENT) foram adicionadas para especificar concessões de memória. Veja [Dicas de consulta &#40;Transact-SQL&#41;](../t-sql/queries/hints-transact-sql-query.md).
- [sys.dm_exec_session_wait_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md) fornece um relatório por sessão semelhante a [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) de todo o servidor.
- [sys.dm_exec_function_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-function-stats-transact-sql.md) fornece estatísticas de execução sobre funções com valor escalar.
- A partir do [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], as entradas em [sys.dm_db_index_usage_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md) são mantidas como eram antes do [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)].
- Informações sobre instruções enviadas a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] podem ser retornadas pela nova função de gerenciamento dinâmico [sys.dm_exec_input_buffer &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md).
- Duas novas exibições dão suporte aos [Serviços do SQL Server R](../advanced-analytics/r-services/sql-server-r-services.md): [sys.dm_external_script_requests](../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) e [sys.dm_external_script_execution_stats](../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). 


###  <a name="Security"></a> Aprimoramentos de segurança

####  <a name="RLS"></a> Segurança em nível de linha
A segurança em nível de linha introduz o controle de acesso baseado em predicados. Ele apresenta uma avaliação centralizada, flexível e baseada em predicado que pode levar em consideração metadados (como rótulos) ou quaisquer outros critérios que o administrador determina conforme apropriado. O predicado é usado como critério para determinar se o usuário tem acesso apropriado aos dados com base em atributos de usuário. O controle de acesso baseado em rótulos pode ser implementado usando o controle de acesso baseado em predicados. Para obter mais informações, veja [Segurança em nível de linha](../relational-databases/security/row-level-security.md).


####  <a name="TCE"></a> Always Encrypted
Com o Sempre Criptografado, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode executar operações em dados criptografados e, o melhor de tudo, a chave de criptografia reside no aplicativo, no ambiente confiável do cliente e não no servidor. O Sempre Criptografado protege os dados do cliente para que DBAs não tenham acesso a dados de texto sem formatação. A criptografia e a descriptografia de dados ocorrem de modo transparente no nível do driver, minimizando as alterações que precisam ser feitas a aplicativos existentes. Para obter mais informações, consulte [Sempre Criptografado &#40;Mecanismo de Banco de Dados&#41;](../relational-databases/security/encryption/always-encrypted-database-engine.md).


####  <a name="Masking"></a> Máscara de Dados Dinâmicos
O mascaramento de dados dinâmicos limita a exposição de dados confidenciais mascarando-os para usuários sem privilégios. O mascaramento de dados dinâmicos ajuda a impedir o acesso não autorizado a dados confidenciais, permitindo que os clientes especifiquem a quantidade de dados confidenciais a revelar, com impacto mínimo sobre a camada de aplicativo. É um recurso de segurança baseado em políticas que oculta os dados confidenciais no conjunto de resultados de uma consulta em relação aos campos do banco de dados designados, sendo que os dados no banco de dados não são alterados. Para obter mais informações, consulte [Dynamic Data Masking](../relational-databases/security/dynamic-data-masking.md).


####  <a name="Perms"></a> Novas permissões
- A permissão **ALTER ANY SECURITY POLICY** está disponível como parte da implementação da segurança em nível de linha.
- As permissões **ALTER ANY MASK** e **UNMASK** estão disponíveis como parte da implementação do mascaramento de dados dinâmicos.
- As permissões **ALTER ANY COLUMN ENCRYPTION KEY**, **VIEW ANY COLUMN ENCRYPTION KEY**, **ALTER ANY COLUMN MASTER KEY DEFINITION**e **VIEW ANY COLUMN MASTER KEY DEFINITION** estão disponíveis como parte da implementação do recurso Sempre Criptografado.
- As permissões **ALTER ANY EXTERNAL DATA SOURCE** e **ALTER ANY EXTERNAL FILE FORMAT** são visíveis no [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] , mas se aplicam somente ao [!INCLUDE[ssAPS](../includes/ssaps-md.md)] ([!INCLUDE[ssDW](../includes/ssdw-md.md)]).
- As permissões **EXECUTE ANY EXTERNAL SCRIPT** estão disponíveis como parte do suporte para scripts do R.
 - As permissões **ALTER ANY DATABASE SCOPED CONFIGURATION** estão disponíveis para autorizar o uso da instrução [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).

####  <a name="TDE"></a> Transparent Data Encryption
- A Transparent Data Encryption foi aprimorada com suporte para aceleração de hardware Intel AES-NI da criptografia. Isso reduzirá a sobrecarga da CPU ao ativar a Transparent Data Encryption.

###  <a name="AES"></a> Criptografia AES para Pontos de Extremidade
- A criptografia padrão para os pontos de extremidade foi alterada de RC4 para AES.

####  <a name="newcredentialtype"></a> Novo Tipo de Credencial
- Uma credencial agora pode ser criada no nível do banco de dados (além da credencial de nível do servidor que estava disponível anteriormente). Para obter mais informações, veja [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../t-sql/statements/create-database-scoped-credential-transact-sql.md).


###  <a name="HighAvailability"></a> Aprimoramentos de Alta disponibilidade
O SQL Server 2016 Standard Edition agora dá suporte a Grupos de Disponibilidade Básicos AlwaysOn. Grupos de disponibilidade básicos dão suporte a uma réplica primária e secundária. Essa funcionalidade substitui a tecnologia obsoleta de Espelhamento de Banco de Dados para alta disponibilidade. Para obter mais informações sobre as diferenças entre grupos de disponibilidade básicos e avançados, veja [Grupos de disponibilidade básicos&#40;Grupos de disponibilidade AlwaysOn&#41;](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).

O balanceamento de carga das solicitações de conexão de intenção de leitura agora tem suporte em um conjunto de réplicas somente leitura. O comportamento anterior sempre direcionava conexões para a primeira réplica somente leitura disponível na lista de roteamento. Para obter mais informações, veja [Configurar o balanceamento de carga entre réplicas somente leitura](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md#loadbalancing).

 O número de réplicas que dão suporte a failover automático foi aumentado de duas para três.

 Contas de Serviço Gerenciado de Grupo agora têm suporte para Clusters de Failover do AlwaysOn. Para obter mais informações, consulte [Contas de Serviço Gerenciado de Grupo](https://technet.microsoft.com/library/hh831782.aspx). Para o Windows Server 2012 R2, é necessária uma atualização para evitar tempo de inatividade temporário após uma alteração de senha. Para obter a atualização, veja [serviços baseados em gMSA não podem fazer logon após uma alteração de senha em um domínio do Windows Server 2012 R2](https://support.microsoft.com/kb/2998082/).

 [!INCLUDE[ssHADR](../includes/sshadr-md.md)] dá suporte a transações distribuídas e ao DTC no Windows Server 2016. Para obter mais informações, veja [Suporte para transações distribuídas](../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md#dtcsupport).

 Agora você pode configurar [!INCLUDE[ssHADR](../includes/sshadr-md.md)] para realizar failover quando um banco de dados fica offline. Essa alteração exige a configuração da opção **DB_FAILOVER** para **ON** nas instruções [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/create-availability-group-transact-sql.md) ou [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/alter-availability-group-transact-sql.md).

O AlwaysOn agora dá suporte a bancos de dados criptografados. Os assistentes de grupo de disponibilidade agora solicitará uma senha para qualquer banco de dados contendo uma chave mestra de banco de dados quando você criar um novo Grupo de Disponibilidade ou quando você adicionar bancos de dados ou adicionar réplicas a um Grupo de Disponibilidade.

Dois grupos de disponibilidade em dois WSFCs (Clusters de Failover do Windows Server) separados agora podem ser combinados em um Grupo de Disponibilidade Distribuído. Para obter mais informações, veja [Grupos de disponibilidade distribuídos e &#40;Grupos de disponibilidade AlwaysOn&#41;](../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md).

A propagação direta permite que uma réplica secundária seja propagada automaticamente pela rede (em vez da propagação manual, que exige a restauração de um backup físico do banco de dados de destino na réplica secundária). A propagação direta é especificada pela configuração de **SEEDING_MODE=AUTOMATIC** na instrução [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/create-availability-group-transact-sql.md) ou [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/alter-availability-group-transact-sql.md). Também é necessário especificar **GRANT CREATE ANY DATABASE** com [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/alter-availability-group-transact-sql.md) em cada réplica secundária usada com a propagação direta.

**Melhorias no desempenho** – A taxa de transferência de sincronização dos grupos de disponibilidade foi aumentada em aproximadamente 10x por meio da compactação paralela e mais rápida dos blocos de log na réplica primária, um protocolo de sincronização otimizado e a descompactação paralela e a restauração dos registros de log na réplica secundária. Isso aumenta a atualização de secundários legíveis e reduz o tempo de recuperação de banco de dados no caso de failover. Observe que a restauração de tabelas com otimização de memória ainda não é paralela no SQL Server 2016.

###  <a name="Repl"></a> Aprimoramentos de Replicação
- Agora há suporte para a replicação de tabelas com otimização de memória. Para obter mais informações, veja [Replicação para assinantes de tabela com otimização de memória](../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md).
- Agora, no [!INCLUDE[ssSDSFull](../includes/sssdsfull-md.md)]há suporte para a replicação. Para obter mais informações, consulte [Replication to SQL Database](../relational-databases/replication/replication-to-sql-database.md).

###  <a name="Tools"></a> Aprimoramentos de ferramentas

####  <a name="SSMS"></a> Management Studio
Baixar o [SSMS (SQL Server Management Studio) mais recente](../ssms/download-sql-server-management-studio-ssms.md)

- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] dá suporte à ADAL (Active Directory Authentication Library), que está em desenvolvimento para conexão com o Microsoft Azure. Isso substitui a autenticação baseada em certificado, usada no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].
- A instalação[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] exige a instalação do .NET 4.6 como um pré-requisito. O .NET 4.6 será instalado automaticamente pela instalação quando o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] for instalado.
- Uma nova opção de grade de resultados da consulta dá suporte a manter o Retorno de Carro/Alimentação de Linha (caracteres de nova linha) ao copiar ou salvar o texto da grade de resultados. Defina-a no menu Ferramentas/Opções.
- O SQL Server Management Tools não é mais instalado por meio da árvore de recursos principal; para obter detalhes, veja [Instalar o SQL Server Management Tools com o SSMS](http://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381).
- A instalação[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] exige a instalação do .NET 4.6.1 como um pré-requisito. O .NET 4.6.1 será instalado automaticamente pela instalação quando o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] for instalado.

####  <a name="UA"></a> Supervisor de Atualização
O Supervisor de Atualização do SQL Server 2016 Preview é uma ferramenta autônoma que permite aos usuários de versões anteriores executar um conjunto de regras de atualização em seu banco de dados do SQL Server para identificar alterações de comportamento, alterações mais recentes e recursos preteridos, bem como fornecer ajuda com a adoção de novos recursos, como o Stretch Database.

 Você pode baixar o Supervisor de Atualização Preview [aqui](https://www.microsoft.com/en-us/download/details.aspx?id=48119) ou instalá-lo usando o Web Platform Installer.

## <a name="see-also"></a>Consulte Também
[Novidades no SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)
 
[Notas de Versão do SQL Server 2016.](../sql-server/sql-server-2016-release-notes.md) 
 
[Instalar as Ferramentas de Gerenciamento do SQL Server com SSMS](http://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381)








