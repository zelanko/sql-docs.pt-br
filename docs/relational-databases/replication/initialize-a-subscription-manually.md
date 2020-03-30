---
title: Inicializar uma assinatura manualmente | Microsoft Docs
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
ms.assetid: 27a1bc38-e498-4fff-8082-04b52aa4b22c
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 85d4d245ae71adbd6b1c534381c7683b676d7fbe
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76288200"
---
# <a name="initialize-a-subscription-manually"></a>Inicializar uma assinatura manualmente
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Este tópico descreve como inicializar uma assinatura manualmente no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Embora o instantâneo inicial seja normalmente usado para inicializar uma assinatura, as assinaturas para publicações podem ser inicializadas sem o uso de um instantâneo, desde que o esquema e os dados iniciais já estejam presentes no assinante.  
  

##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Por exemplo, se houver atividade em um banco de dados publicado que usa replicação transacional entre a hora que os dados e o esquema são copiados no Assinante e a hora em que a assinatura é inicializada manualmente, talvez as alterações resultantes dessa atividade não sejam replicadas no Assinante.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Inicialize manualmente uma assinatura a uma publicação, copiando o esquema (e normalmente dados) ao banco de dados da assinatura. O esquema e os dados devem corresponder ao banco de dados de publicação. Então especifique que a assinatura não requer esquema e dados na página **Inicializar Assinaturas** do Assistente de Novas Assinaturas. Para mais informações sobre como acessar esse assistente, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md) e [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
 Quando você sincroniza a assinatura pela primeira vez, os objetos e metadados exigidos pela replicação são copiados para o banco de dados da assinatura.  
  
#### <a name="to-initialize-a-subscription-to-a-publication-manually"></a>Para inicializar manualmente uma assinatura para uma publicação.  
  
1.  Certifique-se que o esquema e dados são copiados para o banco de dados da assinatura.  
  
2.  Desmarque a caixa de seleção **Inicializar** na página **Inicializar Assinaturas** do Assistente para Novas Assinaturas. Faça isto para cada assinatura que exige apenas que objetos de replicação e metadados sejam copiados.  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 As assinaturas podem ser inicializadas manualmente usando procedimentos de replicação armazenados.  
  
#### <a name="to-manually-initialize-a-pull-subscription-to-a-transactional-publication"></a>Para inicializar manualmente uma assinatura pull para uma publicação transacional  
  
1.  Certifique-se que o esquema e dados existam no banco de dados da assinatura. Para obter mais informações, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
2.  No Publicador do banco de dados da publicação, execute [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Especifique **\@publication**, **\@subscriber**, o nome do banco de dados no Assinante que contém os dados publicados de **\@destination_db**, o valor **pull** para **\@subscription_type** e o valor **replication support only** para **\@sync_type**. Para obter mais informações, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
3.  No Assinante, execute [sp_addpullsubscription](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md). Para atualizar assinaturas, consulte [Create an Updatable Subscription to a Transactional Publication](https://technet.microsoft.com/library/ms152769(v=sql.130).aspx).  
  
4.  No Assinante, execute [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Para obter mais informações, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
5.  Inicie o Distribution Agent para transferir objetos de replicação e baixe as alterações mais recentes do Publicador. Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
#### <a name="to-manually-initialize-a-push-subscription-to-a-transactional-publication"></a>Para inicializar manualmente uma assinatura push para uma publicação transacional  
  
1.  Certifique-se que o esquema e dados existam no banco de dados da assinatura. Para obter mais informações, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
2.  No Publicador do banco de dados da publicação, execute [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Especifique o nome do banco de dados no Assinante que contém os dados publicados para **\@destination_db**, o valor **push** para **\@subscription_type** e o valor **replication support only** para **\@sync_type**. Para atualizar assinaturas, consulte [Create an Updatable Subscription to a Transactional Publication](https://technet.microsoft.com/library/ms152769(v=sql.130).aspx).  
  
3.  No Publicador do banco de dados de publicação, execute [sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Para obter mais informações, consulte [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
4.  Inicie o Distribution Agent para transferir objetos de replicação e baixe as alterações mais recentes do Publicador. Para obter mais informações, consulte [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
#### <a name="to-manually-initialize-a-pull-subscription-to-a-merge-publication"></a>Para inicializar manualmente uma assinatura pull para uma publicação de mesclagem  
  
1.  Certifique-se que o esquema e dados existam no banco de dados da assinatura. Isso pode ser feito restaurando um backup do banco de dados de publicação no Assinante.  
  
2.  No Publicador, execute [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md). Especifique **\@publication**, **\@subscriber**, **\@subscriber_db** e o valor **pull** para **\@subscription_type**. Isso registra a assinatura pull.  
  
3.  No Assinante, no banco de dados que contém os dados publicados, execute [sp_addmergepullsubscription](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Especifique o valor **none** para **\@sync_type**.  
  
4.  No Assinante, execute o [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md). Para obter mais informações, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
5.  Inicie o Agente de Mesclagem para transferir objetos de replicação e baixe as alterações mais recentes do Publicador. Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
#### <a name="to-manually-initialize-a-push-subscription-to-a-merge-publication"></a>Para inicializar manualmente uma assinatura push para uma publicação de mesclagem  
  
1.  Certifique-se que o esquema e dados existam no banco de dados da assinatura. Isso pode ser feito restaurando um backup do banco de dados de publicação no Assinante.  
  
2.  No Publicador, no banco de dados da publicação, execute [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md). Especifique o nome do banco de dados no Assinante que contém os dados publicados para **\@subscriber_db**, o valor **push** para **\@subscription_type** e o valor **none** para **\@sync_type**.  
  
3.  No Publicador, no banco de dados da publicação, execute [sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md). Para obter mais informações, consulte [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
4.  Inicie o Agente de Mesclagem para transferir objetos de replicação e baixe as alterações mais recentes do Publicador. Para obter mais informações, consulte [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)   
 [Fazer backup e restaurar bancos de dados replicados](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
