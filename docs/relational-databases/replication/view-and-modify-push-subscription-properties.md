---
description: Exibir e modificar propriedades de assinatura push
title: Exibir e modificar propriedades de assinatura push | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- viewing replication properties
- push subscriptions [SQL Server replication], properties
- subscriptions [SQL Server replication], push
- push subscriptions [SQL Server replication], modifying
- modifying replication properties, push subscriptions
- modifying subscriptions, SQL Server Management Studio
ms.assetid: 801d2995-7aa5-4626-906e-c8190758ec71
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016
ms.openlocfilehash: 006c577a6fd309ffb0aad25eab2cf5cc7261cb11
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97480917"
---
# <a name="view-and-modify-push-subscription-properties"></a>Exibir e modificar propriedades de assinatura push
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  Este tópico descreve como exibir e modificar propriedades de assinatura push no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)]ou o RMO (Replication Management Objects).  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]

  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Exibir e modificar as propriedades de assinatura push do Publicador em:  
  
-   A caixa de diálogo **Propriedades da Assinatura – \<Publisher>: \<PublicationDatabase>** que está disponível no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   A guia **Todas as Assinaturas** que está disponível no Replication Monitor. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
#### <a name="to-view-and-modify-push-subscription-properties-in-management-studio"></a>Para exibir e modificar propriedades de assinatura push no Management Studio  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó de servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Expanda a publicação apropriada, clique com o botão direito do mouse em uma assinatura e, então, clique em **Propriedades**.  
  
4.  Modifique propriedades, se necessário, depois clique em **OK**.  
  
#### <a name="to-view-and-modify-push-subscription-properties-in-replication-monitor"></a>Para exibir e modificar propriedades de assinatura push no Replication Monitor  
  
1.  Expanda um Grupo do publicador no painel esquerdo do Replication Monitor, expanda um Publicador e, em seguida, clique em uma publicação.  
  
2.  Clique na guia **Todas as Assinaturas** .  
  
3.  Clique com o botão direito do mouse em uma assinatura e clique em **Propriedades**.  
  
4.  Modifique propriedades, se necessário, depois clique em **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 As assinaturas push podem ser modificadas e suas propriedades acessadas programaticamente usando procedimentos armazenados de replicação. Os procedimentos armazenados usados dependem do tipo de publicação ao qual a assinatura pertence.  
  
#### <a name="to-view-the-properties-of-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>Para exibir as propriedades de uma assinatura push de um instantâneo ou publicação transacional  
  
1.  No Publicador do banco de dados da publicação, execute [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md). Especifique **\@publication**, **\@subscriber** e um valor igual a **all** em **\@article**.  
  
2.  No Publicador do banco de dados de publicação, execute [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), especificando **\@subscriber**.  
  
#### <a name="to-change-the-properties-of-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>Para alterar as propriedades de uma assinatura push de um instantâneo ou publicação transacional  
  
1.  No Publicador do banco de dados de publicação, execute [sp_changesubscriber](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md), especificando **\@subscriber** e os parâmetros para as propriedades do Assinante que está sendo alterado.  
  
2.  No Publicador do banco de dados de publicação, execute [sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md). Especifique **\@publication**, **\@subscriber**, **\@destination_db**, um valor igual a **all** em **\@article**, a propriedade da assinatura que está sendo alterada como **\@property** e o novo valor como **\@value**. Isto altera as configurações de segurança para a assinatura push.  
  
3.  (Opcional) Para alterar as propriedades do pacote DTS (Data Transformation Services) de uma assinatura, execute [sp_changesubscriptiondtsinfo](../../relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql.md) , do Assinante no banco de dados de assinatura. Especifique a ID do trabalho do Agente de Distribuição em **\@jobid** e as seguintes propriedades de pacote DTS:  
  
    -   **\@dts_package_name**  
  
    -   **\@dts_package_password**  
  
    -   **\@dts_package_location**  
  
     Isso altera as propriedades de pacote DTS de uma assinatura.  
  
    > [!NOTE]  
    >  O ID de trabalho pode ser obtido executando [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md).  
  
#### <a name="to-view-the-properties-of-a-push-subscription-to-a-merge-publication"></a>Para exibir as propriedades de uma assinatura push de uma publicação de mesclagem  
  
1.  No Publicador do banco de dados de publicação, execute [sp_helpmergesubscription](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md). Especifique **\@publication** e **\@subscriber**.  
  
2.  No Publicador, execute [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), especificando **\@subscriber**.  
  
#### <a name="to-change-the-properties-of-a-push-subscription-to-a-merge-publication"></a>Para alterar as propriedades de uma assinatura push de uma publicação de mesclagem  
  
1.  No Publicador do banco de dados de publicação, execute [sp_changemergesubscription](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md). Especifique **\@publication**, **\@subscriber**, **\@subscriber_db**, a propriedade da assinatura que está sendo alterada como **\@property** e o novo valor como **\@value**.  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> Exemplo (Transact-SQL)  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 As classes RMO a serem usadas para exibir ou modificar as propriedades da assinatura push dependem do tipo de publicação em que a assinatura push está inscrita.  
  
#### <a name="to-view-or-modify-properties-of-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>Para exibir ou modificar as propriedades de uma assinatura push para um instantâneo ou publicação transacional  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Criar uma instância da classe <xref:Microsoft.SqlServer.Replication.TransSubscription>.  
  
3.  Defina as propriedades <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>e <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> .  
  
4.  Defina a configuração da propriedade <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1 para o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de assinatura na etapa 3 foram definidas incorretamente ou a assinatura não existe.  
  
6.  (Opcional) Para alterar as propriedades, defina um novo valor para um das propriedades de <xref:Microsoft.SqlServer.Replication.TransSubscription> que podem ser definidas e depois chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> .  
  
7.  (Opcional) Para exibir as novas configurações, chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> para recarregar as propriedades para a assinatura.  
  
#### <a name="to-view-or-modify-properties-of-a-push-subscription-to-a-merge-publication"></a>Para exibir ou modificar as propriedades de uma assinatura push para uma publicação de mesclagem  
  
1.  Crie uma conexão com o Assinante usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Criar uma instância da classe <xref:Microsoft.SqlServer.Replication.MergeSubscription>.  
  
3.  Defina as propriedades <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>e <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> .  
  
4.  Defina a configuração da propriedade <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1 para o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de assinatura na etapa 3 foram definidas incorretamente ou a assinatura não existe.  
  
6.  (Opcional) Para alterar as propriedades, defina um novo valor para um das propriedades de <xref:Microsoft.SqlServer.Replication.MergeSubscription> que podem ser definidas e depois chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> .  
  
7.  (Opcional) Para exibir as novas configurações, chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> para recarregar as propriedades para a assinatura.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir informações e executar tarefas usando o Replication Monitor](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
