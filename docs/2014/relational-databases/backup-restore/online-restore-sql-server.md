---
title: Restauração online (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- online restores [SQL Server]
- online restores [SQL Server], about online restores
ms.assetid: 7982a687-980a-4eb8-8e9f-6894148e7d8c
caps.latest.revision: 43
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 47093fbf2be19ffcb8891c782df7fd6a72207b42
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009789"
---
# <a name="online-restore-sql-server"></a>Restauração online (SQL Server)
  Somente há suporte para a restauração online no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise edition. Nessa edição, um arquivo, uma página ou uma restauração por etapas está online por padrão. Este tópico é pertinente para bancos de dados que contêm vários arquivos ou grupos de arquivos (e, no modelo de recuperação simples, somente para grupos de arquivos somente leitura).  
  
 A restauração de dados enquanto o banco de dados está online é chamada *restauração online*. O banco de dados é considerado online sempre que o grupo de arquivos primário estiver online, até mesmo se um ou mais de seus grupos de arquivos secundários estiver offline. Em qualquer modelo de recuperação, você poderá restaurar um arquivo que estiver offline enquanto o banco de dados estiver online. No modelo de recuperação completa, você também poderá restaurar páginas enquanto o banco de dados estiver online.  
  
> [!NOTE]  
>  A restauração online acontece automaticamente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise e não requer nenhuma ação do usuário. Se você não quiser usar a restauração online, coloque um banco de dados offline antes de iniciar uma restauração Para obter mais informações, consulte [Colocando um banco de dados ou arquivo offline](#taking_db_or_file_offline), adiante neste tópico.  
  
 Durante uma restauração de arquivo online, qualquer arquivo que esteja sendo restaurado e seu grupo de arquivo ficarão offline. Se quaisquer desses arquivos estiver online quando uma restauração online for iniciada, a primeira instrução de restauração colocará o grupo de arquivos do arquivo offline. Por outro lado, durante uma restauração de página online, só a página fica offline.  
  
 Todo cenário de restauração online envolve as seguintes etapas básicas:  
  
1.  Restaurar os dados.  
  
2.  Restaurar o log usando WITH RECOVERY da última restauração de log. Isso coloca os dados restaurados online.  
  
 Ocasionalmente, uma transação não confirmada não pode ser revertida porque os dados necessários para a reversão estão offline durante a inicialização. Nesse caso, a transação é adiada. Para obter mais informações, veja [Transações adiadas &#40;SQL Server&#41;](deferred-transactions-sql-server.md).  
  
> [!NOTE]  
>  Se o banco de dados estiver usando o modelo de recuperação bulk-logged, recomendamos que você mude para o modelo de recuperação completa antes de iniciar uma restauração online. Para obter mais informações, veja [Exibir ou alterar o modelo de recuperação de um banco de dados &#40;SQL Server&#41;](view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
> [!IMPORTANT]  
>  Se os backups foram realizados com vários dispositivos que estavam anexados ao servidor, o mesmo número de dispositivos deverá estar disponível durante uma restauração online.  
  
## <a name="log-backups-for-online-restore"></a>Backups de log para restauração online  
 Em uma restauração online, o ponto de recuperação é o ponto quando os dados que estão sendo restaurados foram colocados offline ou como somente leitura pela última vez. Todos os backups de log de transações que levam a e incluem esse ponto de recuperação devem estar disponíveis Geralmente, um backup de log é necessário depois desse ponto para cobrir o ponto de recuperação para o arquivo. A única exceção é durante uma restauração online de dados somente leitura de um backup de dados realizado depois que os dados tornaram-se somente leitura. Nesse caso, você não precisa ter um backup de log.  
  
 Geralmente, você pode fazer backups de log de transações enquanto o banco de dados está online, até mesmo depois do início da sequência de restauração. O controle de tempo do último backup de log depende das propriedades do arquivo que estiver sendo restaurado:  
  
-   Para um arquivo somente leitura online, você pode fazer o último backup de log que é necessário para a recuperação, antes ou durante a primeira sequência de restauração. Um grupo de arquivos somente leitura pode não necessitar backups de log se um backup de dados ou diferencial tiver sido realizado depois que os grupos de arquivos tornaram-se somente leitura.  
  
    > [!NOTE]  
    >  A informações precedentes também são aplicadas a todos os arquivos offline.  
  
-   Existe um caso especial para um arquivo de leitura/gravação que estava online quando a primeira instrução de restauração foi emitida e automaticamente colocada offline por essa instrução de restauração. Nesse caso, faça um backup de log durante a primeira *sequência de restauração* (a sequência de uma ou mais instruções RESTORE que restauram, efetuam roll-forward e recuperam dados). Geralmente, esse backup de log deve ocorrer depois que você restaurar todos os backups completos e antes de recuperar os dados. Porém, se houver vários backups de arquivo para um grupo de arquivos específico, o ponto mínimo de backup de log será depois que o grupo de arquivos estiver offline. Esse backup de log após a restauração de dados captura o ponto em que o arquivo foi colocado offline. O backup de log após a restauração de dados é necessário porque o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] não podem usar log online para uma restauração online.  
  
    > [!NOTE]  
    >  Alternativamente, você pode colocar o arquivo offline manualmente antes da sequência de restauração. Para obter mais informações, consulte "Colocando um banco de dados ou arquivo offline", adiante neste tópico.  
  
##  <a name="taking_db_or_file_offline"></a> Colocando um banco de dados ou arquivo offline  
 Se você não quiser usar a restauração online, poderá colocar o banco de dados offline antes de iniciar a sequência de restauração usando um dos seguintes métodos:  
  
-   Em qualquer modelo de recuperação, você pode colocar o banco de dados offline usando a seguinte instrução [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) :  
  
     ALTER DATABASE *database_name* SET OFFLINE  
  
-   Alternativamente, no modelo de recuperação completa, você pode forçar uma restauração de arquivo ou página a ficar offline, usando a seguinte instrução [BACKUP LOG](/sql/t-sql/statements/backup-transact-sql) , colocando o banco de dados no estado de restauração:  
  
     BACKUP LOG *database_name* WITH NORECOVERY.  
  
 Desde que um banco de dados permaneça offline, todas as restaurações serão offline.  
  
## <a name="examples"></a>Exemplos  
  
> [!NOTE]  
>  A sintaxe para uma sequência de restauração online é igual à de uma sequência de restauração offline.  
  
-   [Exemplo: restauração por etapas de banco de dados &#40;Modelo de recuperação simples&#41;](example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Exemplo: restauração por etapas de apenas alguns grupos de arquivos &#40;Modelo de recuperação simples&#41;](example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo somente leitura &#40;Modelo de recuperação simples&#41;](example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Exemplo: restauração por etapas de banco de dados &#40;Modelo de recuperação completa&#41;](example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Exemplo: restauração por etapas de apenas alguns grupos de arquivos &#40;Modelo de recuperação completa&#41;](example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo de leitura/gravação #40;Modelo de recuperação completa&#41;](example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo somente leitura &#40;Modelo de recuperação completa&#41;](example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Restaurar arquivos e grupos de arquivos &#40;SQL Server&#41;](restore-files-and-filegroups-sql-server.md)  
  
-   [Restaurar páginas &#40;SQL Server&#41;](restore-pages-sql-server.md)  
  
-   [Gerenciar a tabela suspect_pages &#40;SQL Server&#41;](manage-the-suspect-pages-table-sql-server.md)  
  
-   [Recuperar um banco de dados sem restaurar dados &#40;Transact-SQL&#41;](recover-a-database-without-restoring-data-transact-sql.md)  
  
-   [Remover grupos de arquivos expirados &#40;SQL Server&#41;](remove-defunct-filegroups-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [Restaurações de arquivo &#40;Modelo de recuperação completa&#41;](file-restores-full-recovery-model.md)   
 [Restaurações de arquivos &#40;Modelo de recuperação simples&#41;](file-restores-simple-recovery-model.md)   
 [Restaurar páginas &#40;SQL Server&#41;](restore-pages-sql-server.md)   
 [Restaurações por etapas &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)   
 [Visão geral de restauração e recuperação &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)  
  
  
