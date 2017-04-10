---
title: "Inicializar uma assinatura manualmente | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "inicialização manual de assinaturas [replicação do SQL Server]"
  - "assinaturas [replicação do SQL Server], inicializando"
  - "inicializando assinaturas [replicação do SQL Server], sem instantâneos"
ms.assetid: 27a1bc38-e498-4fff-8082-04b52aa4b22c
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Inicializar uma assinatura manualmente
  Este tópico descreve como inicializar uma assinatura manualmente no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Embora o instantâneo inicial seja normalmente usado para inicializar uma assinatura, as assinaturas para publicações podem ser inicializadas sem o uso de um instantâneo, desde que o esquema e os dados iniciais já estejam presentes no assinante.  
  

##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Por exemplo, se houver atividade em um banco de dados publicado que usa replicação transacional entre a hora que os dados e o esquema são copiados no Assinante e a hora em que a assinatura é inicializada manualmente, talvez as alterações resultantes dessa atividade não sejam replicadas no Assinante.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Inicialize manualmente uma assinatura a uma publicação, copiando o esquema (e normalmente dados) ao banco de dados da assinatura. O esquema e os dados devem corresponder ao banco de dados de publicação. Então especifique que a assinatura não requer esquema e dados na página **Inicializar Assinaturas** do Assistente de Novas Assinaturas. Para obter mais informações sobre como acessar esse assistente, consulte [inicializar um transacional assinatura sem um instantâneo](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md) e [criar uma assinatura Pull](../../relational-databases/replication/create-a-pull-subscription.md).  
  
 Quando você sincroniza a assinatura pela primeira vez, os objetos e metadados exigidos pela replicação são copiados para o banco de dados da assinatura.  
  
#### Para inicializar manualmente uma assinatura para uma publicação.  
  
1.  Certifique-se que o esquema e dados são copiados para o banco de dados da assinatura.  
  
2.  Desmarque a caixa de seleção **Inicializar** na página **Inicializar Assinaturas** do Assistente para Novas Assinaturas. Faça isto para cada assinatura que exige apenas que objetos de replicação e metadados sejam copiados.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 As assinaturas podem ser inicializadas manualmente usando procedimentos de replicação armazenados.  
  
#### Para inicializar manualmente uma assinatura pull para uma publicação transacional  
  
1.  Certifique-se que o esquema e dados existam no banco de dados da assinatura. Para obter mais informações, consulte [inicializar um transacional assinatura sem um instantâneo](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
2.  No publicador do banco de dados de publicação, execute [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Especifique **@publication**, **@subscriber**, o nome do banco de dados no assinante que contém os dados publicados para **@destination_db**, um valor de **recepção** para **@subscription_type**, e um valor de **suporte somente à replicação** para **@sync_type**. Para obter mais informações, confira [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
3.  No Assinante, execute [sp_addpullsubscription](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md). Para assinaturas de atualização, consulte [criar uma assinatura atualizável em uma publicação transacional](https://technet.microsoft.com/library/ms152769(v=sql.130).aspx).  
  
4.  No Assinante, execute [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Para obter mais informações, confira [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
5.  Inicie o Distribution Agent para transferir objetos de replicação e baixe as alterações mais recentes do Publicador. Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
#### Para inicializar manualmente uma assinatura push para uma publicação transacional  
  
1.  Certifique-se que o esquema e dados existam no banco de dados da assinatura. Para obter mais informações, consulte [inicializar um transacional assinatura sem um instantâneo](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
2.  No publicador do banco de dados de publicação, execute [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Especifique o nome do banco de dados no assinante que contém os dados publicados para **@destination_db**, um valor de **push** para **@subscription_type**, e um valor de **suporte somente à replicação** para **@sync_type**. Para assinaturas de atualização, consulte [criar uma assinatura atualizável em uma publicação transacional](https://technet.microsoft.com/library/ms152769(v=sql.130).aspx).  
  
3.  No publicador do banco de dados de publicação, execute [sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Para obter mais informações, consulte [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
4.  Inicie o Distribution Agent para transferir objetos de replicação e baixe as alterações mais recentes do Publicador. Para obter mais informações, consulte [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
#### Para inicializar manualmente uma assinatura pull para uma publicação de mesclagem  
  
1.  Certifique-se que o esquema e dados existam no banco de dados da assinatura. Isso pode ser feito restaurando um backup do banco de dados de publicação no Assinante.  
  
2.  No publicador, execute [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md). Especifique **@publication**, **@subscriber**, **@subscriber_db**, e um valor de **recepção** para **@subscription_type**. Isso registra a assinatura pull.  
  
3.  No assinante no banco de dados que contém os dados publicados, execute [sp_addmergepullsubscription](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Especifique um valor de **nenhum** para **@sync_type**.  
  
4.  No assinante, execute [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md). Para obter mais informações, confira [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
5.  Inicie o Agente de Mesclagem para transferir objetos de replicação e baixe as alterações mais recentes do Publicador. Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
#### Para inicializar manualmente uma assinatura push para uma publicação de mesclagem  
  
1.  Certifique-se que o esquema e dados existam no banco de dados da assinatura. Isso pode ser feito restaurando um backup do banco de dados de publicação no Assinante.  
  
2.  No publicador do banco de dados de publicação, execute [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md). Especifique o nome do banco de dados no assinante que contém os dados publicados para **@subscriber_db**, um valor de **push** para **@subscription_type**, e um valor de **nenhum** para **@sync_type**.  
  
3.  No publicador do banco de dados de publicação, execute [sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md). Para obter mais informações, consulte [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
4.  Inicie o Agente de Mesclagem para transferir objetos de replicação e baixe as alterações mais recentes do Publicador. Para obter mais informações, consulte [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
## Consulte também  
 [Inicializar uma assinatura transacional sem um instantâneo](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)   
 [Fazer backup e restaurar bancos de dados replicados](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [Práticas recomendadas em relação à segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  