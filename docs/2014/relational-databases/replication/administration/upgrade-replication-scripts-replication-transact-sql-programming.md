---
title: Atualizar scripts de replicação (Programação Transact-SQL de replicação) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- scripts [SQL Server replication], upgrading
- upgrading SQL Server, replicated databases
- upgrading replication applications
- replication [SQL Server], scripting
- replication [SQL Server], upgrading
- upgrading replicated databases
ms.assetid: 0b8720bd-f339-4842-bc8f-b35a46f6d3ee
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cd3f6498cbfb4ef8cf38e27879d619472a6693ce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68210766"
---
# <a name="upgrade-replication-scripts-replication-transact-sql-programming"></a>Atualizar scripts de replicação (Programação Transact-SQL de replicação)
  Podem ser usados arquivos de script[!INCLUDE[tsql](../../../includes/tsql-md.md)] para configurar uma topologia de replicação programaticamente. Para obter mais informações, consulte [Conceitos de procedimentos armazenados no sistema de replicação](../concepts/replication-system-stored-procedures-concepts.md).  
  
> [!IMPORTANT]  
>  Embora não se exija a atualização de scripts executados por membros da função `sysadmin`, recomendamos que você modifique os scripts existentes como descrito neste tópico. Especifique uma conta que tenha permissões mínimas para cada agente de replicação como descrito na seção "Permissões exigidas por agentes" do tópico [Replication Agent Security Model](../security/replication-agent-security-model.md).  
  
 Esses aprimoramentos de segurança, que permitem um maior controle das permissões permitindo que você especifique explicitamente as contas do Windows do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] nas quais são executados trabalhos do agente de replicação, afetam os seguintes procedimentos armazenados nos scripts existentes:  
  
-   **sp_addpublication_snapshot**:  
  
     Agora você deve fornecer as credenciais do Windows **@job_login** como **@job_password** e ao executar [SP_ADDPUBLICATION_SNAPSHOT &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql) para criar o trabalho sob o qual o agente de instantâneo é executado no distribuidor.  
  
-   **sp_addpushsubscription_agent**:  
  
     Agora você deve executar [sp_addpushsubscription_agent &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql) para adicionar explicitamente um trabalho e fornecer as credenciais do Windows**@job_login** ( **@job_password**e) sob as quais o trabalho agente de distribuição é executado no distribuidor. Em versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], isto era feito automaticamente quando era criada uma assinatura push.  
  
-   **sp_addmergepushsubscription_agent**:  
  
     Agora você deve executar [sp_addmergepushsubscription_agent &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql) para adicionar explicitamente um trabalho e fornecer as credenciais do Windows**@job_login** ( **@job_password**e) sob as quais o trabalho agente de mesclagem é executado no distribuidor. Em versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], isto era feito automaticamente quando era criada uma assinatura push.  
  
-   **sp_addpullsubscription_agent**:  
  
     Agora você deve fornecer as credenciais do Windows **@job_login** como **@job_password** e ao executar [SP_ADDPULLSUBSCRIPTION_AGENT &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql) para criar o trabalho sob o qual o agente de distribuição é executado no Assinante.  
  
-   **sp_addmergepullsubscription_agent**:  
  
     Agora você deve fornecer as credenciais do Windows **@job_login** como **@job_password** e ao executar [SP_ADDMERGEPULLSUBSCRIPTION_AGENT &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql) para criar o trabalho sob o qual o agente de mesclagem é executado no Assinante.  
  
-   **sp_addlogreader_agent**:  
  
     Você deve executar o [sp_addlogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql) para adicionar manualmente o trabalho e fornecer as credenciais do Windows sob as quais será executado o Agente de Leitor de Log no Distribuidor. Em versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], isto era feito automaticamente quando era criada uma publicação transacional.  
  
