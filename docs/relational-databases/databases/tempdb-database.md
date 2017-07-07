---
title: Banco de dados tempdb | Microsoft Docs
ms.custom: 
ms.date: 03/04/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- temporary tables [SQL Server], tempdb database
- tempdb database [SQL Server], about tempdb
- temporary stored procedures [SQL Server]
- tempdb database [SQL Server]
ms.assetid: ce4053fb-e37a-4851-b711-8e504059a780
caps.latest.revision: 66
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 003196d8c30ca45c54750587c03c8d7d6e5a358d
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="tempdb-database"></a>Banco de dados tempdb
  O banco de dados do sistema **tempdb** é um recurso global disponível a todos os usuários conectados a uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e é usado para manter o seguinte:  
  
-   Os objetos de usuário temporários criados explicitamente como: tabelas temporárias globais ou locais, procedimentos armazenados temporários, variáveis de tabela ou cursores.  
  
-   Objetos internos criados por [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], por exemplo, tabelas de trabalho para armazenar resultados intermediários para spool ou classificação.  
  
-   Versões de linha geradas por transações de modificação de dados em um banco de dados que usa a leitura de confirmados usando transações de isolação de controle de versão de linha ou isolação de instantâneo.  
  
-   As versões de linhas geradas por meio de transações de modificação de dados para recursos como: operações de índice on-line, vários conjuntos de resultados ativos (MARS) e gatilhos AFTER.  
  
 As operações em **tempdb** são registradas minimamente. Isso permite que transações sejam revertidas. **tempdb** é recriado cada vez que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado, de modo que o sistema sempre começa com uma cópia limpa do banco de dados. As tabelas temporárias e procedimentos armazenados são descartados automaticamente ou desconectados e nenhuma conexão fica ativa quando o sistema é desligado. Portanto, nunca há nada em **tempdb** a ser gravado de uma sessão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para outra. As operações de backup e restauração não são permitidas em **tempdb**.  
  
## <a name="physical-properties-of-tempdb"></a>Propriedades físicas de tempdb  
 A tabela a seguir lista os valores iniciais de configuração dos dados **tempdb** e dos arquivos de log. Os tamanhos desses arquivos podem variar um pouco em diferentes edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Arquivo|Nome lógico|Nome físico|Tamanho inicial|Aumento do arquivo|  
|----------|------------------|-------------------|------------------|-----------------|  
|Dados primários|tempdev|tempdb.mdf|8 megabytes|Aumento automático de 64 MB até que o disco fique cheio|  
|Arquivos de dados secundários*|temp#|tempdb_mssql_#.ndf|8 megabytes|Aumento automático de 64 MB até que o disco fique cheio|  
|Log|templog|templog.ldf|8 megabytes|Aumento automático de 64 megabytes até um máximo de 2 terabytes|  
  
 \* O número de arquivos depende do número de núcleos (lógicos) no computador. O valor será o número de núcleos ou 8, o que for menor.   
O valor padrão para o número de arquivos de dados baseia-se nas diretrizes gerais de [KB 2154845](https://support.microsoft.com/en-us/kb/2154845/).  
  
## <a name="performance-improvements-in-tempdb"></a>Melhorias de desempenho em tempdb  
 Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **tempdb** o desempenho é aprimorado dos seguintes modos:  
  
-   As tabelas temporárias e variáveis de tabela podem ser colocadas em cache. O armazenamento em cache permite que as operações de descarte e criação de objetos temporários sejam executadas rapidamente e reduz a contenção de alocação de página.  
  
-   O protocolo de travamento da página de alocação é aprimorado. Isso reduz o número de travas de UP (atualização) usadas.  
  
-   A sobrecarga de logging para **tempdb** é reduzida. Isso reduz o consumo de largura de banda de E/S do disco no arquivo de log **tempdb** .  
  
-   A Instalação adiciona vários arquivos de dados tempdb durante uma nova instalação da instância. Essa tarefa pode ser realizada com o novo controle de entrada da interface do usuário na seção **Configuração do Mecanismo de Banco de Dados** e em um parâmetro de linha de comando /SQLTEMPDBFILECOUNT. Por padrão, a instalação adicionará um número de arquivos tempdb equivalente à contagem de CPU ou a 8, o que for menor.  
  
-   Quando houver vários arquivos de dados **tempdb** , todos os arquivos aumentarão automaticamente e na mesma quantidade, dependendo das configurações de aumento.  O sinalizador de rastreamento 1117 já não é necessário.  
  
-   Além disso, todas as alocações em **tempdb** usam extensões uniformes. O sinalizador de rastreamento 1118 não é mais necessário.  
  
-   Para o grupo de arquivos primário, a propriedade AUTOGROW_ALL_FILES está ativada e não pode ser modificada.  
  
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
  
-   Adição de grupos de arquivos  
  
-   Backup ou restauração de banco de dados.  
  
-   Alteração de agrupamento. O agrupamento padrão é o agrupamento de servidor.  
  
-   Alteração do proprietário do banco de dados. **tempdb** pertence a **sa**.  
  
-   Criação de um instantâneo do banco de dados  
  
-   Descartando o banco de dados.  
  
-   Descartando o usuário **convidado** do banco de dados.  
  
-   Habilitação do Change Data Capture.  
  
-   Participação no espelhamento de banco de dados.  
  
-   Remoção do grupo de arquivos primário, arquivo de dados primário ou arquivo de log.  
  
-   Renomeação do banco de dados ou grupo de arquivos primário.  
  
-   Execução de DBCC CHECKALLOC.  
  
-   Execução de DBCC CHECKCATALOG.  
  
-   Definindo o banco de dados como OFFLINE.  
  
-   Definindo o banco de dados ou grupo de arquivos primário como READ_ONLY.  
  
## <a name="permissions"></a>Permissões  
 Qualquer usuário pode criar objetos temporários no tempdb. Os usuários podem acessar somente seus próprios objetos, a menos que recebam permissões adicionais. É possível revogar a permissão de conexão ao tempdb para impedir um usuário de usar tempdb, mas isto não é recomendado porque algumas operações rotineiras exigem o uso de tempdb.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Opção SORT_IN_TEMPDB para índices](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)  
  
 [Bancos de dados do sistema](../../relational-databases/databases/system-databases.md)  
  
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
 [Mover arquivos de banco de dados](../../relational-databases/databases/move-database-files.md)  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com tempdb no SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=81216)  
  
  

