---
title: "Estrat&#233;gias para fazer backup e restaurar o instant&#226;neo e a replica&#231;&#227;o transacional | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "backups [replicação do SQL Server], replicação de instantâneo"
  - "restaurando [replicação do SQL Server], replicação transacional"
  - "replicação de instantâneo [SQL Server], backup e restauração"
  - "restaurando [replicação do SQL Server], replicação de instantâneo"
  - "recuperação [replicação do SQL Server], replicação transacional"
  - "replicação transacional, backup e restauração"
  - "recuperação [replicação do SQL Server], replicação de instantâneo"
  - "sync with backup [replicação do SQL Server]"
  - "backups [replicação do SQL Server], replicação transacional"
ms.assetid: a8afcdbc-55db-4916-a219-19454f561f9e
caps.latest.revision: 59
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 59
---
# Estrat&#233;gias para fazer backup e restaurar o instant&#226;neo e a replica&#231;&#227;o transacional
  Ao projetar uma estratégia de backup e restauração para instantâneo e replicação transacional, há três áreas a serem consideradas:  
  
-   Quais bancos de dados para fazer o backup.  
  
-   Configurações de backup para replicação transacional.  
  
-   As etapas que são exigidas para restaurar um banco de dados. Dependem do tipo de replicação e das opções escolhidas.  
  
 Este tópico abrange cada uma dessas áreas nas próximas três seções. Para obter informações sobre backup e restauração para a publicação Oracle, consulte [de Backup e restauração para Publicadores Oracle](../../../relational-databases/replication/non-sql/backup-and-restore-for-oracle-publishers.md).  
  
## Fazendo backup de bancos de dados  
 Para instantâneo e replicação transacional, é necessário fazer o backup regularmente dos seguintes bancos de dados:  
  
-   O banco de dados de publicação no Publicador.  
  
-   O banco de dados de distribuição no Distribuidor.  
  
-   O banco de dados de assinatura em cada Assinante.  
  
-   O **mestre** e **msdb** bancos de dados do sistema no publicador, distribuidor e todos os assinantes. Esses bancos de dados devem ter, cada um, seus backups realizados em simultâneo com o banco de dados de replicação relevante. Por exemplo, faça backup do **mestre** e **msdb** bancos de dados no publicador ao mesmo tempo em que você faz backup do banco de dados de publicação. Se o banco de dados de publicação for restaurado, verifique se o **mestre** e **msdb** bancos de dados são consistentes com o banco de dados relativas à configuração de replicação e as configurações de publicação.  
  
 Se você executar backups de log regulares, qualquer alteração relacionada à replicação deverá ser capturada nos backups de log. Se não executar backups de log, um backup deve ser executado sempre que uma configuração pertinente à replicação for alterada. Para obter mais informações, consulte [ações comuns que requerem um Backup atualizado](../../../relational-databases/replication/administration/common-actions-requiring-an-updated-backup.md).  
  
## Configurações de backup para replicação transacional  
 Usando a replicação transacional inclui o **sincronizar com backup** opção, que pode ser definida no banco de dados de distribuição e o banco de dados de publicação:  
  
-   Nós recomendamos essa opção seja sempre definida no banco de dados de distribuição.  
  
     Definir essa opção no banco de dados de distribuição assegura que as transações no log do banco de dados de publicação não serão truncadas até ser realizado o backup do banco de dados de distribuição. O banco de dados de distribuição pode ser restaurado ao último backup, e quaisquer transações perdidas são entregues do banco de dados de publicação ao banco de dados de distribuição. A replicação continua sem ser afetada.  
  
     Definir essa opção no banco de dados de distribuição não afeta a latência de replicação. Entretanto, a opção retardará o truncamento do log no banco de dados de publicação até ser realizado o backup das transações correspondentes no banco de dados de distribuição. (Isso pode criar um log de transação maior no banco de dados de publicação.)  
  
