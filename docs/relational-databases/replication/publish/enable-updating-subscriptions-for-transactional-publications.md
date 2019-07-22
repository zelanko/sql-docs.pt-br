---
title: Habilitar atualização de assinaturas para publicações transacionais | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, updatable subscriptions
- updatable subscriptions, enabling
- subscriptions [SQL Server replication], updatable
ms.assetid: 539d5bb0-b808-4d8c-baf4-cb6d32d2c595
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1efb8f73d1348b34673eb836e173ed39328d5976
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907624"
---
# <a name="enable-updating-subscriptions-for-transactional-publications"></a>Habilitar atualização de assinaturas para publicações transacionais
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como habilitar as assinaturas de atualização para publicações transacionais no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
> **OBSERVAÇÃO!** [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  

##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
 Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Habilite as assinaturas de atualização para publicações transacionais na página **Tipo de Publicação** do Assistente para Nova Publicação.  
  
 Para usar assinaturas de atualização, você deve configurar também as opções no Assistente para Nova Assinatura.  
  
#### <a name="to-enable-updating-subscriptions"></a>Para habilitar assinaturas de atualização  
  
1.  Na página **Tipo de Publicação** do Assistente para Nova Publicação, selecione **Publicação transacional com assinaturas atualizáveis**.  
  
2.  Na página **Segurança do Agente** , especifique as definições do Queue Reader Agent além de Snapshot Agent e Log Reader Agent. Para obter mais informações sobre as permissões que são exigidas para a conta sob a qual o Queue Reader Agent executa, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

    > **NOTE:** The Queue Reader Agent is configured even if you use only immediate updating subscriptions.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Ao criar uma publicação transacional de forma programática usando procedimentos armazenados de replicação, é possível ativar tanto as assinaturas de atualização imediatas como em fila.  
  
#### <a name="to-create-a-publication-that-supports-immediate-updating-subscriptions"></a>Para criar uma publicação que ofereça suporte a assinaturas de atualização imediatas  
  
1.  Se necessário, crie um trabalho do Log Reader Agent para o banco de dados de publicação.  
  
    -   Se já existir um trabalho do Agente de Leitor de Log para o banco de dados de publicação, passe para a etapa 2.  
  
    -   Se você não estiver seguro quanto à existência de um trabalho do Agente do Leitor de Log para um banco de dados publicado, execute [sp_helplogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) no Publicador do banco de dados de publicação. Se o conjunto de resultados estiver vazio, será preciso criar um trabalho do Log Reader Agent.  
  
    -   No publicador, execute [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md). Especifique as credenciais do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows com as quais o agente é executado para **@job_name** e **@password** . Se o agente usar autenticação do SQL Server ao se conectar ao Publicador, será necessário especificar também um valor **0** para **@publisher_security_mode** e as informações de logon do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para **@publisher_login** e **@publisher_password** .  
  
2.  Execute [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), especificando um valor de **true** para o parâmetro **@allow_sync_tran** .  
  
3.  No Publicador, execute [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especifique o nome da publicação usado na etapa 2 para **@publication** e as credenciais do Windows com as quais o Snapshot Agent será executado para **@job_name** e **@password** . Se o agente usar autenticação do SQL Server ao se conectar ao Publicador, será necessário especificar também um valor **0** para **@publisher_security_mode** e as informações de logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para **@publisher_login** e **@publisher_password** . Isso cria um trabalho do Agente de Instantâneo para a publicação.  
  
4.  Adicione artigos à publicação. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
5.  No Assinante, crie uma assinatura de atualização para essa publicação.   
  
#### <a name="to-create-a-publication-that-supports-queued-updating-subscriptions"></a>Para criar uma publicação que ofereça suporte a assinaturas de atualização em fila  
  
1.  Se necessário, crie um trabalho do Log Reader Agent para o banco de dados de publicação.  
  
    -   Se já existir um trabalho do Agente de Leitor de Log para o banco de dados de publicação, passe para a etapa 2.  
  
    -   Se você não estiver seguro quanto à existência de um trabalho do Agente do Leitor de Log para um banco de dados publicado, execute [sp_helplogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) no Publicador do banco de dados de publicação. Se o conjunto de resultados estiver vazio, será preciso criar um trabalho do Log Reader Agent.  
  
    -   No publicador, execute [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md). Especifique as credenciais do Windows sob as quais o agente será executado para **@job_name** e **@password** . Se o agente usar autenticação do SQL Server ao se conectar ao Publicador, será necessário especificar também um valor **0** para **@publisher_security_mode** e as informações de logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para **@publisher_login** e **@publisher_password** .  
  
2.  Se necessário, crie um trabalho do Queue Reader Agent para o Distribuidor.  
  
    -   Se já houver um trabalho do Queue Reader Agent para o banco de dados da distribuição, passe para a Etapa 3.  
  
    -   Se você não estiver seguro quando à existência do trabalho do Queue Reader Agent no banco de dados da distribuição, execute [sp_helpqreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql.md) no Distribuidor do banco de dados de distribuição. Se o conjunto de resultados estiver vazio, será preciso criar um trabalho do Queue Reader Agent.  
  
    -   Para o Distribuidor, execute [sp_addqreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md). Especifique as credenciais do Windows com as quais o agente é executado para **@job_name** e **@password** . Essas credenciais são usadas quando o Queue Reader Agent se conecta ao Publicador e ao Assinante. Para obter mais informações, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
3.  Execute [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), especificando um valor de **true** para o parâmetro **@allow_queued_tran** e um valor de **pub wins**, **sub reinit** ou **sub wins** para **@conflict_policy** .  
  
4.  No Publicador, execute [sp_addpublication_snapshot (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especifique o nome de publicação usado na etapa 3 para **@publication** e as credenciais do Windows com as quais o Snapshot Agent será executado para **@snapshot_job_name** e **@password** . Se o agente usar autenticação do SQL Server ao se conectar ao Publicador, será necessário especificar também um valor **0** para **@publisher_security_mode** e as informações de logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para **@publisher_login** e **@publisher_password** . Isso cria um trabalho do Agente de Instantâneo para a publicação.  
  
5.  Adicione artigos à publicação. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
6.  No Assinante, crie uma assinatura de atualização para essa publicação.  
  
#### <a name="to-change-the-conflict-policy-for-a-publication-that-allows-queued-updating-subscriptions"></a>Para alterar a política de conflito para uma publicação que permite assinatura de atualização em fila  
  
1.  No Publicador do banco de dados de publicação, execute [sp_changepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md). Especifique um valor de **conflict_policy** para **@property** , o modo de política de conflito desejado de **pub wins**, **sub reinit**ou **sub wins** para **@value** .  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 Esse exemplo cria uma publicação que oferece suporte às assinaturas pull imediatas e em fila.  
  
 [!code-sql[HowTo#sp_createtranupdatingpub](../../../relational-databases/replication/codesnippet/tsql/enable-updating-subscrip_1.sql)]  
  
## <a name="see-also"></a>Consulte Também  
 [Definir opções de resolução de conflitos de atualização na fila &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [Replicação Transacional](../../../relational-databases/replication/transactional/transactional-replication.md)   
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)   
 [Create an Updatable Subscription to a Transactional Publication](create-an-updatable-subscription-to-a-transactional-publication.md)   
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Usar sqlcmd com variáveis de script](../../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)  
  
  
