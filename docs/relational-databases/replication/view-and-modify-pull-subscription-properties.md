---
title: "Exibir e modificar propriedades de assinatura pull | Microsoft Docs"
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
  - "modificando assinaturas"
  - "exibindo propriedades de replicação"
  - "modificando propriedades de replicação, assinaturas pull"
  - "assinaturas pull [replicação do SQL Server], modificando"
  - "assinaturas [replicação do SQL Server], pull"
  - "assinaturas pull [replicação do SQL Server], propriedades"
  - "modificando assinaturas, SQL Server Management Studio"
ms.assetid: 1601e54f-86f0-49e8-b023-87a5d1def033
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Exibir e modificar propriedades de assinatura pull
  Este tópico descreve como exibir e modificar propriedades de assinatura pull no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)], ou RMO (Replication Management Objects).  
  
 **Neste tópico**  
  
-   **Para exibir e modificar propriedades de assinatura pull, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Exibir propriedades de assinatura pull do publicador ou assinante no **Propriedades de assinatura - \< publicador>: \< Banco_de_dados_de_publicação>** caixa de diálogo, disponível em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Há mais propriedades visíveis no Assinante, e as propriedades podem ser modificadas no Assinante. É igualmente possível exibir propriedades no Publicador, na guia **Todas as Assinaturas** , disponível no Replication Monitor. Para obter informações sobre como iniciar o Monitor de replicação, consulte [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
#### Para exibir propriedades de assinatura pull no Publicador do Management Studio  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Expanda a publicação apropriada, clique em uma assinatura e, em seguida, clique em **propriedades**.  
  
4.  Exiba as propriedades. Em seguida, clique em **OK**.  
  
#### Para exibir e modificar as propriedades de assinatura pull no Assinante do Management Studio  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, então, expanda a pasta **Assinaturas Locais** .  
  
3.  Clique em uma assinatura e, em seguida, clique em **propriedades**.  
  
4.  Modifique propriedades, se necessário, depois clique em **OK**.  
  
#### Para exibir propriedades de assinatura pull no Publicador do Replication Monitor  
  
1.  Expanda um Grupo do publicador no painel esquerdo do Replication Monitor, expanda um Publicador e, em seguida, clique em uma publicação.  
  
2.  Clique na guia **Todas as Assinaturas** .  
  
3.  Clique em uma assinatura e, em seguida, clique em **propriedades**.  
  
4.  Exiba as propriedades. Em seguida, clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 As assinaturas pull podem ser modificadas e suas propriedades acessadas programaticamente usando procedimentos armazenados de replicação. Os procedimentos armazenados usados dependem do tipo de publicação ao qual a assinatura pertence.  
  
#### Para visualizar as propriedades de uma assinatura pull para um instantâneo ou publicação transacional  
  
1.  No assinante, execute [sp_helppullsubscription](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md). Especifique **@publisher**, **@publisher_db**, e **@publication**. Isso retorna informações sobre a assinatura que é armazenada em tabelas do sistema no Assinante.  
  
2.  No assinante, execute [sp_helpsubscription_properties](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md). Especifique **@publisher**, **@publisher_db**, **@publication**, e um dos seguintes valores para **@publication_type**:  
  
    -   **0** -assinatura pertence a uma publicação transacional.  
  
    -   **1** -assinatura pertence a uma publicação de instantâneo.  
  
3.  No publicador, execute [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md). Especifique **@publication** e **@subscriber**.  
  
4.  No publicador, execute [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), especificando **@subscriber**. Isso exibe informações sobre o Assinante.  
  
#### Para alterar as propriedades de uma assinatura pull para um instantâneo ou publicação transacional  
  
1.  No assinante, execute [sp_change_subscription_properties](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md), especificando **@publisher**, **@publisher_db**, **@publication**, um valor de **0** (transacional) ou **1** (instantâneo) para **@publication_type**, a propriedade de assinatura sendo alterada **@property**, e o novo valor como **@value**.  
  
2.  (Opcional) No assinante no banco de dados de assinatura, execute [sp_changesubscriptiondtsinfo](../../relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql.md). Especifique a ID do trabalho do Distribution Agent para **@jobid**, e os seguintes serviços de DTS (Data Transformation) propriedades de pacote:  
  
    -   **@dts_package_name**  
  
    -   **@dts_package_password**  
  
    -   **@dts_package_location**  
  
     Isso altera as propriedades de pacote DTS de uma assinatura.  
  
    > [!NOTE]  
    >  O ID pode ser obtida por meio da execução de trabalho [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md).  
  
#### Para exibir as propriedades de uma assinatura pull para uma publicação de mesclagem  
  
1.  No assinante, execute [sp_helpmergepullsubscription](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md). Especifique **@publisher**, **@publisher_db**, e **@publication**.  
  
2.  No assinante, execute [sp_helpsubscription_properties](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md). Especifique **@publisher**, **@publisher_db**, **@publication**, e um valor de 2 para **@publication_type**.  
  
3.  No publicador, execute [sp_helpmergesubscription](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md) para exibir informações de assinatura. Para retornar informações sobre uma assinatura específica, você deve especificar **@publication**, **@subscriber**, e um valor de **recepção** para **@subscription_type**.  
  
4.  No publicador, execute [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), especificando **@subscriber**. Isso exibe informações sobre o Assinante.  
  
#### Para alterar as propriedades de uma assinatura pull para uma publicação de mesclagem  
  
1.  No assinante, execute [sp_changemergepullsubscription](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md). Especifique **@publication**, **@publisher**, **@publisher_db**, a propriedade de assinatura sendo alterada **@property**, e o novo valor como **@value**.  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 As classes RMO usadas para exibir ou modificar as propriedades da assinatura pull dependem do tipo de publicação em que a assinatura pull está inscrita.  
  
#### Para exibir ou modificar as propriedades de uma assinatura pull para um instantâneo ou publicação transacional  
  
1.  Criar uma conexão com o assinante usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.TransPullSubscription> classe.  
  
3.  Definir o <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, e <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> Propriedades.  
  
4.  Defina a conexão da etapa 1 para o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade.  
  
5.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de assinatura na etapa 3 foram definidas incorretamente ou a assinatura não existe no servidor.  
  
6.  (Opcional) Para alterar propriedades, defina um novo valor para uma da <xref:Microsoft.SqlServer.Replication.TransPullSubscription> propriedades que podem ser definidas e, em seguida, chame o <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método.  
  
7.  (Opcional) Para exibir as novas configurações, chame o <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> método para recarregar as propriedades do artigo.  
  
8.  Feche todas as conexões.  
  
#### Para exibir ou modificar as propriedades de uma assinatura pull de uma publicação de mesclagem  
  
1.  Criar uma conexão com o assinante usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergePullSubscription> classe.  
  
3.  Definir o <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, e <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> Propriedades.  
  
4.  Defina a conexão da etapa 1 para o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade.  
  
5.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de assinatura na etapa 3 foram definidas incorretamente ou a assinatura não existe no servidor.  
  
6.  (Opcional) Para alterar propriedades, defina um novo valor para uma da <xref:Microsoft.SqlServer.Replication.MergePullSubscription> propriedades que podem ser definidas e, em seguida, chame o <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método.  
  
7.  (Opcional) Para exibir as novas configurações, chame o <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> método para recarregar as propriedades do artigo.  
  
8.  Feche todas as conexões.  
  
## Consulte também  
 [Exibir informações e executar tarefas para uma assinatura & #40. Monitor de replicação e 41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [Práticas recomendadas em relação à segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  