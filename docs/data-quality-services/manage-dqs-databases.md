---
title: Gerenciar bancos de dados do DQS | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: data-quality-services
ms.reviewer: 
ms.suite: sql
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 655a67aa-d662-42f2-b982-c6217125ada8
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cda0e712bd4473972c1beb0afc6c530a6d48ef1c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="manage-dqs-databases"></a>Gerenciar bancos de dados do DQS
  Esta seção fornece informações sobre as atividades de gerenciamento de banco de dados que podem ser executadas nos bancos de dados DQS como backup/restauração ou anexar/desanexar.  
  
##  <a name="BackupRestore"></a> Backup e restauração dos bancos de dados do DQS  
 O backup e a restauração de bancos de dados do SQL Server são operações comuns que administradores de banco de dados executam para impedir a perda de dados em caso de desastre, recuperando dados dos bancos de dados de backup. O[!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] é implementado basicamente por dois bancos de dados do SQL Server: DQS_MAIN e DQS_PROJECTS. Os procedimentos de backup e restauração dos bancos de dados [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) são semelhante a qualquer outro banco de dados do SQL Server. Há três desafios associados com backup e restauração dos bancos de dados DQS:  
  
-   As operações de backup e restauração dos bancos de dados DQS devem estar sincronizadas. Caso contrário, o [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] restaurado não será funcional.  
  
-   Os dois bancos de dados, DQS, DQS_MAIN e DQS_PROJECTS, contêm assemblies e outros objetos complexos, além de apenas objetos de banco de dados simples (como tabelas e procedimentos armazenados).  
  
-   Há algumas entidades fora dos bancos de dados de DQS que devem existir para que os bancos de dados de DQS sejam funcionais como o [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)], especificamente os dois logons do SQL Server (##MS_dqs_db_owner_login ## e ##MS_dqs_service_login ##), e um procedimento armazenado de inicialização (DQInitDQS_MAIN) no banco de dados mestre.  
  
 Para obter informações detalhadas sobre backup e restauração no SQL Server, consulte [Fazer backup e restaurar bancos de dados do SQL Server](../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
### <a name="default-autogrowth-size-and-recovery-model-for-the-dqs-databases"></a>Tamanho de crescimento automático padrão e modelo de recuperação para bancos de dados DQS  
 Para impedir que os bancos de dados DQS e os logs de transação cresçam infinitamente e que potencialmente preencham o disco rígido:  
  
-   O tamanho **Aumento Automático** padrão dos bancos de dados DQS é definido para 10%.  
  
-   O modelo de recuperação padrão do banco de dados DQS é definido como **Simples**. No modelo de recuperação Simples, as transações são registradas minimamente, e o truncamento de log acontece automaticamente depois que a transação é concluída para liberar espaço no log de transação (arquivo .ldf). Para obter informações detalhadas sobre o modelo de recuperação simples, consulte [Backups completos de banco de dados &#40;SQL Server&#41;](../relational-databases/backup-restore/full-database-backups-sql-server.md).  
  
> [!IMPORTANT]  
>  -   No modelo de recuperação Simples, quando os registros de log permanecem ativos por muito tempo, (por exemplo, uma transação longa e demorada), o truncamento de log pode ser atrasado e, portanto, pode resultar no preenchimento do log de transação. Além disso, o truncamento do log não reduz o tamanho do arquivo de log físico (arquivo .ldf). Para reduzir o tamanho de um arquivo de log físico, você precisará reduzir o arquivo de log. Para obter informações sobre a solução de problemas do log de transações, consulte [O Log de transações &#40;SQL Server&#41;](../relational-databases/logs/the-transaction-log-sql-server.md) ou o artigo do Suporte da Microsoft em [http://go.microsoft.com/fwlink/?LinkId=237446](http://go.microsoft.com/fwlink/?LinkId=237446).  
> -   Você deve executar regularmente um backup completo ou diferencial dos bancos de dados DQS e deve fazer backup do log de transação assim como realizar a recuperação pontual de dados. Para obter mais informações, consulte [Backups completos de banco de dados &#40;SQL Server&#41;](../relational-databases/backup-restore/full-database-backups-sql-server.md) e [Fazer backup de um log de transações &#40;SQL Server&#41;](../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md).  
  
##  <a name="DetachAttach"></a> Anexar/desanexar bancos de dados DQS  
 Você pode desanexar os arquivos de dados e de log de transação dos bancos de dados DQS, e reanexá-los nos bancos de dados na mesma instância ou em outra do SQL Server se quiser alterar os bancos de dados DQS para uma instância diferente do SQL Server no mesmo computador ou para mover o banco de dados.  
  
 Para obter informações detalhadas sobre ideias a serem consideradas antes e durante a desanexação e anexação de bancos de dados no SQL Server, consulte [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../relational-databases/databases/database-detach-and-attach-sql-server.md).  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como fazer backup e restaurar os bancos de dados do DQS.|[Fazer backup e restaurar banco de dados do DQS](../data-quality-services/backing-up-and-restoring-dqs-databases.md)|  
|Descreve como desanexar e anexar bancos de dados DQS.|[Desanexar e anexar bancos de dados do DQS](../data-quality-services/detaching-and-attaching-dqs-databases.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Administração do DQS](../data-quality-services/dqs-administration.md)  
  
  
