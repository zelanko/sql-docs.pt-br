---
title: O log de transações (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- transaction logs [SQL Server], about
- databases [SQL Server], transaction logs
- logs [SQL Server], transaction logs
ms.assetid: d7be5ac5-4c8e-4d0a-b114-939eb97dac4d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1b4a175ad850ccbb0711a0997c3658cf01497686
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63144612"
---
# <a name="the-transaction-log-sql-server"></a>O log de transações (SQL Server)
  Todo banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem um log de transações que registra todas as transações e modificações feitas no banco de dados a cada transação. O log de transações deve ser truncado regularmente para impedir o preenchimento. No entanto, alguns fatores podem atrasar o truncamento de log e, portanto, o monitoramento do tamanho do log é importante. Algumas operações podem ser registradas em log minimamente para reduzir o impacto no tamanho do log de transações.  
  
 O log de transações é um componente crítico do banco de dados e, se houver uma falha do sistema, será necessário que o log de transações retorne seu banco de dados a um estado consistente. O log de transações nunca deve ser excluído ou movido a menos que você compreenda plenamente as consequências disso.  
  
> [!NOTE]  
>  Pontos bons conhecidos com base nos quais começar a aplicar logs de transação durante a recuperação de banco de dados são criados por pontos de verificação. Para obter mais informações, consulte [Pontos de verificação de banco de dados &#40;SQL Server&#41;](database-checkpoints-sql-server.md).  
  
 **Neste tópico:**  
  
-   [Benefícios: Operações com suporte pelo Log de transações](#Benefits)  
  
-   [Truncamento do log de transações](#Truncation)  
  
-   [Fatores que podem atrasar o truncamento de Log](#FactorsThatDelayTruncation)  
  
-   [Operações que podem ser minimamente registradas](#MinimallyLogged)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="Benefits"></a> Benefícios: Operações com suporte pelo Log de transações  
 O log de transações dá suporte às seguintes operações:  
  
-   Recuperação de transações individuais.  
  
-   Recuperação de todas as transações incompletas quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado.  
  
-   Rolando um banco de dados restaurado, arquivo, grupo de arquivo ou página até ao ponto de falha.  
  
-   Dando suporte à replicação transacional.  
  
-   Dando suporte a soluções de alta disponibilidade e recuperação de desastre: [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], espelhamento de banco de dados e envio de log.  
  
##  <a name="Truncation"></a> Truncamento do log de transações  
 O truncamento de log libera espaço no arquivo de log para ser reutilizado pelo log de transações. O truncamento de log é essencial para impedir o preenchimento do log. O truncamento de log exclui arquivos de log virtuais inativos do log de transações lógicas de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , liberando espaço no log lógico para reutilização pelo log de transações físicas. Se um log de transações nunca foi truncado, eventualmente, ele preencherá todo o espaço em disco alocado para seus arquivos de log físicos.  
  
 Para evitar esse problema, a menos que o truncamento de log esteja sendo atrasado por alguma razão, o truncamento ocorrerá automaticamente depois dos seguintes eventos:  
  
-   No modelo de recuperação simples, depois de um ponto de verificação.  
  
-   No modelo de recuperação completa ou bulk-logged, se um ponto de verificação ocorreu desde o backup anterior, o truncamento ocorrerá depois de um backup de log (a menos que esse seja um backup de log de cópia somente).  
  
 Para obter mais informações, consulte [Fatores que podem atrasar o truncamento de log](#FactorsThatDelayTruncation), mais adiante neste tópico.  
  
> [!NOTE]  
>  O truncamento de log não reduz o tamanho do arquivo de log físico. Para reduzir o tamanho físico de um arquivo de log físico, você precisa reduzir o arquivo de log. Para obter informações sobre como encolher o tamanho do arquivo de log físico, consulte [Gerenciar o tamanho do arquivo de log de transações](manage-the-size-of-the-transaction-log-file.md).  
  
##  <a name="FactorsThatDelayTruncation"></a> Fatores que podem atrasar o truncamento de Log  
 Quando os registros de log permanecem ativos por muito tempo, o truncamento do log de transações é atrasado e esse log poderá ocupar todo o espaço.  
  
> [!IMPORTANT]  
>  Para obter informações sobre como responder a um log de transação completa, consulte [Troubleshoot a Full Transaction Log &#40;SQL Server Error 9002&#41;](troubleshoot-a-full-transaction-log-sql-server-error-9002.md).  
  
 O truncamento de log pode ser atrasado por uma variedade de fatores. É possível descobrir se, de fato, há algo impedindo o truncamento de log consultando as colunas **log_reuse_wait** e **log_reuse_wait_desc** da exibição do catálogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) . A tabela a seguir descreve os valores dessas colunas.  
  
|Valor log_reuse_wait|Valor log_reuse_wait_desc|Descrição|  
|----------------------------|----------------------------------|-----------------|  
|0|NOTHING|Atualmente há um ou mais arquivos de log virtuais reutilizáveis.|  
|1|CHECKPOINT|Não aconteceu nenhum ponto de verificação desde o último truncamento de log, ou o início do log ainda não foi movido para fora de um arquivo de log virtual. (Todos os modelos de recuperação)<br /><br /> Essa é uma razão rotineira para atrasar o truncamento de log. Para obter mais informações, consulte [Database Checkpoints &#40;SQL Server&#41;](database-checkpoints-sql-server.md).|  
|2|LOG_BACKUP|Um backup de log é necessário antes do truncamento do log de transações. (Modelos de recuperação completa e bulk-logged somente)<br /><br /> Quando o backup de log seguinte é concluído, parte do espaço do log poder se tornar reutilizável.|  
|3|ACTIVE_BACKUP_OR_RESTORE|Um backup de dados ou uma restauração está em andamento (todos os modelos de recuperação).<br /><br /> Se um backup de dados estiver evitando o truncamento de log, a operação de backup pode ajudar a solucionar o problema imediatamente.|  
|4|ACTIVE_TRANSACTION|Uma transação está ativa (todos os modelos de recuperação).<br /><br /> É possível haver uma transação de longa execução no início do backup de log. Nesse caso, a liberação de espaço pode exigir outro backup de log. Observe que um transações demoradas impedem o truncamento de log em todos os modelos de recuperação, incluindo o modelo de recuperação simples, no qual o log de transações geralmente é truncado em cada ponto de verificação automático.<br /><br /> Uma transação é adiada. Uma *transação adiada* é efetivamente uma transação ativa cuja reversão é bloqueada por causa de algum recurso indisponível. Para obter informações sobre as causas de transações adiadas e como fazer com que elas saiam do estado adiado, consulte [Transações adiadas &#40;SQL Server&#41;](../backup-restore/deferred-transactions-sql-server.md). <br /><br />Transações demoradas também podem preencher o log de transações do tempdb. Tempdb é usado implicitamente por transações de usuário para objetos internos, como tabelas de trabalho para classificação, arquivos de trabalho para hashing, tabelas de trabalho do cursor e a controle de versão de linha. Mesmo que a transação de usuário inclui somente leitura de dados (consultas SELECT), objetos internos podem ser criados e usados em transações de usuário. Dessa forma, o log de transações de tempdb pode ser preenchido.|  
|5|DATABASE_MIRRORING|O espelhamento de banco de dados está pausado, ou em um modo de alto desempenho, o banco de dados espelho fica significativamente atrás do banco de dados principal. (Apenas modelo de recuperação completa)<br /><br /> Para obter mais informações, consulte [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).|  
|6|REPLICATION|Durante as replicações transacionais, as transações relevantes para as publicações ainda não foram entregues no banco de dados de distribuição. (Apenas modelo de recuperação completa)<br /><br /> Para obter mais informações sobre a replicação transacional, consulte [SQL Server Replication](../../relational-databases/replication/sql-server-replication.md).|  
|7|DATABASE_SNAPSHOT_CREATION|Um instantâneo de banco de dados está sendo criado. (Todos os modelos de recuperação)<br /><br /> Esse é um motivo rotineiro e, normalmente breve, de truncamento de log atrasado.|  
|8|LOG_SCAN|Um exame de log está ocorrendo. (Todos os modelos de recuperação)<br /><br /> Esse é um motivo rotineiro e, normalmente breve, de truncamento de log atrasado.|  
|9|AVAILABILITY_REPLICA|Uma réplica secundária de um grupo de disponibilidade está aplicando registros de log de transações desse banco de dados para um banco de dados secundário correspondente. (Modelo de recuperação completa)<br /><br /> Para obter mais informações, consulte [visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).|  
|10|-|Somente para uso interno|  
|11|-|Somente para uso interno|  
|12|-|Somente para uso interno|  
|13|OLDEST_PAGE|Se um banco de dados estiver configurado para usar pontos de verificação indiretos, a página mais antiga no banco de dados poderá ser mais antiga do que o LSN do ponto de verificação. Nesse caso, a página mais antiga pode atrasar o truncamento de log. (Todos os modelos de recuperação)<br /><br /> Para obter informações sobre pontos de verificação indiretos, consulte [Database Checkpoints &#40;SQL Server&#41;](database-checkpoints-sql-server.md).|  
|14|OTHER_TRANSIENT|Esse valor não é usado atualmente.|  
|16|XTP_CHECKPOINT|Quando um banco de dados tem um grupo de arquivos com otimização de memória, o log de transações não pode truncar até o ponto de verificação automático [!INCLUDE[hek_2](../../includes/hek-2-md.md)] ser acionado (o que acontece a cada 512 MB de aumento do log).<br /><br /> Observação: Para truncar o log de transações antes de 512 MB de tamanho, dispare o comando Checkpoint manualmente no banco de dados em questão.|  
  
##  <a name="MinimallyLogged"></a> Operações que podem ser minimamente registradas  
 O*registro mínimo em log* envolve o registro somente das informações que são necessárias para recuperar a transação sem oferecer suporte à recuperação pontual. Este tópico identifica as operações com registro mínimo em log no modelo de recuperação bulk-logged (como também no modelo de recuperação simples, exceto quando há um backup em execução).  
  
> [!NOTE]  
>  O log mínimo não tem suporte para tabelas com otimização de memória.  
  
> [!NOTE]  
>  No modelo de recuperação completa, todas as operações em massa são completamente registradas. Porém, você pode minimizar o log de um conjunto de operações em massa alternando o banco de dados temporariamente para o modelo de recuperação bulk-logged, nas operações em massa. O registro mínimo em log é mais eficiente do que o registro completo, e reduz a possibilidade de que uma operação em massa em grande escala preencha o espaço do log de transações disponível durante uma transação em massa. Porém, se o banco de dados for danificado ou perdido quando o registro mínimo em log estiver em vigor, você não poderá recuperar o banco de dados até o ponto de falha.  
  
 As operações a seguir, completamente registradas sob o modelo de recuperação completa, têm log mínimo no modelo de recuperação simples e bulk-logged:  
  
-   Operações de importação em massa ([bcp](../../tools/bcp-utility.md), [BULK INSERT](/sql/t-sql/statements/bulk-insert-transact-sql) e [INSERT... SELECT](/sql/t-sql/statements/insert-transact-sql)). Para obter mais informações sobre quando a importação em massa para uma tabela é minimamente registrada em log, consulte [Prerequisites for Minimal Logging in Bulk Import](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
    > [!NOTE]  
    >  Quando a replicação transacional está habilitada, as operações BULK INSERT são completamente registradas mesmo no modelo de recuperação bulk-logged.  
  
-   Operações SELECT [INTO](/sql/t-sql/queries/select-into-clause-transact-sql) .  
  
    > [!NOTE]  
    >  Quando a replicação transacional está habilitada, as operações SELECT INTO são completamente registradas mesmo no modelo de recuperação bulk-logged.  
  
-   Atualizações parciais em tipos de dados de valor grande, usando a cláusula .WRITE na instrução [UPDATE](/sql/t-sql/queries/update-transact-sql) ao inserir ou anexar novos dados. Observe que o log mínimo não é usado quando valores existentes estão sendo atualizados. Para obter mais informações sobre tipos de dados de valor grandes, consulte [Tipos de dados &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql).  
  
-   [WRITETEXT](/sql/t-sql/queries/writetext-transact-sql) e [UPDATETEXT](/sql/t-sql/queries/updatetext-transact-sql) ao inserir ou anexar novos dados para o `text`, `ntext`, e `image` colunas de tipo de dados. Observe que o log mínimo não é usado quando valores existentes estão sendo atualizados.  
  
    > [!NOTE]  
    >  As instruções WRITETEXT e UPDATETEXT são preteridas, portanto evite usá-las em novos aplicativos.  
  
-   Se o banco de dados for definido como o modelo de recuperação simples ou bulk-logged, algumas operações INDEX DDL terão log mínimo, independentemente de elas serem executadas offline ou online. As operações de índice de log mínimo são:  
  
    -   Operações[CREATE INDEX](/sql/t-sql/statements/create-index-transact-sql) (incluindo exibições indexadas).  
  
    -   Operações[ALTER INDEX](/sql/t-sql/statements/alter-index-transact-sql) REBUILD ou DBCC DBREINDEX.  
  
        > [!NOTE]  
        >  A instrução DBCC DBREINDEX é preterida, portanto evite usá-la em novos aplicativos.  
  
    -   Recriação de novo heap DROP INDEX (se aplicável).  
  
        > [!NOTE]  
        >  A desalocação de páginas de índice durante uma operação [DROP INDEX](/sql/t-sql/statements/drop-index-transact-sql) sempre é totalmente registrada em log.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 `Managing the transaction log`  
  
-   [Gerenciar o tamanho do arquivo de log de transações](manage-the-size-of-the-transaction-log-file.md)  
  
-   [Solução de problemas de um log de transação completa &#40;Erro do SQL Server 9002&#41;](troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
 **Fazendo backup do log de transações (Modelo de recuperação completa)**  
  
-   [Fazer backup de um log de transações &#40;SQL Server&#41;](../backup-restore/back-up-a-transaction-log-sql-server.md)  
  
 **Restaurando o log de transações (Modelo de recuperação completa)**  
  
-  [Restaurar um Backup de Log de transações](../backup-restore/restore-a-transaction-log-backup-sql-server.md)   
  
## <a name="see-also"></a>Consulte também  
 [Controlar a durabilidade da transação](control-transaction-durability.md)   
 [Pré-requisitos para registro mínimo em log na importação em massa](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md)   
 [Fazer backup e restaurar bancos de dados do SQL Server](../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Pontos de verificação de banco de dados &#40;SQL Server&#41;](database-checkpoints-sql-server.md)   
 [Exibir ou alterar as propriedades de um banco de dados](../databases/view-or-change-the-properties-of-a-database.md)   
 [Modelos de recuperação &#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md)  
  
  
