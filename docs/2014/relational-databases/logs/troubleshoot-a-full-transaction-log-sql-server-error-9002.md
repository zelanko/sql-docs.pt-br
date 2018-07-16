---
title: Solução de problemas em um log de transação completa (SQL Server Erro 9002) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
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
caps.latest.revision: 54
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0b3fa89db4f8fb95ca1f2e912c6ee1d131808f42
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37254028"
---
# <a name="troubleshoot-a-full-transaction-log-sql-server-error-9002"></a>Solução de problemas em um log de transação completa (SQL Server Erro 9002)
  Este tópico aborda as respostas possíveis a um log de transações completo e sugere como evitar isso no futuro. Quando o log de transações fica completo, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] emite um erro 9002. O log pode ficar completo quando o banco de dados estiver online ou em recuperação. Se o log ficar completo enquanto o banco de dados estiver online, o banco de dados permanecerá online, mas só poderá ser lido e não atualizado. Se o log ficar completo durante uma recuperação, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] marcará o banco de dados como RESOURCE PENDING. Em qualquer caso, é necessária a ação do usuário para liberar espaço no log.  
  
## <a name="responding-to-a-full-transaction-log"></a>Respondendo a um log de transações completo  
 A resposta apropriada a um log de transações completo depende em parte das condições que o fizeram ficar completo. Para descobrir o que está impedindo o truncamento de log em um determinado caso, use as colunas **log_reuse_wait** e **log_reuse_wait_desc** da exibição de catálogo do **sys.database**. Para obter mais informações, veja [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql). Para descrições de fatores que podem adiar o truncamento de log, consulte [O log de transações &#40;SQL Server&#41;](the-transaction-log-sql-server.md).  
  
> [!IMPORTANT]  
>  Se o banco de dados estava em recuperação quando o erro 9002 aconteceu, depois de resolver o problema, recupere o banco de dados usando ALTER DATABASE *database_name* SET ONLINE.  
  
 As alternativas para responder a um log de transações completo incluem:  
  
-   Fazer backup do log.  
  
-   Liberar espaço de disco para que o log possa crescer automaticamente.  
  
-   Mover o arquivo de log para uma unidade de disco com espaço suficiente.  
  
-   Aumentar o tamanho de um arquivo de log.  
  
-   Adicionar um arquivo de log a um disco diferente.  
  
-   Completar ou cancelar uma transação demorada.  
  
 Essas alternativas são discutidas nas seções seguintes. Escolha uma resposta que se ajuste melhor a sua situação.  
  
### <a name="backing-up-the-log"></a>Fazendo backup de log  
 No modelo de recuperação completa ou no modelo de recuperação bulk-logged, se não foi feito backup do log de transações recentemente, pode ser que o backup esteja impedindo o truncamento de log. Se nunca tiver sido feito backup do log, você deve criar dois backups de log a fim de permitir o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para truncar o log para o ponto do último backup. Truncar o log libera espaço para novos registros de log. Para impedir que o log fique completo novamente, faça backups de log frequentes.  
  
 **Para criar um backup de log de transações**  
  
> [!IMPORTANT]  
>  Se o banco de dados estiver danificado, consulte [Backups da parte final do Log &#40;SQL Server&#41;](../backup-restore/tail-log-backups-sql-server.md).  
  
-   [Fazer backup de um log de transações &#40;SQL Server&#41;](../backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
### <a name="freeing-disk-space"></a>Liberando espaço no disco  
 Pode ser possível liberar espaço de disco na unidade de disco que contém o arquivo de log de transações do banco de dados excluindo ou movendo outros arquivos. O espaço de disco liberado permite que o sistema de recuperação aumente o arquivo de log automaticamente.  
  
### <a name="moving-the-log-file-to-a-different-disk"></a>Movendo o arquivo de log para um disco diferente  
 Se você não puder liberar espaço de disco suficiente na unidade que contém o arquivo de log, pense em mover o arquivo para outra unidade com espaço suficiente.  
  
> [!IMPORTANT]  
>  Arquivos de log nunca devem ser colocados em sistemas de arquivos compactados.  
  
 **Para mover um arquivo de log**  
  
-   [Mover arquivos de banco de dados](../databases/move-database-files.md)  
  
### <a name="increasing-the-size-of-a-log-file"></a>Aumentando o tamanho de um arquivo de log  
 Se houver espaço disponível no disco de log, você pode aumentar o tamanho do arquivo de log. O tamanho máximo para arquivos de log é de dois terabytes (TB) por arquivo de log.  
  
 **Para aumentar o tamanho do arquivo**  
  
 Se o aumento automático estiver desabilitado, o banco de dados estiver online e houver espaço suficiente disponível no disco, as ações possíveis serão:  
  
-   Aumentar manualmente o tamanho de arquivo para produzir um único incremento de crescimento.  
  
-   Ativar o crescimento automático usando a instrução ALTER DATABASE para definir um incremento de crescimento diferente de zero para a opção FILEGROWTH.  
  
> [!NOTE]  
>  Em qualquer caso, se o limite de tamanho atual foi alcançado, aumente o valor MAXSIZE.  
  
### <a name="adding-a-log-file-on-a-different-disk"></a>Adicionando um arquivo de log a um disco diferente  
 Adicione um arquivo de log novo ao banco de dados em um disco diferente que tenha espaço suficiente usando ALTER DATABASE <database_name> ADD LOG FILE.  
  
 **Para adicionar um arquivo de log**  
  
-   [Adicionar arquivos de dados ou de log a um banco de dados](../databases/add-data-or-log-files-to-a-database.md)  
  
## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [Gerenciar o tamanho do arquivo de log de transações](manage-the-size-of-the-transaction-log-file.md)   
 [Backups de log de transações &#40;SQL Server&#41;](../backup-restore/transaction-log-backups-sql-server.md)   
 [sp_add_log_file_recover_suspect_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-log-file-recover-suspect-db-transact-sql)  
  
  
