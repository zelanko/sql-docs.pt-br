---
title: "Estratégias para fazer backup e restaurar o instantâneo e a replicação transacional | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backups [SQL Server replication], snapshot replication
- restoring [SQL Server replication], transactional replication
- snapshot replication [SQL Server], backup and restore
- restoring [SQL Server replication], snapshot replication
- recovery [SQL Server replication], transactional replication
- transactional replication, backup and restore
- recovery [SQL Server replication], snapshot replication
- sync with backup [SQL Server replication]
- backups [SQL Server replication], transactional replication
ms.assetid: a8afcdbc-55db-4916-a219-19454f561f9e
caps.latest.revision: "59"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 69c0da57bc8bf51162dcc26771726bf2e9f6091d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication"></a>Estratégias para fazer backup e restaurar o instantâneo e a replicação transacional
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Ao projetar uma estratégia de backup e restauração para instantâneo e replicação transacional, há três áreas a serem consideradas:  
  
-   Quais bancos de dados para fazer o backup.  
  
-   Configurações de backup para replicação transacional.  
  
-   As etapas que são exigidas para restaurar um banco de dados. Dependem do tipo de replicação e das opções escolhidas.  
  
 Este tópico abrange cada uma dessas áreas nas próximas três seções. Para obter informações sobre backup e restauração para publicação Oracle, consulte [Backup e restauração para Publicadores Oracle](../../../relational-databases/replication/non-sql/backup-and-restore-for-oracle-publishers.md).  
  
## <a name="backing-up-databases"></a>Fazendo backup de bancos de dados  
 Para instantâneo e replicação transacional, é necessário fazer o backup regularmente dos seguintes bancos de dados:  
  
-   O banco de dados de publicação no Publicador.  
  
-   O banco de dados de distribuição no Distribuidor.  
  
-   O banco de dados de assinatura em cada Assinante.  
  
-   Os bancos de dados de sistema **mestre** e **msdb** no Publicador, Distribuidor e todos os Assinantes. Esses bancos de dados devem ter, cada um, seus backups realizados em simultâneo com o banco de dados de replicação relevante. Por exemplo, faça o backup dos bancos de dados **mestre** e **msdb** no Publicador na mesma hora que faz o backup do banco de dados de publicação. Se o banco de dados de publicação for restaurado, certifique-–e de que os bancos de dados **mestre** e **msdb** são consistentes com o banco de dados de publicação com respeito à configuração de replicação e às configurações.  
  
 Se você executar backups de log regulares, qualquer alteração relacionada à replicação deverá ser capturada nos backups de log. Se não executar backups de log, um backup deve ser executado sempre que uma configuração pertinente à replicação for alterada. Para obter mais informações, consulte [Common Actions Requiring an Updated Backup](../../../relational-databases/replication/administration/common-actions-requiring-an-updated-backup.md).  
  
## <a name="backup-settings-for-transactional-replication"></a>Configurações de backup para replicação transacional  
 A replicação transacional inclui o uso da opção **sync with backup** que pode ser definida no banco de dados de distribuição e no banco de dados de publicação.  
  
-   Nós recomendamos essa opção seja sempre definida no banco de dados de distribuição.  
  
     Definir essa opção no banco de dados de distribuição assegura que as transações no log do banco de dados de publicação não serão truncadas até ser realizado o backup do banco de dados de distribuição. O banco de dados de distribuição pode ser restaurado ao último backup, e quaisquer transações perdidas são entregues do banco de dados de publicação ao banco de dados de distribuição. A replicação continua sem ser afetada.  
  
     Definir essa opção no banco de dados de distribuição não afeta a latência de replicação. Entretanto, a opção retardará o truncamento do log no banco de dados de publicação até ser realizado o backup das transações correspondentes no banco de dados de distribuição. (Isso pode criar um log de transação maior no banco de dados de publicação.)  
  
