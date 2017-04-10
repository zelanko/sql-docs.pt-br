---
title: "Atualizar scripts de replica&#231;&#227;o (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "scripts [replicação do SQL Server], atualizando"
  - "atualizando o SQL Server, bancos de dados replicados"
  - "atualizando aplicativos de replicação"
  - "replicação [SQL Server], scripts"
  - "replicação [SQL Server], atualizando"
  - "atualizando bancos de dados replicados"
ms.assetid: 0b8720bd-f339-4842-bc8f-b35a46f6d3ee
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# Atualizar scripts de replica&#231;&#227;o (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o)
  [!INCLUDE[tsql](../../../includes/tsql-md.md)] para configurar uma topologia de replicação programaticamente. Para obter mais informações, consulte [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md).  
  
> [!IMPORTANT]  
>  Embora não se exija a atualização de scripts executados por membros da função **sysadmin** , recomendamos que você modifique os scripts existentes como descrito neste tópico. Especifique uma conta que tenha permissões mínimas para cada agente de replicação como descrito na seção "Permissões exigidas por agentes" do tópico [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
 Esses aprimoramentos de segurança, que permitem um maior controle das permissões permitindo que você especifique explicitamente as contas do Windows do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] nas quais são executados trabalhos do agente de replicação, afetam os seguintes procedimentos armazenados nos scripts existentes:  
  
-   **sp_addpublication_snapshot**:  
  
     Você deve fornecer as credenciais do Windows como **@job_login** e **@job_password** ao executar [sp_addpublication_snapshot & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) para criar o trabalho na qual o Snapshot Agent é executado no distribuidor.  
  
-   **sp_addpushsubscription_agent**:  
  
     Você deve executar [sp_addpushsubscription_agent & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md) Para adicionar um trabalho explicitamente e fornecer as credenciais do Windows (**@job_login** e **@job_password**) na qual o trabalho do Distribution Agent é executado no distribuidor. Em versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], isto era feito automaticamente quando era criada uma assinatura push.  
  
-   **sp_addmergepushsubscription_agent**:  
  
     Você deve executar [sp_addmergepushsubscription_agent & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md) Para adicionar um trabalho explicitamente e fornecer as credenciais do Windows (**@job_login** e **@job_password**) na qual o trabalho do Merge Agent é executado no distribuidor. Em versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], isto era feito automaticamente quando era criada uma assinatura push.  
  
-   **sp_addpullsubscription_agent**:  
  
     Você deve fornecer as credenciais do Windows como **@job_login** e **@job_password** ao executar [sp_addpullsubscription_agent & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) para criar o trabalho na qual o Distribution Agent é executado no assinante.  
  
-   **sp_addmergepullsubscription_agent**:  
  
     Você deve fornecer as credenciais do Windows como **@job_login** e **@job_password** ao executar [sp_addmergepullsubscription_agent & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) para criar o trabalho na qual o Merge Agent é executado no assinante.  
  
-   **sp_addlogreader_agent**:  
  
     Você deve executar [sp_addlogreader_agent & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md) Para adicionar manualmente o trabalho e fornecer as credenciais do Windows na qual o Log Reader Agent é executado no distribuidor. Em versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], isto era feito automaticamente quando era criada uma publicação transacional.  
  
-   **sp_addqreader_agent**:  
  
     Você deve executar [sp_addqreader_agent & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md) Para adicionar manualmente o trabalho e fornecer as credenciais do Windows na qual o Queue Reader Agent é executado no distribuidor. Em versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], isso era feito automaticamente quando era criada uma publicação transacional que suportava atualização em fila.  
  
 No modelo de segurança introduzido no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], os agentes de replicação sempre fazem conexão com a instância local do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com autenticação do Windows usando as credenciais fornecidas na **@job_name** e **@job_password**. Para obter informações sobre os requisitos de contas do Windows usados ao executar trabalhos de agente de replicação, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se você armazenar credenciais em um arquivo de script, verifique se o arquivo está protegido.  
  
### Para atualizar scripts que configuram um instantâneo ou uma publicação transacional  
  
1.  No script existente, antes de [sp_addpublication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), execute [sp_addlogreader_agent & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md) o publicador do banco de dados de publicação. Especifique as credenciais do Windows na qual o Log Reader Agent é executado para **@job_name** e **@job_password**. Se o agente usará [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] autenticação ao conectar-se ao publicador, você deve especificar um valor de **0** para **@publisher_security_mode** e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] informações de logon para **@publisher_login** e **@publisher_password**. Isso cria um trabalho do Agente de Leitor de Log para o banco de dados de publicação.  
  
    > [!NOTE]  
    >  Essa etapa é só para publicações transacionais e não é necessária para publicações de instantâneo.  
  
