---
title: "Habilitar atualiza&#231;&#227;o de assinaturas para publica&#231;&#245;es transacionais | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "transactional replication, updatable subscriptions"
  - "updatable subscriptions, enabling"
  - "assinaturas [replicação do SQL Server], atualizáveis"
ms.assetid: 539d5bb0-b808-4d8c-baf4-cb6d32d2c595
caps.latest.revision: 42
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# Habilitar atualiza&#231;&#227;o de assinaturas para publica&#231;&#245;es transacionais
  Este tópico descreve como habilitar as assinaturas de atualização para publicações transacionais no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
> **OBSERVAÇÃO:** [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  

##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
 Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Habilite as assinaturas de atualização para publicações transacionais na página **Tipo de Publicação** do Assistente para Nova Publicação.  
  
 Para usar assinaturas de atualização, você deve configurar também as opções no Assistente para Nova Assinatura.  
  
#### Para habilitar assinaturas de atualização  
  
1.  Na página **Tipo de Publicação** do Assistente para Nova Publicação, selecione **Publicação transacional com assinaturas atualizáveis**.  
  
2.  Na página **Segurança do Agente** , especifique as definições do Queue Reader Agent além de Snapshot Agent e Log Reader Agent. Para obter mais informações sobre as permissões que são exigidas para a conta sob a qual o Queue Reader Agent executa, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
    > **Observação:** o Queue Reader Agent está configurado, mesmo se você usar apenas assinaturas de atualização imediata.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Ao criar uma publicação transacional de forma programática usando procedimentos armazenados de replicação, é possível ativar tanto as assinaturas de atualização imediatas como em fila.  
  
#### Para criar uma publicação que ofereça suporte a assinaturas de atualização imediatas  
  
1.  Se necessário, crie um trabalho do Log Reader Agent para o banco de dados de publicação.  
  
    -   Se já existir um trabalho do Agente de Leitor de Log para o banco de dados de publicação, passe para a etapa 2.  
  
    -   Se você não tiver certeza se um trabalho do Log Reader Agent existe para um banco de dados publicado, execute [sp_helplogreader_agent & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) o publicador do banco de dados de publicação. Se o conjunto de resultados estiver vazio, será preciso criar um trabalho do Log Reader Agent.  
  
    -   No publicador, execute [sp_addlogreader_agent & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md). Especifique o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] credenciais do Windows sob a qual o agente executa **@job_name** e **@password**. Se o agente usar autenticação do SQL Server ao se conectar ao Editor, você também deve especificar um valor de **0** para **@publisher_security_mode** e [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] informações de logon para **@publisher_login** e **@publisher_password**.  
  
2.  Executar [sp_addpublication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), especificando um valor de **true** para o parâmetro **@allow_sync_tran**.  
  
3.  No publicador, execute [sp_addpublication_snapshot & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especifique o nome da publicação usado na etapa 2 para **@publication** e as credenciais do Windows na qual o Snapshot Agent é executado para **@job_name** e **@password**. Se o agente usar autenticação do SQL Server ao se conectar ao Editor, você também deve especificar um valor de **0** para **@publisher_security_mode** e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] informações de logon para **@publisher_login** e **@publisher_password**. Isso cria um trabalho do Agente de Instantâneo para a publicação.  
  
4.  Adicione artigos à publicação. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
5.  No Assinante, crie uma assinatura de atualização para essa publicação.   
  
#### Para criar uma publicação que ofereça suporte a assinaturas de atualização em fila  
  
1.  Se necessário, crie um trabalho do Log Reader Agent para o banco de dados de publicação.  
  
    -   Se já existir um trabalho do Agente de Leitor de Log para o banco de dados de publicação, passe para a etapa 2.  
  
    -   Se você não tiver certeza se um trabalho do Log Reader Agent existe para um banco de dados publicado, execute [sp_helplogreader_agent & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) o publicador do banco de dados de publicação. Se o conjunto de resultados estiver vazio, será preciso criar um trabalho do Log Reader Agent.  
  
    -   No publicador, execute [sp_addlogreader_agent & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md). Especifique as credenciais do Windows na qual o agente é executado para **@job_name** e **@password**. Se o agente usar autenticação do SQL Server ao se conectar ao Editor, você também deve especificar um valor de **0** para **@publisher_security_mode** e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] informações de logon para **@publisher_login** e **@publisher_password**.  
  
2.  Se necessário, crie um trabalho do Queue Reader Agent para o Distribuidor.  
  
    -   Se já houver um trabalho do Queue Reader Agent para o banco de dados da distribuição, passe para a Etapa 3.  
  
    -   Se você não tiver certeza se um trabalho do Queue Reader Agent existe para o banco de dados de distribuição, execute [sp_helpqreader_agent & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql.md) no distribuidor no banco de dados de distribuição. Se o conjunto de resultados estiver vazio, será preciso criar um trabalho do Queue Reader Agent.  
  
    -   No distribuidor, execute [sp_addqreader_agent & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md). Especifique as credenciais do Windows na qual o agente é executado para **@job_name** e **@password**. Essas credenciais são usadas quando o Queue Reader Agent se conecta ao Publicador e ao Assinante. Para obter mais informações, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
3.  Executar [sp_addpublication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), especificando um valor de **true** para o parâmetro **@allow_queued_tran** e um valor de **wins pub**, **sub reinit**, ou **sub wins** para **@conflict_policy**.  
  
4.  No publicador, execute [sp_addpublication_snapshot (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especifique o nome da publicação usado na etapa 3 para **@publication** e as credenciais do Windows na qual o Snapshot Agent é executado para **@snapshot_job_name** e **@password**. Se o agente usar autenticação do SQL Server ao se conectar ao Editor, você também deve especificar um valor de **0** para **@publisher_security_mode** e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] informações de logon para **@publisher_login** e **@publisher_password**. Isso cria um trabalho do Agente de Instantâneo para a publicação.  
  
5.  Adicione artigos à publicação. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
6.  No Assinante, crie uma assinatura de atualização para essa publicação.  
  
#### Para alterar a política de conflito para uma publicação que permite assinatura de atualização em fila  
  
1.  No publicador do banco de dados de publicação, execute [sp_changepublication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md). Especifique um valor de **conflict_policy** para **@property** e o modo de política de conflito desejado de **wins pub**, **sub reinit**, ou **sub wins** para **@value**.  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 Esse exemplo cria uma publicação que oferece suporte às assinaturas pull imediatas e em fila.  
  
 [!code-sql[HowTo#sp_createtranupdatingpub](../../../relational-databases/replication/codesnippet/tsql/enable-updating-subscrip_1.sql)]  
  
## Consulte também  
 [Definir opções de resolução de conflito atualização na fila & #40. SQL Server Management Studio e 41;](../../../relational-databases/replication/publish/set-queued-updating-conflict-resolution-options-sql-server-management-studio.md)   
 [Tipos de publicação para Replicação Transacional](../../../relational-databases/replication/transactional/publication-types-for-transactional-replication.md)   
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Crie uma publicação](../../../relational-databases/replication/publish/create-a-publication.md)   
 [Criar uma assinatura atualizável em uma publicação transacional](https://msdn.microsoft.com/library/mt740635.aspx)   
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Usar sqlcmd com variáveis de script](../../../relational-databases/scripting/use-sqlcmd-with-scripting-variables.md)  
  
  