-   Nós recomendamos a definição dessa opção no banco de dados de publicação se seu aplicativo puder tolerar a latência adicional.  
  
     Definir essa opção no banco de dados de publicação assegura que as transações não serão entregues ao banco de dados de distribuição até ser realizado o backup do banco de dados de publicação. O último backup do banco de dados de publicação poderá, então, ser restaurado no Publicador sem qualquer chance do banco de dados de distribuição possuir transações que o banco de dados de publicação restaurado não possua.  
  
     A latência e a taxa de transferência serão afetadas porque as transações não poderão ser entregues ao banco de dados de distribuição até que o backup tenha sido feito no Publicador. Por exemplo, se o log de transações tem seu backup realizado a cada cinco minutos, haverá cinco minutos adicionais de latência quando a transação é confirmada no Publicador, e quando a transação é entregue ao banco de dados de distribuição e, subsequentemente, ao Assinante.  
  
    > [!NOTE]  
    >  A opção **sync with backup** assegura a consistência entre o banco de dados de publicação e banco de dados de distribuição, mas a opção não dá garantia contra perda de dados. Por exemplo, se o log de transações for perdido, as transações que foram confirmadas desde o último backup do log de transações não estarão disponíveis no banco de dados de publicação ou no banco de dados de distribuição. Esse é o mesmo comportamento de um banco de dados não replicado.  
  
 **Para definir a opção sync with backup**  
  