2.  (Opcional) Antes de [sp_addpublication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), execute [sp_addqreader_agent & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md) no distribuidor no banco de dados de distribuição. Especifique as credenciais do Windows na qual o Queue Reader Agent é executado para **@job_name** e **@job_password**. Isso cria um trabalho do Agente de Leitor de Fila para o Distribuidor.  
  
    > [!NOTE]  
    >  Essa etapa só é necessária para publicações transacionais que dão suporte a assinantes de atualização em fila.  
  
3.  (Opcional) Atualize a execução de [sp_addpublication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) Para definir qualquer valor não padrão para parâmetros que implementam funcionalidades de replicação novas.  
  
4.  Depois de [sp_addpublication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), execute [sp_addpublication_snapshot & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) o publicador do banco de dados de publicação. Especifique **@publication** e as credenciais do Windows na qual o Snapshot Agent é executado para **@job_name** e **@job_password**. Se o agente usará [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] autenticação ao conectar-se ao publicador, você deve especificar um valor de **0** para **@publisher_security_mode** e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] informações de logon para **@publisher_login** e **@publisher_password**. Isso cria um trabalho do Agente de Instantâneo para a publicação.  
  
5.  (Opcional) Atualize a execução de [sp_addarticle & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) Para definir qualquer valor não padrão para parâmetros que implementam funcionalidades de replicação novas.  
  
### Para atualizar scripts que adicionam assinaturas a um instantâneo ou publicação transacional  
  
