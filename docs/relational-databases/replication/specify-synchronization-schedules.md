---
title: Especificar agendas de sincronização | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication], synchronizing
- scheduling synchronization [SQL Server replication]
- synchronization [SQL Server replication], schedules
- replication [SQL Server], synchronization
ms.assetid: 97f2535b-ec19-4973-823d-bcf3d5aa0216
caps.latest.revision: 40
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 05e5e55f02573bc73ac13a411ebb03671bf9bba2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32964801"
---
# <a name="specify-synchronization-schedules"></a>Especificar agendas de sincronização
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como especificar agendas de sincronização no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)]ou o RMO (Replication Management Objects). Quando criar uma assinatura, você pode definir uma agenda de sincronização que controla quando o agente de replicação para a assinatura executará. Se você não especificar os parâmetros de programação, a assinatura usará a agenda padrão.  
  
 Assinaturas são sincronizadas pelo Agente de Distribuição (para replicação transacional e de instantâneo) ou pelo Agente de Mesclagem (para replicação de mesclagem). Os agentes podem ser executados continuamente, sob demanda ou em um agendamento.  
  
 **Neste tópico**  
  
-   **Para especificar agendas de sincronização, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Especifique agendas de sincronização na página **Agenda de Sincronização** do Assistente para Nova Assinatura. Para mais informações sobre como acessar esse assistente, consulte [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md) e [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
 Modifique agendas de sincronização na caixa de diálogo **Propriedades da Agenda de Trabalho** , que se encontra disponível na pasta **Trabalhos** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e nas janelas de detalhes do agente no Replication Monitor. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
 Se você especificar agendas da pasta **Jobs** use a tabela a seguir para determinar o nome do trabalho do agente.  
  
|Agente|Nome do trabalho|  
|-----------|--------------|  
|Merge Agent para assinaturas pull|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<integer>**|  
|Merge Agent para assinaturas push|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|  
|Distribution Agent para assinaturas push|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>** <sup>1</sup>|  
|Distribution Agent para assinaturas pull|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<GUID>** <sup>2</sup>|  
|Distribution Agent para assinaturas push para Assinantes não SQL Server|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|  
  
 <sup>1</sup> Em assinaturas push para publicações Oracle, é **\<Publisher>-\<Publisher**> em vez de **\<Publisher>-\<PublicationDatabase>**  
  
 <sup>2</sup> Para assinaturas pull para publicações Oracle, é **\<Publisher>-\<DistributionDatabase**> em vez de **\<Publisher>-\<PublicationDatabase>**  
  
#### <a name="to-specify-synchronization-schedules"></a>Para especificar agendas de sincronização  
  
1.  Na página **SynchronizationSchedule** do Assistente para Nova Assinatura, selecione um dos seguintes valores da lista suspensa **Agenda do Agente** para cada assinatura que está sendo criada:  
  
    -   **Executar continuamente**  
  
    -   **Executar somente sob demanda**  
  
    -   **\<Definir agendamento...>**  
  
2.  Se você selecionar **\<Define agendamento…>**, especifique uma agenda na caixa de diálogo **Propriedades da Agenda de Trabalho** e clique em **OK**.  
  
3.  Conclua o assistente.  
  
#### <a name="to-modify-a-synchronization-schedule-for-a-push-subscription-in-replication-monitor"></a>Para modificar uma agenda de sincronização para uma assinatura push no Replication Monitor  
  
1.  Expanda um Grupo do publicador no painel esquerdo do Replication Monitor, expanda um Publicador e, em seguida, clique em uma publicação.  
  
2.  Clique na guia **Todas as Assinaturas** .  
  
3.  Clique com o botão direito do mouse em uma assinatura e clique em **Exibir Detalhes**.  
  
4.  Na janela **Assinatura <SubscriptionName>**, clique em **Ação** e depois em **Propriedades do Trabalho de \<AgentName>**.  
  
5.  Na página **Agendas** da caixa de diálogo **Propriedades do Trabalho – \<JobName>**, clique em **Editar.**  
  
6.  Na caixa de diálogo **Propriedades da Agenda de Trabalho** , selecione um valor da lista suspensa **Tipo de Agenda** :  
  
    -   Para especificar que o agente deve executar continuamente, selecione **Iniciar automaticamente quando o SQL Server Agent for iniciado**.  
  
    -   Para especificar que o agente deve ser executado em uma agenda, selecione **Recorrente**.  
  
    -   Para especificar que o agente deve ser executado sob demanda, selecione **Uma vez**.  
  
7.  Se você selecionar **Recorrente**, especifique uma agenda para o agente.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### <a name="to-modify-a-synchronization-schedule-for-a-push-subscription-in-management-studio"></a>Para modificar uma agenda de sincronização para uma assinatura push no Management Studio  
  
1.  Conecte-se ao Distribuidor no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e, em seguida, expanda o nó do servidor.  
  
2.  Expanda a pasta **SQL Server Agent** e, em seguida, a pasta **Trabalhos** .  
  
3.  Clique com o botão direito do mouse no trabalho para o Distribution Agent ou Merge Agent associado à assinatura e, então, clique em **Propriedades**.  
  
4.  Na página **Agendas** da caixa de diálogo **Propriedades do Trabalho – \<JobName>**, clique em **Editar.**  
  
5.  Na caixa de diálogo **Propriedades da Agenda de Trabalho** , selecione um valor da lista suspensa **Tipo de Agenda** :  
  
    -   Para especificar que o agente deve executar continuamente, selecione **Iniciar automaticamente quando o SQL Server Agent for iniciado**.  
  
    -   Para especificar que o agente deve ser executado em uma agenda, selecione **Recorrente**.  
  
    -   Para especificar que o agente deve ser executado sob demanda, selecione **Uma vez**.  
  
6.  Se você selecionar **Recorrente**, especifique uma agenda para o agente.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### <a name="to-modify-a-synchronization-schedule-for-a-pull-subscription-in-management-studio"></a>Para modificar uma agenda de sincronização para uma assinatura pull no Management Studio  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **SQL Server Agent** e, em seguida, a pasta **Trabalhos** .  
  
3.  Clique com o botão direito do mouse no trabalho para o Distribution Agent ou Merge Agent associado à assinatura e, então, clique em **Propriedades**.  
  
4.  Na página **Agendas** da caixa de diálogo **Propriedades do Trabalho – \<JobName>**, clique em **Editar.**  
  
5.  Na caixa de diálogo **Propriedades da Agenda de Trabalho** , selecione um valor da lista suspensa **Tipo de Agenda** :  
  
    -   Para especificar que o agente deve executar continuamente, selecione **Iniciar automaticamente quando o SQL Server Agent for iniciado**.  
  
    -   Para especificar que o agente deve ser executado em uma agenda, selecione **Recorrente**.  
  
    -   Para especificar que o agente deve ser executado sob demanda, selecione **Uma vez**.  
  
6.  Se você selecionar **Recorrente**, especifique uma agenda para o agente.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Você pode definir agendas de sincronização de forma programada, usando os procedimentos de replicação armazenados. Os procedimentos armazenados que você usar dependem do tipo de replicação e do tipo de assinatura (de recepção ou push).  
  
 Uma agenda é definida pelos seguintes parâmetros de programação, os comportamentos dos quais são herdados de [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md):  
  
-   **@frequency_type** - o tipo de frequência usado ao programar o agente.  
  
-   **@frequency_interval** - o dia da semana em que o agente executa.  
  
-   **@frequency_relative_interval** - semana de um determinado mês em que o agente é agendado para ser executado mensalmente.  
  
-   **@frequency_recurrence_factor** - número de unidades do tipo-frequência que ocorrem entre sincronizações.  
  
-   **@frequency_subday** - unidade de frequência em que o agente é executado com frequência maior que uma vez ao dia.  
  
-   **@frequency_subday_interval** - número de unidades de frequência entre execuções quando o agente é executado com frequência maior que uma vez ao dia.  
  
-   **@active_start_time_of_day** - o horário mais cedo em um determinado dia em que uma execução de agente se iniciará.  
  
-   **@active_end_time_of_day** - o horário mais tarde em um determinado dia em que uma execução de agente se iniciará.  
  
-   **@active_start_date** - o primeiro dia em que a agenda do agente estará em vigor.  
  
-   **@active_end_date** - o último dia em que a agenda do agente estará em vigor.  
  
#### <a name="to-define-the-synchronization-schedule-for-a-pull-subscription-to-a-transactional-publication"></a>Para definir a agenda de sincronização para uma assinatura pull em uma publicação transacional  
  
1.  Crie uma assinatura pull nova para uma publicação transacional. Para obter mais informações, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
2.  No Assinante, execute [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Especifique o **@publisher**, o **@publisher_db**, o **@publication**e as credenciais do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows sob as quais o Distribution Agent no Assinante executa o **@job_name** e **@password**. Especifique os parâmetros de sincronização, detalhados acima, que definem a agenda para o trabalho do Distribution Agent que sincroniza a assinatura.  
  
#### <a name="to-define-the-synchronization-schedule-for-a-push-subscription-to-a-transactional-publication"></a>Para definir a agenda de sincronização para uma assinatura push em uma publicação transacional  
  
1.  Crie uma assinatura push nova para uma publicação transacional. Para obter mais informações, consulte [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
2.  No Assinante, execute [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md). Especifique o **@subscriber**, o **@subscriber_db**, o **@publication**e as credenciais do Windows sob as quais o Distribution Agent no Assinante executa o **@job_name** e **@password**. Especifique os parâmetros de sincronização, detalhados acima, que definem a agenda para o trabalho do Distribution Agent que sincroniza a assinatura.  
  
#### <a name="to-define-the-synchronization-schedule-for-a-pull-subscription-to-a-merge-publication"></a>Para definir a agenda de sincronização para uma assinatura pull em uma publicação de mesclagem  
  
1.  Crie uma assinatura pull nova para uma publicação de mesclagem. Para obter mais informações, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
2.  No Assinante, execute o [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Especifique o **@publisher**, o **@publisher_db**, o **@publication**e as credenciais do Windows sob as quais o Merge Agent no Assinante executa o **@job_name** e **@password**. Especifique os parâmetros de sincronização, detalhados acima, que definem a agenda para o trabalho do Agente de Mesclagem que sincroniza a assinatura.  
  
#### <a name="to-define-the-synchronization-schedule-for-a-push-subscription-to-a-merge-publication"></a>Para definir a agenda de sincronização para uma assinatura push em uma publicação de mesclagem  
  
1.  Crie uma assinatura push nova para uma publicação de mesclagem. Para obter mais informações, consulte [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
2.  No Assinante, execute o [sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md). Especifique o **@subscriber**, o **@subscriber_db**, o **@publication**e as credenciais do Windows sob as quais o Merge Agent no Assinante executa o **@job_name** e **@password**. Especifique os parâmetros de sincronização, detalhados acima, que definem a agenda para o trabalho do Agente de Mesclagem que sincroniza a assinatura.  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 A replicação usa o SQL Server Agent para agendar trabalhos para atividades que ocorrem periodicamente, como geração de instantâneo e sincronização de assinatura. Use programaticamente os RMO (Replication Management Objects) para especificar agendamentos de trabalhos de agente de replicação.  
  
> [!NOTE]  
>  Quando uma subscrição é criada e um valor **false** é especificado para **CreateSyncAgentByDefault** (comportamento padrão para inscrições pull), o trabalho do agente não é criado e as propriedades agendadas são ignoradas. Nesse caso, o agendamento de sincronização precisará ser determinado pelo aplicativo. Para obter mais informações, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) e [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-push-subscription-to-a-transactional-publication"></a>Para definir um agendamento de agente de replicação quando é criada uma assinatura push para uma publicação transacional  
  
1.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransSubscription> para a assinatura que está sendo criada. Para obter mais informações, consulte [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
2.  Antes de chamar <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>, defina um ou mais dos campos seguintes da propriedade <xref:Microsoft.SqlServer.Replication.Subscription.AgentSchedule%2A> :  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> - o tipo de frequência (como diária ou semanalmente) usado para agendar o agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> - dia da semana em que o agente é executado.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> - semana de um determinado mês em que o agente é agendado para ser executado mensalmente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> - número de unidades do tipo-frequência que ocorrem entre sincronizações.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> - unidade de frequência em que o agente é executado com frequência maior que uma vez ao dia.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> - número de unidades de frequência entre execuções quando o agente é executado com frequência maior que uma vez ao dia.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - hora anterior em determinado dia em que tem início a execução do agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - hora posterior em um determinado dia em que tem início a execução do agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> - primeiro dia em que o agendamento do agente entra em vigor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> - último dia de vigência do agendamento.  
  
    > [!NOTE]  
    >  Se uma dessas propriedades não for especificada, um valor padrão será determinado.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> para criar a assinatura.  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-pull-subscription-to-a-transactional-publication"></a>Para definir um agendamento de agente de replicação quando é criada uma assinatura pull para uma publicação transacional  
  
1.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransPullSubscription> para a assinatura que está sendo criada. Para obter mais informações, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
2.  Antes de chamar <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A>, defina um ou mais dos campos seguintes da propriedade <xref:Microsoft.SqlServer.Replication.PullSubscription.AgentSchedule%2A> :  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> - tipo de frequência (por exemplo, diária ou semanal) usada durante o agendamento do agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> - dia da semana em que o agente é executado.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> - semana de um determinado mês em que o agente é agendado para ser executado mensalmente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> - número de unidades do tipo-frequência que ocorrem entre sincronizações.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> - unidade de frequência em que o agente é executado com frequência maior que uma vez ao dia.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> - número de unidades de frequência entre execuções quando o agente é executado com frequência maior que uma vez ao dia.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - hora anterior em determinado dia em que tem início a execução do agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - hora posterior em um determinado dia em que tem início a execução do agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> - primeiro dia em que o agendamento do agente entra em vigor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> - último dia de vigência do agendamento.  
  
    > [!NOTE]  
    >  Se uma dessas propriedades não for especificada, um valor padrão será determinado.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> para criar a assinatura.  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-pull-subscription-to-a-merge-publication"></a>Para definir um agendamento de agente de replicação quando uma assinatura pull é criada para uma publicação de mesclagem  
  
1.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePullSubscription> para a assinatura que está sendo criada. Para obter mais informações, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
2.  Antes de chamar <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A>, defina um ou mais dos campos seguintes da propriedade <xref:Microsoft.SqlServer.Replication.PullSubscription.AgentSchedule%2A> :  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> - tipo de frequência (por exemplo, diária ou semanal) usada durante o agendamento do agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> - dia da semana em que o agente é executado.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> - semana de um determinado mês em que o agente é agendado para ser executado mensalmente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> - número de unidades do tipo-frequência que ocorrem entre sincronizações.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> - unidade de frequência em que o agente é executado com frequência maior que uma vez ao dia.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> - número de unidades de frequência entre execuções quando o agente é executado com frequência maior que uma vez ao dia.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - hora anterior em determinado dia em que tem início a execução do agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - hora posterior em um determinado dia em que tem início a execução do agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> - primeiro dia em que o agendamento do agente entra em vigor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> - último dia de vigência do agendamento.  
  
    > [!NOTE]  
    >  Se uma dessas propriedades não for especificada, um valor padrão será determinado.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> para criar a assinatura.  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-push-subscription-to-a-merge-publication"></a>Para definir um agendamento de agente de replicação quando uma assinatura push é criada para uma publicação de mesclagem  
  
1.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergeSubscription> para a assinatura que está sendo criada. Para obter mais informações, consulte [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
2.  Antes de chamar <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>, defina um ou mais dos campos seguintes da propriedade <xref:Microsoft.SqlServer.Replication.Subscription.AgentSchedule%2A> :  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> - tipo de frequência (por exemplo, diária ou semanal) usada durante o agendamento do agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> - dia da semana em que o agente é executado.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> - semana de um determinado mês em que o agente é agendado para ser executado mensalmente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> - número de unidades do tipo-frequência que ocorrem entre sincronizações.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> - unidade de frequência em que o agente é executado com frequência maior que uma vez ao dia.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> - número de unidades de frequência entre execuções quando o agente é executado com frequência maior que uma vez ao dia.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - hora anterior em determinado dia em que tem início a execução do agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - hora posterior em um determinado dia em que tem início a execução do agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> - primeiro dia em que o agendamento do agente entra em vigor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> - último dia de vigência do agendamento.  
  
    > [!NOTE]  
    >  Se uma dessas propriedades não for especificada, um valor padrão será determinado.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> para criar a assinatura.  
  
###  <a name="PShellExample"></a> Exemplo (RMO)  
 Esse exemplo cria uma assinatura push para uma publicação de mesclagem e especifica o agendamento em que a assinatura é sincronizada.  
  
 [!code-cs[HowTo#rmo_CreateMergePushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepushsub)]  
  
## <a name="see-also"></a>Consulte Também  
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [Sincronizar uma assinatura push](../../relational-databases/replication/synchronize-a-push-subscription.md)   
 [Sincronizar uma assinatura pull](../../relational-databases/replication/synchronize-a-pull-subscription.md)   
 [Sincronizar dados](../../relational-databases/replication/synchronize-data.md)  
  
  