-   Nós recomendamos a definição dessa opção no banco de dados de publicação se seu aplicativo puder tolerar a latência adicional.  
  
     Definir essa opção no banco de dados de publicação assegura que as transações não serão entregues ao banco de dados de distribuição até ser realizado o backup do banco de dados de publicação. O último backup do banco de dados de publicação poderá, então, ser restaurado no Publicador sem qualquer chance do banco de dados de distribuição possuir transações que o banco de dados de publicação restaurado não possua.  
  
     A latência e a taxa de transferência serão afetadas porque as transações não poderão ser entregues ao banco de dados de distribuição até que o backup tenha sido feito no Publicador. Por exemplo, se o log de transações tem seu backup realizado a cada cinco minutos, haverá cinco minutos adicionais de latência quando a transação é confirmada no Publicador, e quando a transação é entregue ao banco de dados de distribuição e, subsequentemente, ao Assinante.  
  
    > [!NOTE]  
    >  O **sincronizar com backup** opção garante a consistência entre o banco de dados de publicação e o banco de dados de distribuição, mas a opção não oferece garantia contra perda de dados. Por exemplo, se o log de transações for perdido, as transações que foram confirmadas desde o último backup do log de transações não estarão disponíveis no banco de dados de publicação ou no banco de dados de distribuição.  Esse é o mesmo comportamento de um banco de dados não replicado.  
  
 **Para definir a opção sync with backup**  
  
-   Replicação [!INCLUDE[tsql](../../../includes/tsql-md.md)] programação: [Habilitar Backups coordenados para replicação transacional e 40; Programação Transact-SQL de replicação e 41;](../../../relational-databases/replication/administration/enable coordinated backups for transactional replication.md)  
  
## Restaurando bancos de dados envolvidos em replicação  
 É possível restaurar todos os bancos de dados em uma topologia de replicação se backups recentes estiverem disponíveis e as etapas adequadas forem seguidas. As etapas de restauração para o banco de dados de publicação dependem do tipo de replicação e das opções que foram usadas; entretanto, as etapas de restauração para todos os outros bancos de dados independem de tipo e opções.  
  
 A replicação oferece suporte à restauração de bancos de dados replicados para o mesmo servidor e banco de dados dos quais o backup foi criado. Se você restaurar um backup de um banco de dados replicado para outro servidor ou banco de dados, as configurações de replicação não poderão ser preservadas. Nesse caso, é necessário recriar todas as publicações e assinaturas depois que os backups forem restaurados.  
  
### Publicador  
 Há etapas de restauração fornecidas para os seguintes tipos de replicação:  
  
-   Replicação de instantâneo  
  
-   Replicação transacional somente para leitura  
  
-   Replicação transacional com assinaturas de atualização  
  
-   Replicação transacional ponto a ponto  
  
 A restauração do **msdb** e **mestre** bancos de dados, que também são abordados nesta seção, é o mesmo para todos os quatro tipos.  
  
#### Banco de dados de publicação: replicação de instantâneo   
  
1.  Restaure o último backup de banco de dados do banco de dados de publicação. Vá para a etapa 2.  
  
2.  O backup do banco de dados de publicação contém a configuração mais recente de todas as publicações e assinaturas? Se a resposta for afirmativa, a restauração está concluída. Se não, vá para a etapa 3.  
  
