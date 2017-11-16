---
title: "O log de transações (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 10/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-transaction-log
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transaction logs [SQL Server], about
- databases [SQL Server], transaction logs
- logs [SQL Server], transaction logs
ms.assetid: d7be5ac5-4c8e-4d0a-b114-939eb97dac4d
caps.latest.revision: "65"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 5c2b3a5bd97800d958c04bbc11a509d0db15cdc3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="the-transaction-log-sql-server"></a>O log de transações (SQL Server)
  Todo banco de dados do SQL Server tem um log de transações que registra todas as transações e as modificações feitas no banco de dados por cada transação.
  
O log de transações é um componente crítico do banco de dados. Se houver uma falha no sistema, você precisará que o log retorne o seu banco de dados a um estado consistente. 

> [!IMPORTANT] 
> Nunca exclua ou mova esse log, a menos que você compreenda totalmente as implicações de fazer isso. 

> [!TIP]
> Pontos bons conhecidos com base nos quais começar a aplicar logs de transação durante a recuperação de banco de dados são criados por pontos de verificação. Para obter mais informações, consulte [Pontos de verificação de banco de dados (SQL Server)](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
## <a name="operations-supported-by-the-transaction-log"></a>Operações com suporte pelo log de transações  
 O log de transações dá suporte às seguintes operações:  
  
-   Recuperação de transações individuais.  
  
-   Recuperação de todas as transações incompletas quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado.  
  
-   Rolando um banco de dados restaurado, arquivo, grupo de arquivo ou página até ao ponto de falha.  
  
-   Dando suporte à replicação transacional.  
  
-   Dando suporte a soluções de alta disponibilidade e recuperação de desastre: [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], espelhamento de banco de dados e envio de log.

## <a name="individual-transaction-recovery"></a>Recuperação de transações individuais
Se um aplicativo emitir uma instrução ROLLBACK, ou se o Mecanismo de Banco de Dados detectar um erro como a perda de comunicação com um cliente, o registro de log será usado para reverter as modificações feitas por uma transação incompleta. 

## <a name="recovery-of-all-incomplete-transactions-when-includessnoversionincludesssnoversion-mdmd-is-started"></a>Recuperação de todas as transações incompletas quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado
Se um servidor falhar, os bancos de dados poderão ser deixados em um estado em que algumas modificações nunca foram gravadas do cache de buffer para os arquivos de dados e poderá haver algumas modificações de transações incompletas nos arquivos de dados. Quando uma instância do SQL Server é iniciada, ele executa uma recuperação de cada banco de dados. Toda modificação registrada no log que não foi gravada nos arquivos de dados é efetuado roll forward. Toda transação incompleta encontrada no log de transações é revertida para assegurar que a integridade do banco de dados seja preservada. 

## <a name="rolling-a-restored-database-file-filegroup-or-page-forward-to-the-point-of-failure"></a>Efetuar roll forward em um banco de dados restaurado, um arquivo, grupo de arquivo ou em uma página até ao ponto de falha
Depois de uma perda de hardware ou falha de disco que afeta os arquivos de banco de dados, você pode restaurar o banco de dados ao ponto de falha. Você primeiro restaura o último backup de banco de dados e o último backup de banco de dados diferencial e, depois, restaura a sequência subsequente dos backups de log de transações ao ponto de falha. 

Ao restaurar cada backup de log, o Mecanismo de Banco de Dados reaplica todas as modificações registradas no log para efetuar roll forward todas as transações. Quando o último backup de log é restaurado, o Mecanismo de Banco de Dados usa as informações de log para reverter todas as transações que não estavam completas naquele ponto. 

## <a name="supporting-transactional-replication"></a>Dando suporte à replicação transacional
O Agente de Leitor de Log monitora o log de transações de cada banco de dados configurado para replicação transacional e copia as transações marcadas para replicação do log de transações no banco de dados de distribuição. Para obter mais informações, veja [Como funciona a replicação transacional](http://msdn.microsoft.com/library/ms151706.aspx).

## <a name="supporting-high-availability-and-disaster-recovery-solutions"></a>Suporte a soluções de recuperação de desastres e alta disponibilidade
As soluções do servidor em espera, grupos de disponibilidade Always On, espelhamento de banco de dados e envio de logs dependem muito do log de transações. 

Em um cenário de grupos de disponibilidade Sempre Ativo, cada atualização de um banco de dados, a réplica primária, é imediatamente reproduzida em cópias separadas e completas do banco de dados, as réplicas secundárias. A réplica primária envia imediatamente cada registro de log para as réplicas secundárias, que aplica os registros de log de entrada nos bancos de dados de grupo de disponibilidade, efetuando roll forward de forma contínua. Para obter mais informações, consulte [Instâncias do cluster de failover do AlwaysOn](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)

Em um cenário de envio de logs, o servidor primário envia o log de transações ativo do banco de dados primário a um ou mais destinos. Cada servidor secundário restaura o log a seu banco de dados secundário local. Para obter mais informações, consulte [Sobre o Envio de Logs](../../database-engine/log-shipping/about-log-shipping-sql-server.md). 

Em um cenário de espelhamento de banco de dados, em cada atualização de um banco de dados – o banco de dados principal – é imediatamente reproduzido em uma cópia separada, cópia do banco de dados completo, o banco de dados espelho. A instância do servidor principal envia imediatamente cada registro de log para a instância do servidor espelho, a qual aplica os registros de log de entrada ao banco de dados espelho, rolando adiante continuamente. Para obter mais informações, veja [Espelhamento de banco de dados](../../database-engine/database-mirroring/database-mirroring-sql-server.md).
  

##  <a name="Characteristics"></a>Transaction Log characteristics

Características do log de transações [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]: 
-  O log de transações é implementado como um arquivo separado ou conjunto de arquivos no banco de dados. O cache de log é gerenciado separadamente do cache de buffer para páginas de dados, o que resulta num código simples, rápido e robusto dentro do Mecanismo de Banco de Dados. Para obter mais informações, consulte [Arquitetura física de log de transações](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch).
-  O formato de registros de log e páginas não está restrito ao formato de páginas de dados.
-  O log de transações pode ser implementado em vários arquivos. Os arquivos podem ser definidos para expandir automaticamente definindo-se o valor FILEGROWTH como log. Isso reduz a possibilidade de realizar a execução fora de espaço no log de transações, e ao mesmo tempo reduz a sobrecarga administrativa. Para obter mais informações, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).
-  O mecanismo para reutilizar o espaço dentro dos arquivos de log é rápido e tem efeito mínimo em taxa de transferência de transações.

##  <a name="Truncation"></a> Truncamento do log de transações  
 O truncamento de log libera espaço no arquivo de log para ser reutilizado pelo log de transações. Você deve truncar regularmente o log de transações para impedir que ele preencha o espaço alocado (o que certamente ocorrerá). Vários fatores podem atrasar o truncamento de log, portanto, o monitoramento do tamanho do log é importante. Algumas operações podem ser registradas em log minimamente para reduzir o impacto no tamanho do log de transações.  
 
  O truncamento de log exclui arquivos de log virtuais inativos do log de transações lógicas de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , liberando espaço no log lógico para reutilização pelo log de transações físicas. Se um log de transações nunca for truncado, eventualmente, ele preencherá todo o espaço em disco alocado para seus arquivos de log físicos.  
  
 Para evitar a falta de espaço, a menos que o truncamento de log seja atrasado por alguma razão, o truncamento ocorrerá automaticamente depois dos seguintes eventos:  
  
-   No modelo de recuperação simples, depois de um ponto de verificação.  
  
-   No modelo de recuperação completa ou bulk-logged, se um ponto de verificação ocorreu desde o backup anterior, o truncamento ocorrerá depois de um backup de log (a menos que esse seja um backup de log de cópia somente).  
  
 Para obter mais informações, consulte [Fatores que podem atrasar o truncamento de log](#FactorsThatDelayTruncation), mais adiante neste tópico.  
  
> [!NOTE]
> O truncamento de log não reduz o tamanho do arquivo de log físico. Para reduzir o tamanho físico de um arquivo de log físico, você deve reduzir o arquivo de log. Para obter informações sobre como encolher o tamanho do arquivo de log físico, consulte [Manage the Size of the Transaction Log File](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md).  
  
##  <a name="FactorsThatDelayTruncation"></a> Factors that can delay log truncation  
 Quando os registros de log permanecem ativos por muito tempo, o truncamento do log de transações é atrasado e esse log poderá ocupar todo o espaço, como mencionado anteriormente nesse tópico.  
  
> [!IMPORTANT} Para obter informações sobre como responder a um log de transações completo, consulte [Solução de problemas de um log de transações completo &#40;Erro do SQL Server 9002&#41;](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md).  
  
 Na verdade, o truncamento de log pode ser atrasado por uma variedade de motivos. Descubra o que, se houver, está impedindo o truncamento de log consultando as colunas **log_reuse_wait** e **log_reuse_wait_desc** da exibição do catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md). A tabela a seguir descreve os valores dessas colunas.  
  
|Valor log_reuse_wait|Valor log_reuse_wait_desc|Descrição|  
|----------------------------|----------------------------------|-----------------|  
|0|NOTHING|Atualmente há um ou mais arquivos de log virtuais reutilizáveis.|  
|1|CHECKPOINT|Não aconteceu nenhum ponto de verificação desde o último truncamento de log, ou o início do log ainda não foi movido para fora de um arquivo de log virtual. (Todos os modelos de recuperação)<br /><br /> Essa é uma razão rotineira para atrasar o truncamento de log. Para obter mais informações, consulte [Database Checkpoints &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md).|  
|2|LOG_BACKUP|Um backup de log é necessário antes do truncamento do log de transações. (Modelos de recuperação completa e bulk-logged somente)<br /><br /> Quando o backup de log seguinte é concluído, parte do espaço do log poder se tornar reutilizável.|  
|3|ACTIVE_BACKUP_OR_RESTORE|Um backup de dados ou uma restauração está em andamento (todos os modelos de recuperação).<br /><br /> Se um backup de dados estiver evitando o truncamento de log, a operação de backup pode ajudar a solucionar o problema imediatamente.|  
|4|ACTIVE_TRANSACTION|Uma transação está ativa (todos os modelos de recuperação):<br /><br /> É possível haver uma transação de longa execução no início do backup de log. Nesse caso, a liberação de espaço pode exigir outro backup de log. Observe que transações demoradas impedem o truncamento de log em todos os modelos de recuperação, incluindo o modelo de recuperação simples, no qual o log de transações geralmente é truncado em cada ponto de verificação automático.<br /><br /> Uma transação é adiada. Uma *transação adiada* é efetivamente uma transação ativa cuja reversão é bloqueada por causa de algum recurso indisponível. Para obter informações sobre as causas de transações adiadas e como fazer com que elas saiam do estado adiado, consulte [Transações adiadas &#40;SQL Server&#41;](../../relational-databases/backup-restore/deferred-transactions-sql-server.md).<br /> <br /> Transações demoradas também podem preencher o log de transações do tempdb. Tempdb é usado implicitamente por transações de usuário para objetos internos, como tabelas de trabalho para classificação, arquivos de trabalho para hashing, tabelas de trabalho do cursor e a controle de versão de linha. Mesmo que a transação do usuário inclua dados como somente leitura (consultas `SELECT`), objetos internos podem ser criados e usados em transações de usuário. Dessa forma, o log de transações de tempdb pode ser preenchido.|  
|5|DATABASE_MIRRORING|O espelhamento de banco de dados está pausado, ou em um modo de alto desempenho, o banco de dados espelho fica significativamente atrás do banco de dados principal. (Apenas modelo de recuperação completa)<br /><br /> Para obter mais informações, consulte [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).|  
|6|REPLICATION|Durante as replicações transacionais, as transações relevantes para as publicações ainda não foram entregues no banco de dados de distribuição. (Apenas modelo de recuperação completa)<br /><br /> Para obter mais informações sobre a replicação transacional, consulte [SQL Server Replication](../../relational-databases/replication/sql-server-replication.md).|  
|7|DATABASE_SNAPSHOT_CREATION|Um instantâneo de banco de dados está sendo criado. (Todos os modelos de recuperação)<br /><br /> Esse é um motivo rotineiro e, normalmente breve, de truncamento de log atrasado.|  
|8|LOG_SCAN|Um exame de log está ocorrendo. (Todos os modelos de recuperação)<br /><br /> Esse é um motivo rotineiro e, normalmente breve, de truncamento de log atrasado.|  
|9|AVAILABILITY_REPLICA|Uma réplica secundária de um grupo de disponibilidade está aplicando registros de log de transações desse banco de dados para um banco de dados secundário correspondente. (Modelo de recuperação completa)<br /><br /> Para obter mais informações, consulte [Visão geral de grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).|  
|10|—|Somente para uso interno|  
|11|—|Somente para uso interno|  
|12|—|Somente para uso interno|  
|13|OLDEST_PAGE|Se um banco de dados estiver configurado para usar pontos de verificação indiretos, a página mais antiga no banco de dados poderá ser mais antiga do que o LSN do ponto de verificação. Nesse caso, a página mais antiga pode atrasar o truncamento de log. (Todos os modelos de recuperação)<br /><br /> Para obter informações sobre pontos de verificação indiretos, consulte [Database Checkpoints &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md).|  
|14|OTHER_TRANSIENT|Esse valor não é usado atualmente.|  
  
##  <a name="MinimallyLogged"></a> Operações que podem ser minimamente registradas em log  
 O*registro mínimo em log* envolve o registro somente das informações que são necessárias para recuperar a transação sem oferecer suporte à recuperação pontual. Este tópico identifica as operações com registro mínimo em log no [modelo de recuperação](../backup-restore/recovery-models-sql-server.md) bulk-logged (como também no modelo de recuperação simples, exceto quando há um backup em execução).  
  
> [!NOTE]
> O log mínimo não tem suporte para tabelas com otimização de memória.  
  
> [!NOTE]
> No [modelo de recuperação](../backup-restore/recovery-models-sql-server.md)completa, todas as operações em massa são completamente registradas. Porém, você pode minimizar o log de um conjunto de operações em massa alternando o banco de dados temporariamente para o modelo de recuperação bulk-logged, nas operações em massa. O registro mínimo em log é mais eficiente do que o registro completo, e reduz a possibilidade de que uma operação em massa em grande escala preencha o espaço do log de transações disponível durante uma transação em massa. Porém, se o banco de dados for danificado ou perdido quando o registro mínimo em log estiver em vigor, você não poderá recuperar o banco de dados até o ponto de falha.  
  
 As operações a seguir, completamente registradas sob o modelo de recuperação completa, têm log mínimo no modelo de recuperação simples e bulk-logged:  
  
-   Operações de importação em massa ([bcp](../../tools/bcp-utility.md), [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e [INSERT... SELECT](../../t-sql/statements/insert-transact-sql.md)). Para obter mais informações sobre quando a importação em massa para uma tabela é minimamente registrada em log, consulte [Prerequisites for Minimal Logging in Bulk Import](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
Quando a replicação transacional está habilitada, as operações BULK INSERT são completamente registradas mesmo no modelo de recuperação bulk-logged.  
  
-   Operações SELECT [INTO](../../t-sql/queries/select-into-clause-transact-sql.md) .  
  
Quando a replicação transacional está habilitada, as operações SELECT INTO são completamente registradas mesmo no modelo de recuperação bulk-logged.  
  
-   Atualizações parciais em tipos de dados de valor grande, usando a cláusula .WRITE na instrução [UPDATE](../../t-sql/queries/update-transact-sql.md) ao inserir ou anexar novos dados. Observe que o log mínimo não é usado quando valores existentes estão sendo atualizados. Para obter mais informações sobre tipos de dados de valor grandes, consulte [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).  
  
-   Instruções[WRITETEXT](../../t-sql/queries/writetext-transact-sql.md) e [UPDATETEXT](../../t-sql/queries/updatetext-transact-sql.md) ao inserir ou anexar novos dados em colunas de tipos de dados **text**, **ntext**, e **image** . Observe que o log mínimo não é usado quando valores existentes estão sendo atualizados.  
  
    > [!IMPORTANT]
    > As instruções WRITETEXT e UPDATETEXT são **preteridas**; evite usá-las em novos aplicativos.  
  
-   Se o banco de dados for definido como o modelo de recuperação simples ou bulk-logged, algumas operações INDEX DDL terão log mínimo, independentemente de elas serem executadas offline ou online. As operações de índice de log mínimo são:  
  
    -   Operações[CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) (incluindo exibições indexadas).  
  
    -   Operações[ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) REBUILD ou DBCC DBREINDEX.  
  
        > [!IMPORTANT]
        > A **instrução DBCC DBREINDEX** foi **preterida**. Não a use em novos aplicativos.  
  
    -   Recriação de novo heap DROP INDEX (se aplicável). (A desalocação de páginas de índice durante uma operação [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md) **sempre** é totalmente registrada em log.)
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Gerenciando o log de transações**  
  
-   [Gerenciar o tamanho do arquivo de log de transações](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)  
  
-   [Solução de problemas em um log de transação completa &#40;Erro do SQL Server 9002&#41;](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
 **Fazendo backup do log de transações (Modelo de recuperação completa)**  
  
-   [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
 **Restaurando o log de transações (Modelo de recuperação completa)**  
  
-   [Restaurar um backup de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
## <a name="more-information"></a>Mais informações!  
  [Guia de arquitetura e gerenciamento de log de transações do SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)   
 [Controlar a durabilidade da transação](../../relational-databases/logs/control-transaction-durability.md)   
 [Pré-requisitos para registro mínimo em log na importação em massa](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)   
 [Backup e Restauração de bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Pontos de verificação de banco de dados &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)   
 [Exibir ou alterar as propriedades de um banco de dados](../../relational-databases/databases/view-or-change-the-properties-of-a-database.md)   
 [Modelos de recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
  