-   **sp_addqreader_agent**:  
  
     Você deve executar o [sp_addqreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql) para adicionar manualmente o trabalho e fornecer as credenciais do Windows sob as quais será executado o Queue Reader Agent no Distribuidor. Em versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], isso era feito automaticamente quando era criada uma publicação transacional que suportava atualização em fila.  
  
 No modelo de segurança introduzido no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], os agentes de replicação sempre fazem conexões com a instância [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] local do com a autenticação do Windows usando **@job_name** as **@job_password**credenciais fornecidas no e no. Para obter informações sobre os requisitos de contas do Windows usados ao executar trabalhos de agente de replicação, consulte [Replication Agent Security Model](../security/replication-agent-security-model.md).  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se você armazenar credenciais em um arquivo de script, verifique se o arquivo está protegido.  
  
### <a name="to-upgrade-scripts-that-configure-a-snapshot-or-transactional-publication"></a>Para atualizar scripts que configuram um instantâneo ou uma publicação transacional  
  
1.  No script existente, antes de [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql), execute [sp_addlogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql) no publicador do banco de dados de publicação. Especifique as credenciais do Windows sob as quais o Agente de Leitor de Log **@job_name** é **@job_password**executado para e. Se [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o agente usar a autenticação do ao se conectar ao Publicador, você também deverá especificar um valor de **@publisher_security_mode** **0** para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e as informações **@publisher_login** de **@publisher_password**logon para e. Isso cria um trabalho do Agente de Leitor de Log para o banco de dados de publicação.  
  
    > [!NOTE]  
    >  Essa etapa é só para publicações transacionais e não é necessária para publicações de instantâneo.  
  
2.  (Opcional) Antes de [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql), execute [sp_addqreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql) no Distribuidor no banco de dados de distribuição. Especifique as credenciais do Windows sob as quais o Queue Reader Agent **@job_name** é **@job_password**executado para e. Isso cria um trabalho do Agente de Leitor de Fila para o Distribuidor.  
  
    > [!NOTE]  
    >  Essa etapa só é necessária para publicações transacionais que dão suporte a assinantes de atualização em fila.  
  
3.  (Opcional) Atualize a execução de [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) para definir qualquer valor não padrão para parâmetros que implementam novas funcionalidades de replicação.  
  
4.  Depois de [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql), execute [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql) no Publicador do banco de dados de publicação. Especifique **@publication** e as credenciais do Windows sob as quais o agente de instantâneo **@job_name** é **@job_password**executado para e. Se [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o agente usar a autenticação do ao se conectar ao Publicador, você também deverá especificar um valor de **@publisher_security_mode** **0** para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e as informações **@publisher_login** de **@publisher_password**logon para e. Isso cria um trabalho do Agente de Instantâneo para a publicação.  
  
5.  (Opcional) Atualize a execução de [sp_addarticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) para definir qualquer valor não padrão para parâmetros que implementam novas funcionalidades de replicação.  
  
### <a name="to-upgrade-scripts-that-add-subscriptions-to-a-snapshot-or-transactional-publication"></a>Para atualizar scripts que adicionam assinaturas a um instantâneo ou publicação transacional  
  
1.  Após executar o procedimento armazenado que cria a assinatura, certifique-se de executar o procedimento armazenado que cria um trabalho do agente de distribuição para sincronizar a assinatura. O procedimento armazenado usado dependerá do tipo de assinatura.  
  
    -   Para uma assinatura pull, atualize a execução de [sp_addpullsubscription_agent &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql) para fornecer as credenciais do Windows sob as quais o agente de distribuição é executado no **@job_name** assinante para e **@job_password**. Isso é feito após a execução de [sp_addpullsubscription](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql). Para obter mais informações, consulte [Create a Pull Subscription](../create-a-pull-subscription.md).  
  
    -   Para uma assinatura push, execute [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql) no Publicador. Especifique **@subscriber**, **@subscriber_db**, **@publication**, as credenciais do Windows sob as quais o agente de distribuição é executado **@job_name** no **@job_password**distribuidor para e e uma agenda para esse trabalho do Agent. Para obter mais informações, consulte [Specify Synchronization Schedules](../specify-synchronization-schedules.md). Isso é feito após a execução de [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql). Para obter mais informações, consulte [Create a Push Subscription](../create-a-push-subscription.md).  
  
### <a name="to-upgrade-scripts-that-configure-a-merge-publication"></a>Para atualizar scripts que configuram uma publicação de mesclagem  
  
1.  (Opcional) No script existente, atualize a execução de [sp_addmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql) para definir qualquer valor não padrão para parâmetros que implementam novas funcionalidades de replicação.  
  
2.  Depois de [sp_addmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql), execute [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql) no Publicador do banco de dados de publicação. Especifique **@publication** e as credenciais do Windows sob as quais o agente de instantâneo **@job_name** é **@job_password**executado para e. Se [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o agente usar a autenticação do ao se conectar ao Publicador, você também deverá especificar um valor de **@publisher_security_mode** **0** para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e as informações **@publisher_login** de **@publisher_password**logon para e. Isso cria um trabalho do Agente de Instantâneo para a publicação.  
  
3.  (Opcional) Atualize a execução de [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) para definir qualquer valor não padrão para parâmetros que implementam novas funcionalidades de replicação.  
  
### <a name="to-upgrade-scripts-that-add-subscriptions-to-a-merge-publication"></a>Para atualizar scripts que adicionam assinaturas a uma publicação de mesclagem  
  
1.  Após executar o procedimento armazenado que cria a assinatura, assegure-se de executar o procedimento armazenado que cria um trabalho do Agente de Mesclagem para sincronizar a assinatura. O procedimento armazenado usado dependerá do tipo de assinatura.  
  
    -   Para uma assinatura pull, atualize a execução de [sp_addmergepullsubscription_agent &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql) para fornecer as credenciais do Windows sob as quais o agente de mesclagem é executado no **@job_name** assinante para e **@job_password**. Isso é feito após a execução de [sp_addmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql). Para obter mais informações, consulte [Create a Pull Subscription](../create-a-pull-subscription.md).  
  
    -   Para uma assinatura push, execute [sp_addmergepushsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql) no Publicador. Especifique **@subscriber**, **@subscriber_db**, **@publication**, as credenciais do Windows sob as quais o agente de mesclagem no distribuidor é **@job_name** executado **@job_password**para e e uma agenda para esse trabalho do Agent. Para obter mais informações, consulte [Specify Synchronization Schedules](../specify-synchronization-schedules.md). Isso é feito após a execução de [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql). Para obter mais informações, consulte [Create a Push Subscription](../create-a-push-subscription.md).  
  
## <a name="example"></a>Exemplo  
 Abaixo está um exemplo de um script do [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que cria uma publicação transacional para a tabela Produto. Essa publicação dá suporte para a atualização imediata com atualização em fila como failover. Os parâmetros padrão foram removidos para facilitar a legibilidade.  
  
 [!code-sql[HowTo#sp_createtranpub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwtranpub80.sql#sp_createtranpub_nwpreupgrade)]  
  
## <a name="example"></a>Exemplo  
 Abaixo mostramos um exemplo de atualização do script anterior, que cria uma publicação transacional, para que o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e suas versões posteriores possam ser executadas com êxito. Essa publicação dá suporte para a atualização imediata com atualização em fila como failover. Os padrões para parâmetros novos foram declarados explicitamente.  
  
> [!NOTE]  
>  As credenciais do Windows são fornecidas no tempo de execução que usa variáveis de script **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createtranpub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwtranpublication.sql#sp_createtranpub_nwpostupgrade)]  
  
## <a name="example"></a>Exemplo  
 Abaixo mostramos um exemplo de um script do [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que cria uma publicação de mesclagem para a tabela Clientes. Os parâmetros padrão foram removidos para facilitar a legibilidade.  
  
 [!code-sql[HowTo#sp_createmergepub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepub80.sql#sp_createmergepub_nwpreupgrade)]  
  
## <a name="example"></a>Exemplo  
 Abaixo mostramos um exemplo do script anterior, que cria uma publicação de mesclagem, atualizada para que o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e suas versões posteriores possam ser executadas com êxito. Os padrões para parâmetros novos foram declarados explicitamente.  
  
> [!NOTE]  
>  As credenciais do Windows são fornecidas no tempo de execução que usa variáveis de script **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createmergepub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepublication.sql#sp_createmergepub_nwpostupgrade)]  
  
## <a name="example"></a>Exemplo  
 O exemplo abaixo mostra um script do [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que cria uma assinatura push para uma publicação transacional. Os parâmetros padrão foram removidos para facilitar a legibilidade.  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwtranpushsub80.sql#sp_createtranpushsub_nwpreupgrade)]  
  
## <a name="example"></a>Exemplo  
 Abaixo mostramos um exemplo do script anterior, que cria uma assinatura push para uma publicação transacional, atualizado para que o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e suas versões posteriores possam ser executadas com êxito. Os padrões para parâmetros novos foram declarados explicitamente.  
  
> [!NOTE]  
>  As credenciais do Windows são fornecidas no tempo de execução que usa variáveis de script **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwpushsub.sql#sp_createtranpushsub_nwpostupgrade)]  
  
## <a name="example"></a>Exemplo  
 O exemplo abaixo mostra um script do [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que cria uma assinatura push para uma publicação de mesclagem. Os parâmetros padrão foram removidos para facilitar a legibilidade.  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepushsub80.sql#sp_createmergepushsub_nwpreupgrade)]  
  
## <a name="example"></a>Exemplo  
 Abaixo mostramos um exemplo do script anterior, que cria uma assinatura push para uma publicação de mesclagem, atualizado para que o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e suas versões posteriores possam ser executadas com êxito. Os padrões para parâmetros novos foram declarados explicitamente.  
  
> [!NOTE]  
>  As credenciais do Windows são fornecidas no tempo de execução que usa variáveis de script **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwpushsub.sql#sp_createmergepushsub_nwpostupgrade)]  
  
## <a name="example"></a>Exemplo  
 O exemplo abaixo mostra um script do [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que cria uma assinatura pull para uma publicação transacional. Os parâmetros padrão foram removidos para facilitar a legibilidade.  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepushsub80.sql#sp_createmergepushsub_nwpreupgrade)]  
  
## <a name="example"></a>Exemplo  
 Abaixo mostramos um exemplo do script anterior, que cria uma assinatura pull para uma publicação transacional, atualizado para que o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e suas versões posteriores possam ser executadas com êxito. Os padrões para parâmetros novos foram declarados explicitamente.  
  
> [!NOTE]  
>  As credenciais do Windows são fornecidas no tempo de execução que usa variáveis de script **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createtranpullsub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwpullsub.sql#sp_createtranpullsub_nwpostupgrade)]  
  
## <a name="example"></a>Exemplo  
 O exemplo abaixo mostra um script do [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que cria uma assinatura pull para uma publicação de mesclagem. Os parâmetros padrão foram removidos para facilitar a legibilidade.  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepullsub80.sql#sp_createmergepullsub_nwpreupgrade)]  
  
## <a name="example"></a>Exemplo  
 Abaixo mostramos um exemplo do script anterior, que cria uma assinatura pull para uma publicação de mesclagem, atualizado para que o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e suas versões posteriores possam ser executadas com êxito. Os padrões para parâmetros novos foram declarados explicitamente.  
  
> [!NOTE]  
>  As credenciais do Windows são fornecidas no tempo de execução que usa variáveis de script **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwpullsub.sql#sp_createmergepullsub_nwpostupgrade)]  
  
## <a name="see-also"></a>Consulte Também  
 [Create a Publication](../publish/create-a-publication.md)   
 [Create a Push Subscription](../create-a-push-subscription.md)   
 [Create a Pull Subscription](../create-a-pull-subscription.md)   
 [Exibir e modificar configurações de segurança de replicação](../security/view-and-modify-replication-security-settings.md)   
 [MSSQL_ENG021797](../mssql-eng021797.md)   
 [MSSQL_ENG021798](../mssql-eng021798.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [Atualizar bancos de dados replicados](../../../database-engine/install-windows/upgrade-replicated-databases.md)  
  
  