-   Programação [!INCLUDE[tsql](../../../includes/tsql-md.md)] de replicação: [Habilitar backups coordenados para a replicação transacional &#40;Programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md)  
  
## <a name="restoring-databases-involved-in-replication"></a>Restaurando bancos de dados envolvidos em replicação  
 É possível restaurar todos os bancos de dados em uma topologia de replicação se backups recentes estiverem disponíveis e as etapas adequadas forem seguidas. As etapas de restauração para o banco de dados de publicação dependem do tipo de replicação e das opções que foram usadas; entretanto, as etapas de restauração para todos os outros bancos de dados independem de tipo e opções.  
  
 A replicação oferece suporte à restauração de bancos de dados replicados para o mesmo servidor e banco de dados dos quais o backup foi criado. Se você restaurar um backup de um banco de dados replicado para outro servidor ou banco de dados, as configurações de replicação não poderão ser preservadas. Nesse caso, é necessário recriar todas as publicações e assinaturas depois que os backups forem restaurados.  
  
### <a name="publisher"></a>Publicador  
 Há etapas de restauração fornecidas para os seguintes tipos de replicação:  
  
-   Replicação de instantâneo  
  
-   Replicação transacional somente para leitura  
  
-   Replicação transacional com assinaturas de atualização  
  
-   Replicação transacional ponto a ponto  
  
 A restauração dos bancos de dados **msdb** e **mestre** , que também são tratados nesta seção, é a mesma para todos os quatro tipos.  
  
#### <a name="publication-database-snapshot-replication"></a>Banco de dados de publicação: replicação de instantâneo  
  
1.  Restaure o último backup de banco de dados do banco de dados de publicação. Vá para a etapa 2.  
  
2.  O backup do banco de dados de publicação contém a configuração mais recente de todas as publicações e assinaturas? Se a resposta for afirmativa, a restauração está concluída. Se não, vá para a etapa 3.  
  
3.  Remova a configuração de replicação do Publicador, Distribuidor e Assinantes e, em seguida, recrie a configuração. A restauração está concluída.  
  
     Para obter mais informações sobre como remover a replicação, consulte [sp_removedbreplication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
#### <a name="publication-database-read-only-transactional-replication"></a>Banco de dados de publicação: replicação transacional somente para leitura  
  
1.  Restaure o último backup de banco de dados do banco de dados de publicação. Vá para a etapa 2.  
  
2.  A configuração **sync with backup** foi habilitada no banco de dados de publicação antes da falha? Em caso afirmativo, vá para a etapa 3; caso contrário, vá para a etapa 5.  
  
     Se a configuração estiver habilitada, a consulta `SELECT DATABASEPROPERTYEX('<PublicationDatabaseName>', 'IsSyncWithBackup')` retornará ‘1'.  
  
3.  O backup restaurado está completo e atualizado? Ele contém a configuração mais recente para todas as publicações e assinaturas? Se a resposta for afirmativa, a restauração está concluída. Se não, vá para a etapa 4.  
  
4.  As informações de configuração no banco de dados de publicação restauradas não estão atualizadas. Consequentemente, é necessário certificar-se de que os Assinantes têm todos os comandos pendentes no banco de dados de distribuição e, então, descartar e recriar a configuração da replicação.  
  
    1.  Execute o Distribution Agent até que todos os Assinantes estejam sincronizados com os comandos pendentes no banco de dados de distribuição. Verifique se todos os comandos foram entregues aos Assinantes usando a guia **Comandos não Distribuídos** no Replication Monitor ou consultando a exibição [MSdistribuition_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) no banco de dados de distribuição. Vá para a etapa b.  
  
         Para obter mais informações sobre como executar um Agente de Distribuição, consulte [Iniciar e parar um agente de replicação &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [Conceitos dos executáveis do agente de replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
         Para obter mais informações sobre como verificar comandos, consulte [Exibir comandos replicados e outras informações no banco de dados de distribuição &#40;Programação do Transact-SQL de replicação&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md) e [Exibir informações e executar tarefas para os agentes associados a uma assinatura &#40;Replication Monitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
    2.  Remova a configuração de replicação do Publicador, Distribuidor e Assinantes e, em seguida, recrie a configuração. Ao recriar as assinaturas, especifique que o Assinante já tem os dados. A restauração está concluída.  
  
         Para obter mais informações sobre como remover a replicação, consulte [sp_removedbreplication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
         Para obter mais informações sobre como especificar que o Assinante já tem os dados, consulte [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
5.  A opção **sync with backup** não estava definida no banco de dados de publicação. Portanto, as transações que não foram incluídas no backup restaurado podem ter sido entregues ao Distribuidor e Assinantes. Agora, é necessário assegurar-se de que os Assinantes têm todos os comandos pendentes no banco de dados de distribuição e, em seguida, aplicar manualmente ao banco de dados de publicação quaisquer transações que não tenham sido incluídas no backup restaurado.  
  
    > [!IMPORTANT]  
    >  Realizar esse processo pode fazer com que tabelas publicadas sejam restauradas em um point-in-time que é mais recente que o point-in-time de outras tabelas não publicadas que foram restauradas a partir do backup.  
  
    1.  Execute o Distribution Agent até que todos os Assinantes estejam sincronizados com os comandos pendentes no banco de dados de distribuição. Verifique se todos os comandos foram entregues aos Assinantes usando a guia **Comandos não Distribuídos** no Replication Monitor ou consultando a exibição [MSdistribuition_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) no banco de dados de distribuição. Vá para a etapa b.  
  
         Para obter mais informações sobre como executar um Agente de Distribuição, consulte [Iniciar e parar um agente de replicação &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [Conceitos dos executáveis do agente de replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
         Para obter mais informações sobre como verificar comandos, consulte [Exibir comandos replicados e outras informações no banco de dados de distribuição &#40;Programação do Transact-SQL de replicação&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md) e [Exibir informações e executar tarefas para os agentes associados a uma assinatura &#40;Replication Monitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
    2.  Use o [tablediff utility](../../../tools/tablediff-utility.md) ou outra ferramenta para sincronizar manualmente o Publicador com o Assinante. Isso permitirá a recuperação dos dados do banco de dados de assinatura que não estavam contidos no backup de banco de dados de publicação. Vá para a etapa c.  
  
         Para mais informações sobre como usar o utilitário **tablediff**, consulte [Comparar diferenças de tabelas replicadas &#40;Programação de Replicação&#41;](../../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
    3.  O backup restaurado está completo e atualizado? Ele contém a configuração mais recente para todas as publicações e assinaturas? Se sim, execute o procedimento armazenado [sp_replrestart](../../../relational-databases/system-stored-procedures/sp-replrestart-transact-sql.md) para sincronizar novamente os metadados do Publicador com os metadados do Distribuidor. A restauração está concluída. Se não, vá para a etapa d.  
  
    4.  Remova a configuração de replicação do Publicador, Distribuidor e Assinantes e, em seguida, recrie a configuração. Ao recriar as assinaturas, especifique que o Assinante já tem os dados. A restauração está concluída.  
  
         Para obter mais informações sobre como remover a replicação, consulte [sp_removedbreplication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
         Para obter mais informações sobre como especificar que o Assinante já tem os dados, consulte [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
#### <a name="publication-database-transactional-replication-with-updating-subscriptions"></a>Banco de dados de publicação: Replicação transacional com assinaturas de atualização  
  
1.  Restaure o último backup de banco de dados do banco de dados de publicação. Vá para a etapa 2.  
  
2.  Execute o Distribution Agent até que todos os Assinantes estejam sincronizados com os comandos pendentes no banco de dados de distribuição. Verifique se todos os comandos foram entregues aos Assinantes usando a guia **Comandos não Distribuídos** no Replication Monitor ou consultando a exibição [MSdistribuition_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) no banco de dados de distribuição. Vá para a etapa 3.  
  
     Para obter mais informações sobre como executar um Agente de Distribuição, consulte [Iniciar e parar um agente de replicação &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [Conceitos dos executáveis do agente de replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
     Para obter mais informações sobre como verificar comandos, consulte [Exibir comandos replicados e outras informações no banco de dados de distribuição &#40;Programação do Transact-SQL de replicação&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md) e [Exibir informações e executar tarefas para os agentes associados a uma assinatura &#40;Replication Monitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
3.  Se você estiver usando assinaturas de atualização em fila, conecte a cada Assinante e exclua todas as linhas da tabela [MSreplication_queue &#40;Transact-SQL&#41;](../../../relational-databases/system-tables/msreplication-queue-transact-sql.md) no banco de dados de assinatura. Vá para a etapa 4.  
  
    > [!NOTE]  
    >  Se estiver usando assinaturas de atualização em fila e alguma tabela contiver colunas de identidade, é necessário assegurar-se de que os intervalos de identidade corretos serão atribuídos após a restauração. Para obter mais informações, consulte [Replicar colunas de identidade](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
4.  Agora, é necessário assegurar-se de que os Assinantes têm todos os comandos pendentes no banco de dados de distribuição e, em seguida, aplicar manualmente ao banco de dados de publicação quaisquer transações que não tenham sido incluídas no backup restaurado.  
  
    > [!IMPORTANT]  
    >  Realizar esse processo pode fazer com que tabelas publicadas sejam restauradas em um point-in-time que é mais recente que o point-in-time de outras tabelas não publicadas que foram restauradas a partir do backup.  
  
    1.  Execute o Distribution Agent até que todos os Assinantes estejam sincronizados com os comandos pendentes no banco de dados de distribuição. Verifique se todos os comandos foram entregues aos Assinantes usando o Replication Monitor ou consultando a exibição [MSdistribuition_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) no banco de dados de distribuição. Vá para a etapa b.  
  
    2.  Use o [tablediff Utility](../../../tools/tablediff-utility.md) ou outra ferramenta para sincronizar manualmente o Publicador com o Assinante. Isso permitirá a recuperação dos dados do banco de dados de assinatura que não estavam contidos no backup de banco de dados de publicação. Vá para a etapa c.  
  
         Para mais informações sobre como usar o utilitário **tablediff**, consulte [Comparar diferenças de tabelas replicadas &#40;Programação de Replicação&#41;](../../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
    3.  O backup restaurado está completo e atualizado? Ele contém a configuração mais recente para todas as publicações e assinaturas? Se sim, execute o procedimento armazenado [sp_replrestart](../../../relational-databases/system-stored-procedures/sp-replrestart-transact-sql.md) para sincronizar novamente os metadados do Publicador com os metadados do Distribuidor. A restauração está concluída. Se não, vá para a etapa d.  
  
    4.  Remova a configuração de replicação do Publicador, Distribuidor e Assinantes e, em seguida, recrie a configuração. Ao recriar as assinaturas, especifique que o Assinante já tem os dados. A restauração está concluída.  
  
         Para obter mais informações sobre como remover a replicação, consulte e [sp_removedbreplication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
         Para obter mais informações sobre como especificar que o Assinante já tem os dados, consulte [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
#### <a name="publication-database-peer-to-peer-transactional-replication"></a>Banco de dados de publicação: replicação transacional ponto a ponto  
 Nas etapas seguintes, os bancos de dados de publicação **A**, **B**e **C** estão em uma topologia de replicação transacional ponto a ponto. Os bancos de dados **A** e **C** estão online e funcionando corretamente; o banco de dados **B** é o banco de dados a ser restaurado. O processo aqui descrito, especialmente as etapas 7,10 e 11, são muito similares ao processo requerido para adicionar um nó a uma topologia ponto a ponto. O modo mais direto para executar essas etapas é por meio do Assistente para Configurar Topologia Ponto a Ponto, mas você também pode usar procedimentos armazenados.  
  
1.  Execute os Agentes de Distribuição para sincronizar as assinaturas nos bancos de dados **A** e **C**. Vá para a etapa 2.  
  
     Para obter mais informações sobre como executar um Agente de Distribuição, consulte [Iniciar e parar um agente de replicação &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [Conceitos dos executáveis do agente de replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
2.  Se o banco de dados de distribuição que **B** usa ainda estiver disponível, execute os Agentes de Distribuição para sincronizar as assinaturas entre os bancos de dados **B** e **A** e os bancos de dados B e **C**. Vá para a etapa 3.  
  
3.  Remova os metadados do banco de dados de distribuição que **B** usa executando [sp_removedistpublisherdbreplication](../../../relational-databases/system-stored-procedures/sp-removedistpublisherdbreplication-transact-sql.md) no banco de dados de distribuição para **B**. Vá para a etapa 4.  
  
4.  Nos bancos de dados **A** e **C**, remova as assinaturas para a publicação no banco de dados **B**. Vá para a etapa 5.  
  
     Para obter mais informações sobre como descartar assinaturas, consulte [Subscribe to Publications](../../../relational-databases/replication/subscribe-to-publications.md).  
  
5.  Execute um backup de log ou um backup de banco de dados completo do banco de dados **A**. Vá para a etapa 6.  
  
6.  Restaure o backup do banco de dados **A** no banco de dados **B**. O banco de dados **B** agora tem os dados do banco de dados **A**, mas não a configuração de replicação. Ao restaurar um backup em outro servidor, a replicação é removida, portanto a replicação foi removida do banco de dados **B**. Vá para a etapa 7.  
  
7.  Recrie a publicação no banco de dados **B** e, então, recrie as assinaturas entre os bancos de dados **A** e **B**. (Assinaturas que envolvem o banco de dados **C** serão tratadas mais tarde.).  
  
    1.  Recrie a publicação no banco de dados **B**. Vá para a etapa b.  
  
    2.  Recrie a assinatura no banco de dados **B** para a publicação no banco de dados **A**, especificando que a assinatura deverá ser inicializada com um backup (um valor de **inicializar a partir de um backup** para o parâmetro **@sync_type** de [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)). Vá para a etapa c.  
  
    3.  Recrie a assinatura no banco de dados **A** para a publicação no banco de dados **B**, especificando que o Assinante já tem os dados (um valor de **suporte para replicação somente** para o parâmetro **@sync_type** de [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)). Vá para a etapa 8.  
  
8.  Execute o Agente de Distribuição para sincronizar as assinaturas nos bancos de dados **A** e **B**. Se houver alguma coluna de identidade nas tabelas publicadas, vá para a etapa 9. Caso contrário, vá para a etapa 10.  
  
9. Após a restauração, o intervalo de identidade atribuído para cada tabela no banco de dados **A** será usado também no banco de dados **B**. Verifique se o banco de dados restaurado **B** recebeu todas as alterações do banco de dados que apresentou falha **B** que foram propagadas para o banco de dados **A** e o banco de dados **C**; e, então, propague novamente o intervalo de identidade para cada tabela.  
  
    1.  Execute [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) no banco de dados **B** e recupere o parâmetro de saída **@request_id**. Vá para a etapa b.  
  
    2.  Por padrão, o Distribution Agent está definido para executar continuamente; portanto, tokens devem ser enviados automaticamente a todos os nós. Se o Distribution Agent não estiver executando em modo contínuo, execute o agente. Para obter mais informações, consulte [Conceitos Executáveis do Agente de Replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) ou [Iniciar e Parar um Agente de Replicação &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md). Vá para a etapa c.  
  
    3.  Execute [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md), fornecendo o valor de **@request_id** recuperado na etapa b. Espere até que todos os nós indiquem ter recebido a solicitação par. Vá para a etapa d.  
  
    4.  Use [DBCC CHECKIDENT](../../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md) para propagar novamente cada tabela no banco de dados **B** para ter certeza de que um intervalo apropriado seja usado. Vá para a etapa 10.  
  
     Para obter mais informações sobre como administrar os intervalos de identidade, consulte a seção “Atribuindo intervalos para administração manual do intervalo de identidade” de [Replicar colunas de identidades](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
10. Nesse ponto, o banco de dados **B** e o banco de dados **C** não estão diretamente conectados, mas receberão as alterações através do banco de dados **A**. Se a topologia contiver qualquer nó que estiver executando o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], vá para a etapa 11; caso contrário, vá para a etapa 12.  
  
11. Confirme o sistema e, em seguida, recrie a assinatura entre os bancos de dados **B** e **C**. Confirmar um sistema envolve parar as atividades nas tabelas publicadas em todos os nós, e certificar-se de que todos os nós tenham recebido todas as alterações de todos os demais nós.  
  
    1.  Pare todas as atividades nas tabelas publicadas na topologia ponto a ponto. Vá para a etapa b.  
  
    2.  Execute [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) no banco de dados **B** e recupere o parâmetro de saída **@request_id**. Vá para a etapa c.  
  
    3.  Por padrão, o Distribution Agent está definido para executar continuamente; portanto, tokens devem ser enviados automaticamente a todos os nós. Se o Distribution Agent não estiver executando em modo contínuo, execute o agente. Vá para a etapa d.  
  
    4.  Execute [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md), fornecendo o valor de **@request_id** recuperado na etapa b. Espere até que todos os nós indiquem ter recebido a solicitação par. Vá para a etapa e.  
  
    5.  Recrie a assinatura no banco de dados **B** para a publicação no banco de dados **C**, especificando que o Assinante já possui os dados. Vá para a etapa b.  
  
    6.  Recrie a assinatura no banco de dados **C** para a publicação no banco de dados **B**, especificando que o Assinante já possui os dados. Vá para a etapa 13.  
  
12. Recrie a assinatura entre os bancos de dados **B** e **C**:  
  
    1.  No banco de dados **B**, consulte a tabela [MSpeer_lsns](../../../relational-databases/system-tables/mspeer-lsns-transact-sql.md) para recuperar o LSN (número de sequência de log) da mais recente transação que o banco de dados **B** recebeu do banco de dados **C**.  
  
    2.  Recrie a assinatura no banco de dados **B** para a publicação no banco de dados **C**, especificando que a assinatura deverá ser inicializada baseada no LSN (um valor de **inicializar a partir do lsn** para o parâmetro **@sync_type** de [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)). Vá para a etapa b.  
  
    3.  Recrie a assinatura no banco de dados **C** para a publicação no banco de dados **B**, especificando que o Assinante já possui os dados. Vá para a etapa 13.  
  
13. Execute os Distribution Agents para sincronizar as assinaturas nos bancos de dados **B** e **C**. A restauração está concluída.  
  
#### <a name="msdb-database-publisher"></a>Banco de dados msdb (Publicador)  
  
1.  Restaure o último backup do banco de dados **msdb** .  
  
2.  O backup restaurado está completo e atualizado? Ele contém a configuração mais recente para todas as publicações e assinaturas? Se sim, a recuperação está concluída. Se não, vá para a etapa 3.  
  
3.  Recrie o trabalho de limpeza de assinatura de seus scripts de replicação. A recuperação está concluída.  
  
#### <a name="master-database-publisher"></a>Banco de dados mestre (Publicador)  
  
1.  Restaure o último backup do banco de dados **mestre** .  
  
2.  Tenha certeza de que o banco de dados é consistente com o banco de dados de publicação com respeito a configuração de replicação e configurações.  
  
### <a name="databases-at-the-distributor"></a>Bancos de dados no Distribuidor  
  
#### <a name="distribution-database"></a>Banco de dados de distribuição  
  
1.  Restaure o último backup de banco de dados do banco de dados de distribuição.  
  
2.  A configuração **sync with backup** foi habilitada no banco de dados de distribuição antes da falha? Em caso afirmativo, vá para a etapa 3; se não, vá para a etapa 4.  
  
     Se a configuração estiver habilitada, a consulta `SELECT DATABASEPROPERTYEX('<DistributionDatabaseName>', 'IsSyncWithBackup')` retornará ‘1'.  
  
3.  O backup restaurado está completo e atualizado? Ele contém a configuração mais recente para todas as publicações e assinaturas? Se sim, a recuperação está concluída. Se não, vá para a etapa 4.  
  
4.  A informação de configuração do banco de dados de distribuição restaurado não está atualizada ou a opção **sync with backup** não foi definida no banco de dados de distribuição. (Após a restauração, o banco de dados de distribuição pode ter transações faltantes que foram confirmadas no Publicador, mas que ainda não foram entregues aos Assinantes). Remova e recrie a replicação. Depois, execute a validação.  
  
    1.  Remova a configuração de replicação do Publicador, Distribuidor e Assinantes e, em seguida, recrie a configuração. Ao recriar as assinaturas, especifique que o Assinante já tem os dados. Vá para a etapa b.  
  
         Para obter mais informações sobre como remover a replicação, consulte [sp_removedbreplication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
         Para obter mais informações sobre como especificar que o Assinante já tem os dados, consulte [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
    2.  Marque todas as publicações para validação. Reinicialize quaisquer assinaturas com falha de validação. A recuperação está concluída.  
  
         Para obter mais informações sobre validação, consulte [Validate Replicated Data](../../../relational-databases/replication/validate-replicated-data.md). Para mais informações sobre reinicialização, consulte [Reinicializar as assinaturas](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### <a name="msdb-database-distributor"></a>Banco de dados msdb (Distribuidor)  
  
1.  Restaure o último backup do banco de dados **msdb** .  
  
2.  O backup restaurado está completo e atualizado? Ele contém a configuração mais recente para todas as publicações e assinaturas? Se sim, a recuperação está concluída. Se não, vá para a etapa 3.  
  
3.  Remova a configuração de replicação do Publicador, Distribuidor e Assinantes e, em seguida, recrie a configuração. Ao recriar as assinaturas, especifique que o Assinante já tem os dados. Vá para a etapa 4.  
  
     Para obter mais informações sobre como remover a replicação, consulte [sp_removedbreplication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
     Para obter mais informações sobre como especificar que o Assinante já tem os dados, consulte [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
4.  Marque todas as publicações para validação. Reinicialize quaisquer assinaturas com falha de validação. A recuperação está concluída.  
  
     Para obter mais informações sobre validação, consulte [Validate Replicated Data](../../../relational-databases/replication/validate-replicated-data.md). Para mais informações sobre reinicialização, consulte [Reinicializar as assinaturas](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### <a name="master-database-distributor"></a>Banco de dados mestre (Distribuidor)  
  
1.  Restaure o último backup do banco de dados **mestre** .  
  
2.  Tenha certeza de que o banco de dados é consistente com o banco de dados de publicação com respeito a configuração de replicação e configurações.  
  
### <a name="databases-at-the-subscriber"></a>Bancos de dados no Assinante  
  
#### <a name="subscription-database"></a>Banco de dados de assinatura  
  
1.  É o último backup do banco de dados de assinaturas mais recente do que a configuração de retenção mínima de distribuição no banco de dados de distribuição? (Isso determina se o Distribuidor ainda tem todos os comandos que são exigidos para deixar o Assinante atualizado.) Se sim, vá para a etapa 2. Se não, reinicialize a assinatura. A recuperação está concluída.  
  
     Para determinar a configuração de máxima retenção de distribuição, execute [sp_helpdistributiondb](../../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md) e recupere o valor da coluna **max_distretention** (esse valor é em horas).  
  
     Para obter mais informações sobre como reinicializar uma assinatura, consulte [Reinitialize a Subscription](../../../relational-databases/replication/reinitialize-a-subscription.md).  
  
2.  Restaure o último backup de banco de dados de assinatura. Vá para a etapa 3.  
  
3.  Se o banco de dados de assinatura só contiver assinaturas push, vá para etapa 4. Se o banco de dados de assinatura contiver qualquer assinatura pull, faça as perguntas a seguir: As informações de assinatura são atuais? O banco de dados inclui todas as tabelas e opções que foram definidas na hora da falha? Se sim, vá para a etapa 4. Se não, reinicialize a assinatura. A recuperação está concluída.  
  
4.  Para sincronizar o Assinante, execute o Distribution Agent. A recuperação está concluída.  
  
     Para obter mais informações sobre como executar um Agente de Distribuição, consulte [Iniciar e parar um agente de replicação &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [Conceitos dos executáveis do agente de replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
#### <a name="msdb-database-subscriber"></a>Banco de dados msdb (Assinante)  
  
1.  Restaure o último backup do banco de dados **msdb** . São usadas assinaturas pull nesse Assinante? Se não, a restauração está concluída. Se sim, vá para a etapa 2.  
  
2.  O backup restaurado está completo e atualizado? Ele contém a configuração mais recente para todas as assinaturas pull? Se sim, a recuperação está concluída. Se não, vá para a etapa 3.  
  
3.  Descartar e recriar as assinaturas pull. Ao recriar as assinaturas, especifique que o Assinante já tem os dados. A restauração está concluída.  
  
     Para obter mais informações sobre como descartar assinaturas, consulte [Subscribe to Publications](../../../relational-databases/replication/subscribe-to-publications.md).  
  
     Para obter mais informações sobre como especificar que o Assinante já tem os dados, consulte [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
#### <a name="master-database-subscriber"></a>Banco de dados mestre (Assinante)  
  
1.  Restaure o último backup do banco de dados **mestre** .  
  
2.  Tenha certeza de que o banco de dados é consistente com o banco de dados de publicação com respeito a configuração de replicação e configurações.  
  
## <a name="see-also"></a>Consulte também  
 [Backup e Restauração de bancos de dados do SQL Server](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Fazer backup e restaurar bancos de dados replicados](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [Configurar Distribuição](../../../relational-databases/replication/configure-distribution.md)   
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Subscribe to Publications](../../../relational-databases/replication/subscribe-to-publications.md)   
 [Inicializar uma assinatura](../../../relational-databases/replication/initialize-a-subscription.md)   
 [Sincronizar dados](../../../relational-databases/replication/synchronize-data.md)  
  
  