1.  Após executar o procedimento armazenado que cria a assinatura, certifique-se de executar o procedimento armazenado que cria um trabalho do agente de distribuição para sincronizar a assinatura. O procedimento armazenado usado dependerá do tipo de assinatura.  
  
    -   Para uma assinatura pull, atualize a execução de [sp_addpullsubscription_agent & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) para fornecer as credenciais do Windows na qual o Distribution Agent é executado no assinante para **@job_name** e **@job_password**. Isso é feito após a execução de [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md). Para obter mais informações, confira [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
    -   Para uma inscrição de envio, execute [sp_addpushsubscription_agent & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md) no Editor. Especifique **@subscriber**, **@subscriber_db**, **@publication**, as credenciais do Windows na qual o Distribution Agent é executado no distribuidor para **@job_name** e **@job_password**, e um agendamento para esse trabalho de agente. Para obter mais informações, consulte [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md). Isso é feito após a execução de [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Para obter mais informações, consulte [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md).  
  
### Para atualizar scripts que configuram uma publicação de mesclagem  
  
1.  (Opcional) No script existente, atualize a execução de [sp_addmergepublication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) Para definir qualquer valor não padrão para parâmetros que implementam funcionalidades de replicação novas.  
  
2.  Depois de [sp_addmergepublication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md), execute [sp_addpublication_snapshot & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) o publicador do banco de dados de publicação. Especifique **@publication** e as credenciais do Windows na qual o Snapshot Agent é executado para **@job_name** e **@job_password**. Se o agente usará [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] autenticação ao conectar-se ao publicador, você deve especificar um valor de **0** para **@publisher_security_mode** e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] informações de logon para **@publisher_login** e **@publisher_password**. Isso cria um trabalho do Agente de Instantâneo para a publicação.  
  
3.  (Opcional) Atualize a execução de [sp_addmergearticle & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) Para definir qualquer valor não padrão para parâmetros que implementam funcionalidades de replicação novas.  
  
### Para atualizar scripts que adicionam assinaturas a uma publicação de mesclagem  
  
1.  Após executar o procedimento armazenado que cria a assinatura, assegure-se de executar o procedimento armazenado que cria um trabalho do Agente de Mesclagem para sincronizar a assinatura. O procedimento armazenado usado dependerá do tipo de assinatura.  
  
    -   Para uma assinatura pull, atualize a execução de [sp_addmergepullsubscription_agent & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) para fornecer as credenciais do Windows na qual o Merge Agent é executado no assinante para **@job_name** e **@job_password**. Isso é feito após a execução de [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Para obter mais informações, confira [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
    -   Para uma inscrição de envio, execute [sp_addmergepushsubscription_agent & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md) no Editor. Especifique **@subscriber**, **@subscriber_db**, **@publication**, as credenciais do Windows sob a qual o Merge Agent no distribuidor executa **@job_name** e **@job_password**, e um agendamento para esse trabalho de agente. Para obter mais informações, consulte [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md). Isso é feito após a execução de [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md). Para obter mais informações, consulte [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md).  
  
## Exemplo  
 Abaixo está um exemplo de um script do [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que cria uma publicação transacional para a tabela Produto. Essa publicação dá suporte para a atualização imediata com atualização em fila como failover. Os parâmetros padrão foram removidos para facilitar a legibilidade.  
  
 [!code-sql[HowTo#sp_createtranpub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_1.sql)]  
  
## Exemplo  
 Abaixo mostramos um exemplo de atualização do script anterior, que cria uma publicação transacional, para que o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e suas versões posteriores possam ser executadas com êxito. Essa publicação dá suporte para a atualização imediata com atualização em fila como failover. Os padrões para parâmetros novos foram declarados explicitamente.  
  
> [!NOTE]  
>  Credenciais do Windows são fornecidas em tempo de execução usando **sqlcmd** variáveis de script.  
  
 [!code-sql[HowTo#sp_createtranpub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_2.sql)]  
  
## Exemplo  
 Abaixo mostramos um exemplo de um script do [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que cria uma publicação de mesclagem para a tabela Clientes. Os parâmetros padrão foram removidos para facilitar a legibilidade.  
  
 [!code-sql[HowTo#sp_createmergepub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_3.sql)]  
  
## Exemplo  
 Abaixo mostramos um exemplo do script anterior, que cria uma publicação de mesclagem, atualizada para que o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e suas versões posteriores possam ser executadas com êxito. Os padrões para parâmetros novos foram declarados explicitamente.  
  
> [!NOTE]  
>  Credenciais do Windows são fornecidas em tempo de execução usando **sqlcmd** variáveis de script.  
  
 [!code-sql[HowTo#sp_createmergepub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_4.sql)]  
  
## Exemplo  
 O exemplo abaixo mostra um script do [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que cria uma assinatura push para uma publicação transacional. Os parâmetros padrão foram removidos para facilitar a legibilidade.  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_5.sql)]  
  
## Exemplo  
 Abaixo mostramos um exemplo do script anterior, que cria uma assinatura push para uma publicação transacional, atualizado para que o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e suas versões posteriores possam ser executadas com êxito. Os padrões para parâmetros novos foram declarados explicitamente.  
  
> [!NOTE]  
>  Credenciais do Windows são fornecidas em tempo de execução usando **sqlcmd** variáveis de script.  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_6.sql)]  
  
## Exemplo  
 O exemplo abaixo mostra um script do [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que cria uma assinatura push para uma publicação de mesclagem. Os parâmetros padrão foram removidos para facilitar a legibilidade.  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_7.sql)]  
  
## Exemplo  
 Abaixo mostramos um exemplo do script anterior, que cria uma assinatura push para uma publicação de mesclagem, atualizado para que o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e suas versões posteriores possam ser executadas com êxito. Os padrões para parâmetros novos foram declarados explicitamente.  
  
> [!NOTE]  
>  Credenciais do Windows são fornecidas em tempo de execução usando **sqlcmd** variáveis de script.  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_8.sql)]  
  
## Exemplo  
 O exemplo abaixo mostra um script do [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que cria uma assinatura pull para uma publicação transacional. Os parâmetros padrão foram removidos para facilitar a legibilidade.  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_7.sql)]  
  
## Exemplo  
 Abaixo mostramos um exemplo do script anterior, que cria uma assinatura pull para uma publicação transacional, atualizado para que o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e suas versões posteriores possam ser executadas com êxito. Os padrões para parâmetros novos foram declarados explicitamente.  
  
> [!NOTE]  
>  Credenciais do Windows são fornecidas em tempo de execução usando **sqlcmd** variáveis de script.  
  
 [!code-sql[HowTo#sp_createtranpullsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_9.sql)]  
  
## Exemplo  
 O exemplo abaixo mostra um script do [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que cria uma assinatura pull para uma publicação de mesclagem. Os parâmetros padrão foram removidos para facilitar a legibilidade.  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_10.sql)]  
  
## Exemplo  
 Abaixo mostramos um exemplo do script anterior, que cria uma assinatura pull para uma publicação de mesclagem, atualizado para que o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e suas versões posteriores possam ser executadas com êxito. Os padrões para parâmetros novos foram declarados explicitamente.  
  
> [!NOTE]  
>  Credenciais do Windows são fornecidas em tempo de execução usando **sqlcmd** variáveis de script.  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_11.sql)]  
  
## Consulte também  
 [Crie uma publicação](../../../relational-databases/replication/publish/create-a-publication.md)   
 [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md)   
 [Criar uma assinatura pull](../../../relational-databases/replication/create-a-pull-subscription.md)   
 [View and Modify Replication Security Settings](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [MSSQL_ENG021797](../../../relational-databases/replication/mssql-eng021797.md)   
 [MSSQL_ENG021798](../../../relational-databases/replication/mssql-eng021798.md)   
 [Conceitos dos procedimentos armazenados do sistema de replicação](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Atualizar bancos de dados replicados](../../../database-engine/install-windows/upgrade-replicated-databases.md)  
  
  