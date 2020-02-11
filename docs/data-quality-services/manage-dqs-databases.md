---
title: Gerenciar bancos de dados do DQS
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 655a67aa-d662-42f2-b982-c6217125ada8
author: swinarko
ms.author: sawinark
ms.openlocfilehash: ce7b0239168a0a85e5d0f559b042dac0562ead94
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75246984"
---
# <a name="manage-dqs-databases"></a>Gerenciar bancos de dados do DQS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Esta seção fornece informações sobre as atividades de gerenciamento de banco de dados que podem ser executadas nos bancos de dados DQS como backup/restauração ou anexar/desanexar.  
  
##  <a name="BackupRestore"></a>Fazer backup e restaurar os bancos de dados do DQS  
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
>  -   No modelo de recuperação Simples, quando os registros de log permanecem ativos por muito tempo, (por exemplo, uma transação longa e demorada), o truncamento de log pode ser atrasado e, portanto, pode resultar no preenchimento do log de transação. Além disso, o truncamento do log não reduz o tamanho do arquivo de log físico (arquivo .ldf). Para reduzir o tamanho de um arquivo de log físico, você precisará reduzir o arquivo de log. Para obter informações sobre a solução de problemas do log de transações, consulte [O Log de transações &#40;SQL Server&#41;](../relational-databases/logs/the-transaction-log-sql-server.md) ou o artigo do Suporte da Microsoft em [https://go.microsoft.com/fwlink/?LinkId=237446](https://go.microsoft.com/fwlink/?LinkId=237446).  
> -   Você deve executar regularmente um backup completo ou diferencial dos bancos de dados DQS e deve fazer backup do log de transação assim como realizar a recuperação pontual de dados. Para obter mais informações, consulte [Backups completos de banco de dados &#40;SQL Server&#41;](../relational-databases/backup-restore/full-database-backups-sql-server.md) e [Fazer backup de um log de transações &#40;SQL Server&#41;](../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md).  
  
##  <a name="DetachAttach"></a>Desanexar/anexar os bancos de dados do DQS  
 Você pode desanexar os arquivos de dados e de log de transação dos bancos de dados DQS, e reanexá-los nos bancos de dados na mesma instância ou em outra do SQL Server se quiser alterar os bancos de dados DQS para uma instância diferente do SQL Server no mesmo computador ou para mover o banco de dados.  
  
 Para obter informações detalhadas sobre ideias a serem consideradas antes e durante a desanexação e anexação de bancos de dados no SQL Server, consulte [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../relational-databases/databases/database-detach-and-attach-sql-server.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como fazer backup e restaurar os bancos de dados do DQS.|[Fazendo backup e restaurando banco de dados do DQS](../data-quality-services/backing-up-and-restoring-dqs-databases.md)|  
|Descreve como desanexar e anexar bancos de dados DQS.|[Desanexando e anexando bancos de dados do DQS](../data-quality-services/detaching-and-attaching-dqs-databases.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [administração do dqs](../data-quality-services/dqs-administration.md)  
  
  
