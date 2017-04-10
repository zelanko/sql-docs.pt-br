---
title: "Especificar agendas de sincroniza&#231;&#227;o | Microsoft Docs"
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
  - "subscriptions [SQL Server replication], synchronizing"
  - "scheduling synchronization [SQL Server replication]"
  - "synchronization [SQL Server replication], schedules"
  - "replicação [replicação do SQL Server], sincronização"
ms.assetid: 97f2535b-ec19-4973-823d-bcf3d5aa0216
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# Especificar agendas de sincroniza&#231;&#227;o
  Este tópico descreve como especificar agendas de sincronização no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)] ou o RMO (Replication Management Objects). Quando criar uma assinatura, você pode definir uma agenda de sincronização que controla quando o agente de replicação para a assinatura executará. Se você não especificar os parâmetros de programação, a assinatura usará a agenda padrão.  
  
 Assinaturas são sincronizadas pelo Agente de Distribuição (para replicação transacional e de instantâneo) ou pelo Agente de Mesclagem (para replicação de mesclagem). Os agentes podem ser executados continuamente, sob demanda ou em um agendamento.  
  
 **Neste tópico**  
  
-   **Para especificar agendas de sincronização, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Especifique agendas de sincronização na página **Agenda de Sincronização** do Assistente para Nova Assinatura. Para mais informações sobre como acessar esse assistente, consulte [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md) e [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
 Modifique agendas de sincronização na caixa de diálogo **Propriedades da Agenda de Trabalho** , que se encontra disponível na pasta **Trabalhos** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e nas janelas de detalhes do agente no Replication Monitor. Para obter informações sobre como iniciar o Monitor de replicação, consulte [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
 Se você especificar agendas da pasta **Jobs** use a tabela a seguir para determinar o nome do trabalho do agente.  
  
|Agente|Nome do trabalho|  
|-----------|--------------|  
|Merge Agent para assinaturas pull|**\< publicador>-\< Banco_de_dados_de_publicação>-\< publicação>-\< assinante>-\< Banco_de_dados_de_assinatura>-\< inteiro>**|  
|Merge Agent para assinaturas push|**\< publicador>-\< Banco_de_dados_de_publicação>-\< publicação>-\< assinante>-\< inteiro>**|  
|Distribution Agent para assinaturas push|**\< publicador>-\< Banco_de_dados_de_publicação>-\< publicação>-\< assinante>-\< inteiro>** <sup>1</sup>|  
|Distribution Agent para assinaturas pull|**\< publicador>-\< Banco_de_dados_de_publicação>-\< publicação>-\< assinante>-\< Banco_de_dados_de_assinatura>-\< GUID>** <sup>2</sup>|  
|Distribution Agent para assinaturas push para Assinantes não SQL Server|**\< publicador>-\< Banco_de_dados_de_publicação>-\< publicação>-\< assinante>-\< inteiro>**|  
  
 <sup>1</sup> para assinaturas push para publicações Oracle, é **\< publicador>-\< publicador**> em vez de **\< publicador>-\< banco De_dados_de_publicação>**  
  
 <sup>2</sup> para assinaturas pull para publicações Oracle, é **\< publicador>-\< Banco_de_dados_de_distribuição**> em vez de **\< publicador>-\< banco De_dados_de_publicação>**  
  
#### Para especificar agendas de sincronização  
  
1.  Sobre o **SynchronizationSchedule** página do Assistente para nova assinatura, selecione um dos seguintes valores do **agenda do agente** lista suspensa para cada assinatura que você está criando:  
  
    -   **Executar continuamente**  
  
    -   **Executar somente sob demanda**  
  
    -   **\<Definir agendamento...>**  
  
2.  Se você selecionar **\< Definir agendamento... >**, especifique uma agenda no **Propriedades da agenda de trabalho** caixa de diálogo e clique **OK**.  
  
3.  Conclua o assistente.  
  
#### Para modificar uma agenda de sincronização para uma assinatura push no Replication Monitor  
  
1.  Expanda um Grupo do publicador no painel esquerdo do Replication Monitor, expanda um Publicador e, em seguida, clique em uma publicação.  
  
2.  Clique na guia **Todas as Assinaturas** .  
  
3.  Clique em uma assinatura e, em seguida, clique em **Exibir detalhes**.  
  
4.  No **assinatura \< Nome_da_assinatura >** janela, clique em **ação**, e, em seguida, clique em **\< Nome_do_agente> Propriedades do trabalho**.  
  
5.  No **agendas** página o **Propriedades do trabalho - \< Nome_do_trabalho>** caixa de diálogo, clique em **Editar.**  
  
6.  No **Propriedades da agenda de trabalho** caixa de diálogo, selecione um valor da **tipo de agenda** lista suspensa:  
  
    -   Para especificar que o agente deve executar continuamente, selecione **Iniciar automaticamente quando o SQL Server Agent for iniciado**.  
  
    -   Para especificar que o agente deve ser executado em uma agenda, selecione **Recorrente**.  
  
    -   Para especificar que o agente deve ser executado sob demanda, selecione **Uma vez**.  
  
7.  Se você selecionar **Recorrente**, especifique uma agenda para o agente.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### Para modificar uma agenda de sincronização para uma assinatura push no Management Studio  
  
1.  Conecte-se ao Distribuidor no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e, em seguida, expanda o nó do servidor.  
  
2.  Expanda a pasta **SQL Server Agent** e, em seguida, a pasta **Trabalhos** .  
  
3.  Clique no trabalho para o Distribution Agent ou do Merge Agent associado à assinatura e, em seguida, clique em **propriedades**.  
  
4.  No **agendas** página o **Propriedades do trabalho - \< Nome_do_trabalho>** caixa de diálogo, clique em **Editar.**  
  
5.  No **Propriedades da agenda de trabalho** caixa de diálogo, selecione um valor da **tipo de agenda** lista suspensa:  
  
    -   Para especificar que o agente deve executar continuamente, selecione **Iniciar automaticamente quando o SQL Server Agent for iniciado**.  
  
    -   Para especificar que o agente deve ser executado em uma agenda, selecione **Recorrente**.  
  
    -   Para especificar que o agente deve ser executado sob demanda, selecione **Uma vez**.  
  
6.  Se você selecionar **Recorrente**, especifique uma agenda para o agente.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### Para modificar uma agenda de sincronização para uma assinatura pull no Management Studio  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **SQL Server Agent** e, em seguida, a pasta **Trabalhos** .  
  
3.  Clique no trabalho para o Distribution Agent ou do Merge Agent associado à assinatura e, em seguida, clique em **propriedades**.  
  
4.  No **agendas** página o **Propriedades do trabalho - \< Nome_do_trabalho>** caixa de diálogo, clique em **Editar.**  
  
5.  No **Propriedades da agenda de trabalho** caixa de diálogo, selecione um valor da **tipo de agenda** lista suspensa:  
  
    -   Para especificar que o agente deve executar continuamente, selecione **Iniciar automaticamente quando o SQL Server Agent for iniciado**.  
  
    -   Para especificar que o agente deve ser executado em uma agenda, selecione **Recorrente**.  
  
    -   Para especificar que o agente deve ser executado sob demanda, selecione **Uma vez**.  
  
6.  Se você selecionar **Recorrente**, especifique uma agenda para o agente.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Você pode definir agendas de sincronização de forma programada, usando os procedimentos de replicação armazenados. Os procedimentos armazenados que você usar dependem do tipo de replicação e do tipo de assinatura (de recepção ou push).  
  
 Uma agenda é definida, os seguintes parâmetros de agendamento, os comportamentos dos quais são herdados de [sp_add_schedule & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md):  
  
-   **@frequency_type** -o tipo de frequência usado ao programar o agente.  
  
-   **@frequency_interval** - o dia da semana em que um agente é executado.  
  
-   **@frequency_relative_interval** - semana de um determinado mês quando o agente é agendado para ser executado mensalmente.  
  
-   **@frequency_recurrence_factor** -o número de unidades tipo frequência que ocorrem entre as sincronizações.  
  
-   **@frequency_subday** -a unidade de frequência quando o agente é executado com mais frequência do que uma vez por dia.  
  
-   **@frequency_subday_interval** -o número de unidades de frequência entre é executado quando o agente é executado com mais frequência do que uma vez por dia.  
  
-   **@active_start_time_of_day** - o horário mais cedo em um determinado dia quando começará a execução do agente.  
  
-   **@active_end_time_of_day** - a hora mais recente em um determinado dia quando começará a execução do agente.  
  
-   **@active_start_date** - o primeiro dia em que a agenda do agente estará em vigor.  
  
-   **@active_end_date** - o último dia em que a agenda do agente estará em vigor.  
  
#### Para definir a agenda de sincronização para uma assinatura pull em uma publicação transacional  
  
1.  Crie uma assinatura pull nova para uma publicação transacional. Para obter mais informações, confira [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
2.  No assinante, execute [sp_addpullsubscription_agent & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Especifique **@publisher**, **@publisher_db**, **@publication**, e o [!INCLUDE[msCoName](../../includes/msconame-md.md)] as credenciais do Windows sob as quais o Distribution Agent no assinante executa **@job_name** e **@password**. Especifique os parâmetros de sincronização, detalhados acima, que definem a agenda para o trabalho do Distribution Agent que sincroniza a assinatura.  
  
#### Para definir a agenda de sincronização para uma assinatura push em uma publicação transacional  
  
1.  Crie uma assinatura push nova para uma publicação transacional. Para obter mais informações, consulte [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
2.  No assinante, execute [sp_addpushsubscription_agent & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md). Especifique **@subscriber**, **@subscriber_db**, **@publication**, e as credenciais do Windows sob a qual o Distribution Agent no assinante executa **@job_name** e **@password**. Especifique os parâmetros de sincronização, detalhados acima, que definem a agenda para o trabalho do Distribution Agent que sincroniza a assinatura.  
  
#### Para definir a agenda de sincronização para uma assinatura pull em uma publicação de mesclagem  
  
1.  Crie uma assinatura pull nova para uma publicação de mesclagem. Para obter mais informações, confira [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
2.  No assinante, execute [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Especifique **@publisher**, **@publisher_db**, **@publication**, e as credenciais do Windows sob a qual o Merge Agent no assinante executa **@job_name** e **@password**. Especifique os parâmetros de sincronização, detalhados acima, que definem a agenda para o trabalho do Agente de Mesclagem que sincroniza a assinatura.  
  
#### Para definir a agenda de sincronização para uma assinatura push em uma publicação de mesclagem  
  
1.  Crie uma assinatura push nova para uma publicação de mesclagem. Para obter mais informações, consulte [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
2.  No assinante, execute [sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md). Especifique **@subscriber**, **@subscriber_db**, **@publication**, e as credenciais do Windows sob a qual o Merge Agent no assinante executa **@job_name** e **@password**. Especifique os parâmetros de sincronização, detalhados acima, que definem a agenda para o trabalho do Agente de Mesclagem que sincroniza a assinatura.  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 A replicação usa o SQL Server Agent para agendar trabalhos para atividades que ocorrem periodicamente, como geração de instantâneo e sincronização de assinatura. Use programaticamente os RMO (Replication Management Objects) para especificar agendamentos de trabalhos de agente de replicação.  
  
> [!NOTE]  
>  Quando você criar uma assinatura e especificar um valor **false** para **CreateSyncAgentByDefault** (o comportamento padrão para assinaturas pull) o trabalho do agente não será criado e as propriedades de agendamento são ignoradas. Nesse caso, o agendamento de sincronização precisará ser determinado pelo aplicativo. Para obter mais informações, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) e [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
#### Para definir um agendamento de agente de replicação quando é criada uma assinatura push para uma publicação transacional  
  
1.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.TransSubscription> classe para a assinatura que você está criando. Para obter mais informações, consulte [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
2.  Antes de chamar <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>, defina uma ou mais dos seguintes campos do <xref:Microsoft.SqlServer.Replication.Subscription.AgentSchedule%2A> propriedade:  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> -o tipo de frequência (por exemplo, diária ou semanalmente) usar ao agendar o agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> - o dia da semana em que um agente é executado.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> - semana de um determinado mês quando o agente é agendado para ser executado mensalmente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> -o número de unidades tipo frequência que ocorrem entre as sincronizações.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> -a unidade de frequência quando o agente é executado com mais frequência do que uma vez por dia.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> -o número de unidades de frequência entre é executado quando o agente é executado com mais frequência do que uma vez por dia.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - hora mais antiga em um determinado dia que inicia uma execução de agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - hora posterior em um determinado dia que inicia uma execução de agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> - primeiro dia em que a agenda do agente está em vigor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> - último dia em que a agenda do agente está em vigor.  
  
    > [!NOTE]  
    >  Se uma dessas propriedades não for especificada, um valor padrão será determinado.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> método para criar a assinatura.  
  
#### Para definir um agendamento de agente de replicação quando é criada uma assinatura pull para uma publicação transacional  
  
1.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.TransPullSubscription> classe para a assinatura que você está criando. Para obter mais informações, confira [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
2.  Antes de chamar <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A>, defina uma ou mais dos seguintes campos do <xref:Microsoft.SqlServer.Replication.PullSubscription.AgentSchedule%2A> propriedade:  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> -o tipo de frequência (por exemplo, diária ou semanal) que você usa ao agendar o agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> - o dia da semana em que um agente é executado.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> - semana de um determinado mês em que o agente é agendado para ser executado mensalmente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> -o número de unidades tipo frequência que ocorrem entre as sincronizações.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> -a unidade de frequência quando o agente é executado com mais frequência do que uma vez por dia.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> -o número de unidades de frequência entre é executado quando o agente é executado com mais frequência do que uma vez por dia.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - hora mais antiga em um determinado dia que inicia uma execução de agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - hora posterior em um determinado dia que inicia uma execução de agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> - primeiro dia em que a agenda do agente está em vigor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> - último dia em que a agenda do agente está em vigor.  
  
    > [!NOTE]  
    >  Se uma dessas propriedades não for especificada, um valor padrão será determinado.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> método para criar a assinatura.  
  
#### Para definir um agendamento de agente de replicação quando uma assinatura pull é criada para uma publicação de mesclagem  
  
1.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergePullSubscription> classe para a assinatura que você está criando. Para obter mais informações, confira [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
2.  Antes de chamar <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A>, defina uma ou mais dos seguintes campos do <xref:Microsoft.SqlServer.Replication.PullSubscription.AgentSchedule%2A> propriedade:  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> -o tipo de frequência (por exemplo, diária ou semanal) que você usa ao agendar o agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> - o dia da semana em que um agente é executado.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> - semana de um determinado mês em que o agente é agendado para ser executado mensalmente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> -o número de unidades tipo frequência que ocorrem entre as sincronizações.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> -a unidade de frequência quando o agente é executado com mais frequência do que uma vez por dia.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> -o número de unidades de frequência entre é executado quando o agente é executado com mais frequência do que uma vez por dia.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - hora mais antiga em um determinado dia que inicia uma execução de agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - hora posterior em um determinado dia que inicia uma execução de agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> - primeiro dia em que a agenda do agente está em vigor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> - último dia em que a agenda do agente está em vigor.  
  
    > [!NOTE]  
    >  Se uma dessas propriedades não for especificada, um valor padrão será determinado.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> método para criar a assinatura.  
  
#### Para definir um agendamento de agente de replicação quando uma assinatura push é criada para uma publicação de mesclagem  
  
1.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergeSubscription> classe para a assinatura que você está criando. Para obter mais informações, consulte [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
2.  Antes de chamar <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>, defina uma ou mais dos seguintes campos do <xref:Microsoft.SqlServer.Replication.Subscription.AgentSchedule%2A> propriedade:  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> -o tipo de frequência (por exemplo, diária ou semanal) que você usa ao agendar o agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> - o dia da semana em que um agente é executado.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> - semana de um determinado mês em que o agente é agendado para ser executado mensalmente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> -o número de unidades tipo frequência que ocorrem entre as sincronizações.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> -a unidade de frequência quando o agente é executado com mais frequência do que uma vez por dia.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> -o número de unidades de frequência entre é executado quando o agente é executado com mais frequência do que uma vez por dia.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - hora mais antiga em um determinado dia que inicia uma execução de agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - hora posterior em um determinado dia que inicia uma execução de agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> - primeiro dia em que a agenda do agente está em vigor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> - último dia em que a agenda do agente está em vigor.  
  
    > [!NOTE]  
    >  Se uma dessas propriedades não for especificada, um valor padrão será determinado.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> método para criar a assinatura.  
  
###  <a name="PShellExample"></a> Exemplo (RMO)  
 Esse exemplo cria uma assinatura push para uma publicação de mesclagem e especifica o agendamento em que a assinatura é sincronizada.  
  
 [!code-csharp[HowTo#rmo_CreateMergePushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepushsub)]  
  
## Consulte também  
 [Práticas recomendadas em relação à segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)   
 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)   
 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)   
 [Sincronizar dados](../../relational-databases/replication/synchronize-data.md)  
  
  