3.  Remova a configuração de replicação do Publicador, Distribuidor e Assinantes e, em seguida, recrie a configuração. A restauração está concluída.  
  
     Para obter mais informações sobre como remover a replicação, consulte [sp_removedbreplication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
#### Banco de dados de publicação: replicação transacional somente para leitura  
  
1.  Restaure o último backup de banco de dados do banco de dados de publicação. Vá para a etapa 2.  
  
2.  Foi o **sincronizar com backup** configuração habilitada no banco de dados de publicação antes da falha? Em caso afirmativo, vá para a etapa 3; caso contrário, vá para a etapa 5.  
  
     Se a configuração estiver habilitada, a consulta `SELECT DATABASEPROPERTYEX('<PublicationDatabaseName>', 'IsSyncWithBackup')` retornará ‘1'.  
  
3.  O backup restaurado está completo e atualizado? Ele contém a configuração mais recente para todas as publicações e assinaturas? Se a resposta for afirmativa, a restauração está concluída. Se não, vá para a etapa 4.  
  
4.  As informações de configuração no banco de dados de publicação restauradas não estão atualizadas. Consequentemente, é necessário certificar-se de que os Assinantes têm todos os comandos pendentes no banco de dados de distribuição e, então, descartar e recriar a configuração da replicação.  
  
    1.  Execute o Distribution Agent até que todos os Assinantes estejam sincronizados com os comandos pendentes no banco de dados de distribuição. Verifique se todos os comandos são entregues aos assinantes usando o **comandos não distribuídos** guia no Replication Monitor ou consultando o [Msdistribuition_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) exibição no banco de dados de distribuição. Vá para a etapa b.  
  
         Para obter mais informações sobre como executar o agente de distribuição, consulte [Iniciar e parar um agente de replicação e 40; SQL Server Management Studio e 41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [conceitos dos executáveis do Replication Agent](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
         Para obter mais informações sobre como verificar comandos, consulte [comandos replicados e outras informações no banco de dados de distribuição & #40. Programação Transact-SQL de replicação e 41;](../../../relational-databases/replication/monitor/view replicated commands and information in distribution database.md) e [Exibir informações e executar tarefas para os agentes associados com uma assinatura & #40. Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
    2.  Remova a configuração de replicação do Publicador, Distribuidor e Assinantes e, em seguida, recrie a configuração. Ao recriar as assinaturas, especifique que o Assinante já tem os dados. A restauração está concluída.  
  
         Para obter mais informações sobre como remover a replicação, consulte [sp_removedbreplication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
         Para obter mais informações sobre como especificar que o assinante já tem os dados, consulte [inicializar uma assinatura manualmente](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
5.  O **sincronizar com backup** opção não foi definida no banco de dados de publicação. Portanto, as transações que não foram incluídas no backup restaurado podem ter sido entregues ao Distribuidor e Assinantes. Agora, é necessário assegurar-se de que os Assinantes têm todos os comandos pendentes no banco de dados de distribuição e, em seguida, aplicar manualmente ao banco de dados de publicação quaisquer transações que não tenham sido incluídas no backup restaurado.  
  
    > [!IMPORTANT]  
    >  Realizar esse processo pode fazer com que tabelas publicadas sejam restauradas em um point-in-time que é mais recente que o point-in-time de outras tabelas não publicadas que foram restauradas a partir do backup.  
  
    1.  Execute o Distribution Agent até que todos os Assinantes estejam sincronizados com os comandos pendentes no banco de dados de distribuição. Verifique se todos os comandos são entregues aos assinantes usando o **comandos não distribuídos** guia no Replication Monitor ou consultando o [Msdistribuition_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) exibição no banco de dados de distribuição. Vá para a etapa b.  
  
         Para obter mais informações sobre como executar o agente de distribuição, consulte [Iniciar e parar um agente de replicação e 40; SQL Server Management Studio e 41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [conceitos dos executáveis do Replication Agent](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
         Para obter mais informações sobre como verificar comandos, consulte [comandos replicados e outras informações no banco de dados de distribuição & #40. Programação Transact-SQL de replicação e 41;](../../../relational-databases/replication/monitor/view replicated commands and information in distribution database.md) e [Exibir informações e executar tarefas para os agentes associados com uma assinatura & #40. Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
    2.  Use o [utilitário tablediff](../../../tools/tablediff-utility.md) ou outra ferramenta para sincronizar manualmente o publicador com o assinante. Isso permitirá a recuperação dos dados do banco de dados de assinatura que não estavam contidos no backup de banco de dados de publicação. Vá para a etapa c.  
  
         Para obter mais informações sobre o **tablediff** utilitário, consulte [Comparar tabelas replicadas para diferenças & #40. Programação de replicação e 41;](../../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
    3.  O backup restaurado está completo e atualizado? Ele contém a configuração mais recente para todas as publicações e assinaturas? Se Sim, execute o [sp_replrestart](../../../relational-databases/system-stored-procedures/sp-replrestart-transact-sql.md) procedimento armazenado para sincronizar novamente os metadados do publicador com os metadados do distribuidor. A restauração está concluída. Se não, vá para a etapa d.  
  
    4.  Remova a configuração de replicação do Publicador, Distribuidor e Assinantes e, em seguida, recrie a configuração. Ao recriar as assinaturas, especifique que o Assinante já tem os dados. A restauração está concluída.  
  
         Para obter mais informações sobre como remover a replicação, consulte [sp_removedbreplication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
         Para obter mais informações sobre como especificar que o assinante já tem os dados, consulte [inicializar uma assinatura manualmente](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
#### Banco de dados de publicação: Replicação transacional com assinaturas de atualização  
  
1.  Restaure o último backup de banco de dados do banco de dados de publicação. Vá para a etapa 2.  
  
2.  Execute o Distribution Agent até que todos os Assinantes estejam sincronizados com os comandos pendentes no banco de dados de distribuição. Verifique se todos os comandos são entregues aos assinantes usando o **comandos não distribuídos** guia no Replication Monitor ou consultando o [Msdistribuition_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) exibição no banco de dados de distribuição. Vá para a etapa 3.  
  
     Para obter mais informações sobre como executar o agente de distribuição, consulte [Iniciar e parar um agente de replicação e 40; SQL Server Management Studio e 41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [conceitos dos executáveis do Replication Agent](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
     Para obter mais informações sobre como verificar comandos, consulte [comandos replicados e outras informações no banco de dados de distribuição & #40. Programação Transact-SQL de replicação e 41;](../../../relational-databases/replication/monitor/view replicated commands and information in distribution database.md) e [Exibir informações e executar tarefas para os agentes associados com uma assinatura & #40. Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
3.  Se você estiver usando assinaturas de atualização na fila se conectar a cada assinante e excluir todas as linhas de [MSreplication_queue & #40. O Transact-SQL e 41;](../../../relational-databases/system-tables/msreplication-queue-transact-sql.md) tabela do banco de dados de assinatura. Vá para a etapa 4.  
  
    > [!NOTE]  
    >  Se estiver usando assinaturas de atualização em fila e alguma tabela contiver colunas de identidade, é necessário assegurar-se de que os intervalos de identidade corretos serão atribuídos após a restauração.  Para obter mais informações, consulte [replicar colunas de identidade](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
4.  Agora, é necessário assegurar-se de que os Assinantes têm todos os comandos pendentes no banco de dados de distribuição e, em seguida, aplicar manualmente ao banco de dados de publicação quaisquer transações que não tenham sido incluídas no backup restaurado.  
  
    > [!IMPORTANT]  
    >  Realizar esse processo pode fazer com que tabelas publicadas sejam restauradas em um point-in-time que é mais recente que o point-in-time de outras tabelas não publicadas que foram restauradas a partir do backup.  
  
    1.  Execute o Distribution Agent até que todos os Assinantes estejam sincronizados com os comandos pendentes no banco de dados de distribuição. Verifique se todos os comandos são entregues aos assinantes usando o Replication Monitor ou consultando o [Msdistribuition_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) exibição no banco de dados de distribuição. Vá para a etapa b.  
  
    2.  Use o [utilitário tablediff](../../../tools/tablediff-utility.md) ou outra ferramenta para sincronizar manualmente o publicador com o assinante. Isso permitirá a recuperação dos dados do banco de dados de assinatura que não estavam contidos no backup de banco de dados de publicação. Vá para a etapa c.  
  
         Para obter mais informações sobre o **tablediff** utilitário, consulte [Comparar tabelas replicadas para diferenças & #40. Programação de replicação e 41;](../../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
    3.  O backup restaurado está completo e atualizado? Ele contém a configuração mais recente para todas as publicações e assinaturas? Se Sim, execute o [sp_replrestart](../../../relational-databases/system-stored-procedures/sp-replrestart-transact-sql.md) procedimento armazenado para sincronizar novamente os metadados do publicador com os metadados do distribuidor. A restauração está concluída. Se não, vá para a etapa d.  
  
    4.  Remova a configuração de replicação do Publicador, Distribuidor e Assinantes e, em seguida, recrie a configuração. Ao recriar as assinaturas, especifique que o Assinante já tem os dados. A restauração está concluída.  
  
         Para obter mais informações sobre como remover a replicação, consulte e [sp_removedbreplication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
         Para obter mais informações sobre como especificar que o assinante já tem os dados, consulte [inicializar uma assinatura manualmente](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
#### Banco de dados de publicação: replicação transacional ponto a ponto  
 Nas etapas a seguir, bancos de dados de publicação **um**, **B**, e **C** estão em uma topologia de replicação transacional ponto a ponto. Bancos de dados **A** e **C** estão online e funcionando corretamente, banco de dados; **B** é o banco de dados a ser restaurado. O processo aqui descrito, especialmente as etapas 7,10 e 11, são muito similares ao processo requerido para adicionar um nó a uma topologia ponto a ponto. O modo mais direto para executar essas etapas é por meio do Assistente para Configurar Topologia Ponto a Ponto, mas você também pode usar procedimentos armazenados.  
  
1.  Execute o Distribution Agent para sincronizar as assinaturas nos bancos de dados **A** e **C**. Vá para a etapa 2.  
  
     Para obter mais informações sobre como executar o agente de distribuição, consulte [Iniciar e parar um agente de replicação e 40; SQL Server Management Studio e 41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [conceitos dos executáveis do Replication Agent](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
2.  Se a distribuição de banco de dados **B** usa ainda estiver disponível, execute os agentes de distribuição para sincronizar assinaturas entre bancos de dados **B** e **A** e bancos de dados e B e **C**. Vá para a etapa 3.  
  
3.  Remova os metadados da distribuição de banco de dados **B** usa executando [sp_removedistpublisherdbreplication](../../../relational-databases/system-stored-procedures/sp-removedistpublisherdbreplication-transact-sql.md) o banco de dados de distribuição de **B**. Vá para a etapa 4.  
  
4.  Nos bancos de dados **A** e **C**, descarte as assinaturas para a publicação no banco de dados **B**. Vá para a etapa 5.  
  
     Para obter mais informações sobre como descartar assinaturas, consulte [assinar publicações](../../../relational-databases/replication/subscribe-to-publications.md).  
  
5.  Executar um backup de log ou backup completo do banco de dados **A**. Vá para a etapa 6.  
  
6.  Restaure o backup do banco de dados **um** no banco de dados **B**. Banco de dados **B** agora tem os dados do banco de dados **um**, mas não a configuração de replicação. Quando você restaurar um backup para outro servidor, a replicação é removida; Portanto, a replicação foi removida do banco de dados **B**. Vá para a etapa 7.  
  
7.  Recrie a publicação no banco de dados **B**, e, em seguida, recrie as assinaturas entre bancos de dados **A** e **B**. (Assinaturas que envolvem o banco de dados **C** são manipulados em um estágio posterior.).  
  
    1.  Recrie a publicação no banco de dados **B**. Vá para a etapa b.  
  
    2.  Crie novamente a inscrição no banco de dados **B** para a publicação no banco de dados **um**, especificando que a assinatura deve ser inicializada com um backup (um valor de **inicializar com backup** para o **@sync_type** parâmetro do [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)). Vá para a etapa c.  
  
    3.  Crie novamente a inscrição no banco de dados **um** para a publicação no banco de dados **B**, especificando que o assinante já tem os dados (um valor de **suporte somente à replicação** para o **@sync_type** parâmetro do [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)). Vá para a etapa 8.  
  
8.  Execute o Distribution Agent para sincronizar as assinaturas nos bancos de dados **A** e **B**. Se houver alguma coluna de identidade nas tabelas publicadas, vá para a etapa 9. Caso contrário, vá para a etapa 10.  
  
9. Após a restauração, o intervalo de identidade que você atribuiu para cada tabela no banco de dados **um** será usado também no banco de dados **B**. Verifique se o banco de dados restaurado **B** recebeu todas as alterações do banco de dados com falha **B** que foram propagadas para o banco de dados **A** e banco de dados **C**; e propagar novamente o intervalo de identidade para cada tabela.  
  
    1.  Executar [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) no banco de dados **B** e recuperar o parâmetro de saída **@request_id**. Vá para a etapa b.  
  
    2.  Por padrão, o Distribution Agent está definido para executar continuamente; portanto, tokens devem ser enviados automaticamente a todos os nós. Se o Distribution Agent não estiver executando em modo contínuo, execute o agente. Para obter mais informações, consulte [conceitos dos executáveis do agente de replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) ou [Iniciar e parar um agente de replicação e 40; SQL Server Management Studio e 41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md). Vá para a etapa c.  
  
    3.  Executar [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md), fornecendo o **@request_id** valor recuperado na etapa b. Espere até que todos os nós indiquem ter recebido a solicitação par. Vá para a etapa d.  
  
    4.  Use [DBCC CHECKIDENT](../../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md) para propagar novamente cada tabela no banco de dados **B** para certificar-se de que um intervalo apropriado seja usado. Vá para a etapa 10.  
  
     Para obter mais informações sobre como gerenciar intervalos de identidade, consulte a seção "Atribuindo intervalos para gerenciamento de intervalo de identidade manual" [replicar colunas de identidade](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
10. Neste ponto, banco de dados **B** e banco de dados **C** não estão diretamente conectados, mas receberão as alterações por meio do banco de dados **A**. Se a topologia contiver qualquer nó que estiver executando o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], vá para a etapa 11; caso contrário, vá para a etapa 12.  
  
11. Confirme o sistema e, em seguida, recrie a assinatura entre bancos de dados **B** e **C**. Confirmar um sistema envolve parar as atividades nas tabelas publicadas em todos os nós, e certificar-se de que todos os nós tenham recebido todas as alterações de todos os demais nós.  
  
    1.  Pare todas as atividades nas tabelas publicadas na topologia ponto a ponto. Vá para a etapa b.  
  
    2.  Executar [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) no banco de dados **B** e recuperar o parâmetro de saída **@request_id**. Vá para a etapa c.  
  
    3.  Por padrão, o Distribution Agent está definido para executar continuamente; portanto, tokens devem ser enviados automaticamente a todos os nós. Se o Distribution Agent não estiver executando em modo contínuo, execute o agente. Vá para a etapa d.  
  
    4.  Executar [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md), fornecendo o **@request_id** valor recuperado na etapa b. Espere até que todos os nós indiquem ter recebido a solicitação par. Vá para a etapa e.  
  
    5.  Crie novamente a inscrição no banco de dados **B** para a publicação no banco de dados **C**, especificando que o assinante já tem os dados. Vá para a etapa b.  
  
    6.  Crie novamente a inscrição no banco de dados **C** para a publicação no banco de dados **B**, especificando que o assinante já tem os dados. Vá para a etapa 13.  
  
12. Recrie a assinatura entre bancos de dados **B** e **C**:  
  
    1.  No banco de dados **B**, consulta o [MSpeer_lsns](../../../relational-databases/system-tables/mspeer-lsns-transact-sql.md) tabela para recuperar o número de sequência de log (LSN) da transação mais recente desse banco de dados **B** recebeu do banco de dados **C**.  
  
    2.  Crie novamente a inscrição no banco de dados **B** para a publicação no banco de dados **C**, especificando que a assinatura deve ser inicializada com base no LSN (um valor de **inicializar do lsn** para o **@sync_type** parâmetro do [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)). Vá para a etapa b.  
  
    3.  Crie novamente a inscrição no banco de dados **C** para a publicação no banco de dados **B**, especificando que o assinante já tem os dados. Vá para a etapa 13.  
  
13. Execute o Distribution Agent para sincronizar as assinaturas nos bancos de dados **B** e **C**. A restauração está concluída.  
  
#### Banco de dados msdb (Publicador)  
  
1.  Restaure o backup mais recente do **msdb** banco de dados.  
  
2.  O backup restaurado está completo e atualizado? Ele contém a configuração mais recente para todas as publicações e assinaturas? Se sim, a recuperação está concluída. Se não, vá para a etapa 3.  
  
3.  Recrie o trabalho de limpeza de assinatura de seus scripts de replicação. A recuperação está concluída.  
  
#### Banco de dados mestre (Publicador)  
  
1.  Restaure o backup mais recente do **mestre** banco de dados.  
  
2.  Tenha certeza de que o banco de dados é consistente com o banco de dados de publicação com respeito a configuração de replicação e configurações.  
  
### Bancos de dados no Distribuidor  
  
#### Banco de dados de distribuição  
  
1.  Restaure o último backup de banco de dados do banco de dados de distribuição.  
  
2.  Foi o **sincronizar com backup** configuração habilitada no banco de dados de distribuição antes da falha? Em caso afirmativo, vá para a etapa 3; se não, vá para a etapa 4.  
  
     Se a configuração estiver habilitada, a consulta `SELECT DATABASEPROPERTYEX('<DistributionDatabaseName>', 'IsSyncWithBackup')` retornará ‘1'.  
  
3.  O backup restaurado está completo e atualizado? Ele contém a configuração mais recente para todas as publicações e assinaturas? Se sim, a recuperação está concluída. Se não, vá para a etapa 4.  
  
4.  As informações de configuração do banco de dados de distribuição restaurado não estão atualizadas, ou o **sincronizar com backup** opção não foi definida no banco de dados de distribuição. (Após a restauração, o banco de dados de distribuição pode ter transações faltantes que foram confirmadas no Publicador, mas que ainda não foram entregues aos Assinantes). Remova e recrie a replicação. Depois, execute a validação.  
  
    1.  Remova a configuração de replicação do Publicador, Distribuidor e Assinantes e, em seguida, recrie a configuração. Ao recriar as assinaturas, especifique que o Assinante já tem os dados. Vá para a etapa b.  
  
         Para obter mais informações sobre como remover a replicação, consulte [sp_removedbreplication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
         Para obter mais informações sobre como especificar que o assinante já tem os dados, consulte [inicializar uma assinatura manualmente](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
    2.  Marque todas as publicações para validação. Reinicialize quaisquer assinaturas com falha de validação. A recuperação está concluída.  
  
         Para obter mais informações sobre validação, consulte [Validar dados replicados](../../../relational-databases/replication/validate-replicated-data.md). Para obter mais informações sobre reinicialização, consulte [reinicializar assinaturas](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### Banco de dados msdb (Distribuidor)  
  
1.  Restaure o backup mais recente do **msdb** banco de dados.  
  
2.  O backup restaurado está completo e atualizado? Ele contém a configuração mais recente para todas as publicações e assinaturas? Se sim, a recuperação está concluída. Se não, vá para a etapa 3.  
  
3.  Remova a configuração de replicação do Publicador, Distribuidor e Assinantes e, em seguida, recrie a configuração. Ao recriar as assinaturas, especifique que o Assinante já tem os dados. Vá para a etapa 4.  
  
     Para obter mais informações sobre como remover a replicação, consulte [sp_removedbreplication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
     Para obter mais informações sobre como especificar que o assinante já tem os dados, consulte [inicializar uma assinatura manualmente](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
4.  Marque todas as publicações para validação. Reinicialize quaisquer assinaturas com falha de validação. A recuperação está concluída.  
  
     Para obter mais informações sobre validação, consulte [Validar dados replicados](../../../relational-databases/replication/validate-replicated-data.md). Para obter mais informações sobre reinicialização, consulte [reinicializar assinaturas](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### Banco de dados mestre (Distribuidor)  
  
1.  Restaure o backup mais recente do **mestre** banco de dados.  
  
2.  Tenha certeza de que o banco de dados é consistente com o banco de dados de publicação com respeito a configuração de replicação e configurações.  
  
### Bancos de dados no Assinante  
  
#### Banco de dados de assinatura  
  
1.  É o último backup do banco de dados de assinaturas mais recente do que a configuração de retenção mínima de distribuição no banco de dados de distribuição? (Isso determina se o Distribuidor ainda tem todos os comandos que são exigidos para deixar o Assinante atualizado.) Se sim, vá para a etapa 2. Se não, reinicialize a assinatura. A recuperação está concluída.  
  
     Para determinar a configuração de retenção máximo da distribuição, execute [sp_helpdistributiondb](../../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md) e recuperar o valor a partir de **max_distretention** coluna (esse valor é em horas).  
  
     Para obter mais informações sobre como reinicializar uma assinatura, consulte [reinicializar uma assinatura](../../../relational-databases/replication/reinitialize-a-subscription.md).  
  
2.  Restaure o último backup de banco de dados de assinatura. Vá para a etapa 3.  
  
3.  Se o banco de dados de assinatura só contiver assinaturas push, vá para etapa 4. Se o banco de dados de assinatura contiver qualquer assinatura pull, faça as perguntas a seguir: As informações de assinatura são atuais? O banco de dados inclui todas as tabelas e opções que foram definidas na hora da falha? Se sim, vá para a etapa 4. Se não, reinicialize a assinatura. A recuperação está concluída.  
  
4.  Para sincronizar o Assinante, execute o Distribution Agent. A recuperação está concluída.  
  
     Para obter mais informações sobre como executar o agente de distribuição, consulte [Iniciar e parar um agente de replicação e 40; SQL Server Management Studio e 41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [conceitos dos executáveis do Replication Agent](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
#### Banco de dados msdb (Assinante)  
  
1.  Restaure o backup mais recente do **msdb** banco de dados. São usadas assinaturas pull nesse Assinante? Se não, a restauração está concluída. Se sim, vá para a etapa 2.  
  
2.  O backup restaurado está completo e atualizado? Ele contém a configuração mais recente para todas as assinaturas pull? Se sim, a recuperação está concluída. Se não, vá para a etapa 3.  
  
3.  Descartar e recriar as assinaturas pull. Ao recriar as assinaturas, especifique que o Assinante já tem os dados. A restauração está concluída.  
  
     Para obter mais informações sobre como descartar assinaturas, consulte [assinar publicações](../../../relational-databases/replication/subscribe-to-publications.md).  
  
     Para obter mais informações sobre como especificar que o assinante já tem os dados, consulte [inicializar uma assinatura manualmente](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
#### Banco de dados mestre (Assinante)  
  
1.  Restaure o backup mais recente do **mestre** banco de dados.  
  
2.  Tenha certeza de que o banco de dados é consistente com o banco de dados de publicação com respeito a configuração de replicação e configurações.  
  
## Consulte também  
 [Fazer backup e restaurar bancos de dados do SQL Server](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Fazer backup e restaurar bancos de dados replicados](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [Configurar a distribuição](../../../relational-databases/replication/configure-distribution.md)   
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Assinar publicações](../../../relational-databases/replication/subscribe-to-publications.md)   
 [Inicializar uma assinatura](../../../relational-databases/replication/initialize-a-subscription.md)   
 [Sincronizar dados](../../../relational-databases/replication/synchronize-data.md)  
  
  