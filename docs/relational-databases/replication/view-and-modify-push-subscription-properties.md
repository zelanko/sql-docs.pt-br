---
title: "Exibir e modificar propriedades de assinatura push | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "viewing replication properties"
  - "push subscriptions [SQL Server replication], properties"
  - "subscriptions [SQL Server replication], push"
  - "push subscriptions [SQL Server replication], modifying"
  - "modifying replication properties, push subscriptions"
  - "modificando assinaturas, SQL Server Management Studio"
ms.assetid: 801d2995-7aa5-4626-906e-c8190758ec71
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Exibir e modificar propriedades de assinatura push
  Este tópico descreve como exibir e modificar propriedades de assinatura push no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)] ou o RMO (Replication Management Objects).  
  
 **Neste tópico**  
  
-   **Para exibir e modificar propriedades de assinatura push, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Exibir e modificar as propriedades de assinatura push do Publicador em:  
  
-   O **Propriedades de assinatura - \< publicador>: \< Banco_de_dados_de_publicação>** caixa de diálogo, disponível em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   A guia **Todas as Assinaturas** que está disponível no Replication Monitor. Para obter informações sobre como iniciar o Monitor de replicação, consulte [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
#### Para exibir e modificar propriedades de assinatura push no Management Studio  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Expanda a publicação apropriada, clique em uma assinatura e, em seguida, clique em **propriedades**.  
  
4.  Modifique propriedades, se necessário, depois clique em **OK**.  
  
#### Para exibir e modificar propriedades de assinatura push no Replication Monitor  
  
1.  Expanda um Grupo do publicador no painel esquerdo do Replication Monitor, expanda um Publicador e, em seguida, clique em uma publicação.  
  
2.  Clique na guia **Todas as Assinaturas** .  
  
3.  Clique em uma assinatura e, em seguida, clique em **propriedades**.  
  
4.  Modifique propriedades, se necessário, depois clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 As assinaturas push podem ser modificadas e suas propriedades acessadas programaticamente usando procedimentos armazenados de replicação. Os procedimentos armazenados usados dependem do tipo de publicação ao qual a assinatura pertence.  
  
#### Para exibir as propriedades de uma assinatura push de um instantâneo ou publicação transacional  
  
1.  No publicador do banco de dados de publicação, execute [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md). Especifique **@publication**, **@subscriber**, e o valor **all** para **@article**.  
  
2.  No publicador do banco de dados de publicação, execute [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), especificando **@subscriber**.  
  
#### Para alterar as propriedades de uma assinatura push de um instantâneo ou publicação transacional  
  
1.  No publicador do banco de dados de publicação, execute [sp_changesubscriber](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md), especificando **@subscriber** e quaisquer parâmetros para as propriedades do assinante que está sendo alterados.  
  
2.  No publicador do banco de dados de publicação, execute [sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md). Especifique **@publication**, **@subscriber**, **@destination_db**, um valor de **todos os** para **@article**, a propriedade de assinatura sendo alterada **@property**, e o novo valor como **@value**. Isto altera as configurações de segurança para a assinatura push.  
  
3.  (Opcional) Para alterar as propriedades do pacote Data Transformation Services (DTS) de uma assinatura, execute [sp_changesubscriptiondtsinfo](../../relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql.md) no assinante no banco de dados de assinatura. Especifique o ID do trabalho do Distribution Agent para **@jobid** e as seguintes propriedades de pacote DTS:  
  
    -   **@dts_package_name**  
  
    -   **@dts_package_password**  
  
    -   **@dts_package_location**  
  
     Isso altera as propriedades de pacote DTS de uma assinatura.  
  
    > [!NOTE]  
    >  O ID pode ser obtida por meio da execução de trabalho [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md).  
  
#### Para exibir as propriedades de uma assinatura push de uma publicação de mesclagem  
  
1.  No publicador do banco de dados de publicação, execute [sp_helpmergesubscription](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md). Especifique **@publication** e **@subscriber**.  
  
2.  No publicador, execute [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), especificando **@subscriber**.  
  
#### Para alterar as propriedades de uma assinatura push de uma publicação de mesclagem  
  
1.  No publicador do banco de dados de publicação, execute [sp_changemergesubscription](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md). Especifique **@publication**, **@subscriber**, **@subscriber_db**, a propriedade de assinatura sendo alterada **@property**, e o novo valor como **@value**.  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 As classes RMO a serem usadas para exibir ou modificar as propriedades da assinatura push dependem do tipo de publicação em que a assinatura push está inscrita.  
  
#### Para exibir ou modificar as propriedades de uma assinatura push para um instantâneo ou publicação transacional  
  
1.  Criar uma conexão com o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.TransSubscription> classe.  
  
3.  Definir o <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, e <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> Propriedades.  
  
4.  Definir o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1 para o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> configuração de propriedade.  
  
5.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades da assinatura na etapa 3 foram definidas incorretamente ou a assinatura não existe.  
  
6.  (Opcional) Para alterar propriedades, defina um novo valor para uma da <xref:Microsoft.SqlServer.Replication.TransSubscription> propriedades que podem ser definidas e, em seguida, chame o <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método.  
  
7.  (Opcional) Para exibir as novas configurações, chame o <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> método para recarregar as propriedades da assinatura.  
  
#### Para exibir ou modificar as propriedades de uma assinatura push para uma publicação de mesclagem  
  
1.  Criar uma conexão com o assinante usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergeSubscription> classe.  
  
3.  Definir o <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, e <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> Propriedades.  
  
4.  Definir o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1 para o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> configuração de propriedade.  
  
5.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades da assinatura na etapa 3 foram definidas incorretamente ou a assinatura não existe.  
  
6.  (Opcional) Para alterar propriedades, defina um novo valor para uma da <xref:Microsoft.SqlServer.Replication.MergeSubscription> propriedades que podem ser definidas e, em seguida, chame o <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método.  
  
7.  (Opcional) Para exibir as novas configurações, chame o <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> método para recarregar as propriedades da assinatura.  
  
## Consulte também  
 [Exibir informações e executar tarefas para uma assinatura & #40. Monitor de replicação e 41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [Práticas recomendadas em relação à segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  