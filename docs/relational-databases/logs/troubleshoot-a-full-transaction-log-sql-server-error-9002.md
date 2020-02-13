---
title: Solução do erro 9002 referente ao log de transações cheio
ms.custom: seo-lt-2019
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], full
- troubleshooting [SQL Server], full transaction log
- 9002 (Database Engine error)
- transaction logs [SQL Server], truncation
- backing up transaction logs [SQL Server], full logs
- transaction logs [SQL Server], full log
- full transaction logs [SQL Server]
ms.assetid: 0f23aa84-475d-40df-bed3-c923f8c1b520
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ad8b68338987256f1c7fa01f1f0d56242cef6a7f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "74056070"
---
# <a name="troubleshoot-a-full-transaction-log-sql-server-error-9002"></a>Solução de problemas em um log de transação completa (SQL Server Erro 9002)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico aborda as respostas possíveis a um log de transações completo e sugere como evitar isso no futuro. 
  
  Quando o log de transações fica completo, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] emite um **erro 9002**. O log pode ficar completo quando o banco de dados estiver online ou em recuperação. Se o log ficar cheio enquanto o banco de dados estiver online, o banco de dados permanecerá online, mas só poderá ser lido, não atualizado. Se o log ficar completo durante uma recuperação, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] marcará o banco de dados como RESOURCE PENDING. Em qualquer caso, é necessária a ação do usuário para liberar espaço no log.  
  
## <a name="responding-to-a-full-transaction-log"></a>Respondendo a um log de transações completo  
 A resposta apropriada a um log de transações completo depende em parte das condições que o fizeram ficar completo. 
 
 Para descobrir o que está impedindo o truncamento de log em um determinado caso, use as colunas **log_reuse_wait** e **log_reuse_wait_desc** da exibição de catálogo do **sys.database**. Para obter mais informações, veja [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md). Para descrições de fatores que podem adiar o truncamento de log, consulte [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
> **IMPORTANTE:**  
>  Se o banco de dados estava em recuperação quando o erro 9002 aconteceu, depois de resolver o problema, recupere o banco de dados usando [ALTER DATABASE *database_name* SET ONLINE.](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
 As alternativas para responder a um log de transações completo incluem:  
  
-   Fazer backup do log.  
  
-   Liberar espaço de disco para que o log possa crescer automaticamente.  
  
-   Mover o arquivo de log para uma unidade de disco com espaço suficiente.  
  
-   Aumentar o tamanho de um arquivo de log.  
  
-   Adicionar um arquivo de log a um disco diferente.  
  
-   Completar ou cancelar uma transação demorada.  
  
 Essas alternativas são discutidas nas seções seguintes. Escolha uma resposta que se ajuste melhor a sua situação.  
  
## <a name="back-up-the-log"></a>Fazer backup do log  
 No modelo de recuperação completa ou no modelo de recuperação bulk-logged, se não foi feito backup do log de transações recentemente, pode ser que o backup esteja impedindo o truncamento de log. Se nunca foi feito backup do log, **é necessário criar dois backups de log** para permitir que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] trunque o log no ponto do último backup. Truncar o log libera espaço para novos registros de log. Para impedir que o log fique completo novamente, faça backups de log frequentes.  
  
 **Para criar um backup de log de transações**  
  
> **IMPORTANTE**  
>  Se o banco de dados estiver danificado, consulte [Backups da parte final do Log &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
-   [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
### <a name="freeing-disk-space"></a>Liberando espaço em disco  
 Pode ser possível liberar espaço de disco na unidade de disco que contém o arquivo de log de transações do banco de dados excluindo ou movendo outros arquivos. O espaço de disco liberado permite que o sistema de recuperação aumente o arquivo de log automaticamente.  
  
### <a name="move-the-log-file-to-a-different-disk"></a>Mover o arquivo de log para um disco diferente  
 Se você não puder liberar espaço de disco suficiente na unidade que contém o arquivo de log, pense em mover o arquivo para outra unidade com espaço suficiente.  
  
> **IMPORTANTE:** Arquivos de log nunca devem ser colocados em sistemas de arquivos compactados.  
  
 **Mover um arquivo de log**  
  
-   [Mover arquivos de banco de dados](../../relational-databases/databases/move-database-files.md)  
  
### <a name="increase-log-file-size"></a>Aumentar o tamanho do arquivo de log  
 Se houver espaço disponível no disco de log, você pode aumentar o tamanho do arquivo de log. O tamanho máximo para arquivos de log é de dois terabytes (TB) por arquivo de log.  
  
 **Aumentar o tamanho de arquivo**  
  
 Se o aumento automático estiver desabilitado, o banco de dados estiver online e houver espaço suficiente disponível no disco, as ações possíveis serão:  
  
-   Aumentar manualmente o tamanho de arquivo para produzir um único incremento de crescimento.  
  
-   Ativar o crescimento automático usando a instrução ALTER DATABASE para definir um incremento de crescimento diferente de zero para a opção FILEGROWTH.  
  
> **OBSERVAÇÃO** Em qualquer caso, se o limite de tamanho atual tiver sido alcançado, aumente o valor MAXSIZE.  
  
### <a name="add-a-log-file-on-a-different-disk"></a>Adicionar um arquivo de log a um disco diferente  
 Adicione um arquivo de log novo ao banco de dados em um disco diferente que tenha espaço suficiente usando ALTER DATABASE <database_name> ADD LOG FILE.  
  
 **Adicionar um arquivo de log**  
  
-   [Adicionar arquivos de dados ou de log a um banco de dados](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)  
## <a name="complete-or-kill-a-long-running-transaction"></a>Concluir ou encerrar uma transação de longa duração
### <a name="discovering-long-running-transactions"></a>Descobrindo transações demoradas
Uma transação muito demorada pode fazer com que o log de transações fique cheio. Para procurar transações demoradas, use um dos seguintes:
 - **[sys.dm_tran_database_transactions](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md).**
Essa exibição de gerenciamento dinâmico retorna informações sobre as transações no banco de dados. Para uma transação demorada, as colunas de interesse específico incluem a hora do primeiro registro de log [(database_transaction_begin_time)](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md), o estado atual da transação [(database_transaction_state)](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)e o [LSN (número de sequência de log)](../backup-restore/recover-to-a-log-sequence-number-sql-server.md) do registro de início do log de transações [(database_transaction_begin_lsn)](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md).

 - **[DBCC OPENTRAN](../../t-sql/database-console-commands/dbcc-opentran-transact-sql.md).**
Essa instrução permite identificar a ID do proprietário da transação, de modo que seja possível localizar potencialmente a origem da transação para um término mais ordenado (confirmar, em vez de revertê-la).

### <a name="kill-a-transaction"></a>Encerrar uma transação
Às vezes, você precisa encerrar o processo. Talvez seja necessário usar a instrução [KILL](../../t-sql/language-elements/kill-transact-sql.md) . Use esta instrução com muito cuidado, especialmente quando processos críticos que você não deseja encerrar estiverem em execução. Para obter mais informações, consulte [KILL (Transact-SQL)](../../t-sql/language-elements/kill-transact-sql.md)

## <a name="see-also"></a>Confira também  
[Artigo de suporte da base de dados de conhecimento – um log de transações aumenta inesperadamente ou fica cheio no SQL Server](https://support.microsoft.com/kb/317375) [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Gerenciar o tamanho do arquivo de log de transações](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)   
 [Backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
 [sp_add_log_file_recover_suspect_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-file-recover-suspect-db-transact-sql.md)  
  
  
