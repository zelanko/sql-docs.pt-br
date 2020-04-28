---
title: Desabilitar publicação e distribuição | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- disabling publishing
- publishing [SQL Server replication], disabling
- distribution disabling [SQL Server replication]
- removing replication
- replication [SQL Server], removing
- disabling replication
- disabling distribution
ms.assetid: 6d4a1474-4d13-4826-8be2-80050fafa8a5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 682f015215218f362f0ca57557b9d6afb6edee08
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73882372"
---
# <a name="disable-publishing-and-distribution"></a>Desabilitar publicação e distribuição
  Este tópico descreve como desabilitar a publicação e a distribuição no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)]ou o RMO (Replication Management Objects).  
  
 É possível fazer o seguinte:  
  
-   Excluir todos os bancos de dados de distribuição no Distribuidor.  
  
-   Desabilitar todos os Publicadores que usam o Distribuidor e excluir todas as publicações nesses Publicadores.  
  
-   Excluir todas as assinaturas para as publicações. Os dados nos bancos de dados de publicação e de assinatura não serão excluídos, porém, eles perdem a sua relação de sincronização com qualquer banco de dados de publicação. Se quiser que os dados no Assinante sejam excluídos, eles deverão ser excluídos manualmente.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Pré-requisitos](#Prerequisites)  
  
-   **Para desabilitar a publicação e a distribuição, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
  
-   Para desabilitar a publicação e a distribuição, todos os bancos de dados de distribuição e publicação devem estar online. Se quaisquer *instantâneos de banco de dados* existirem para os bancos de dados de distribuição ou de publicação, eles devem ser descartados antes de desabilitar a publicação e a distribuição. O instantâneo do banco de dados é uma cópia offline somente leitura de um banco de dados e não está relacionado a nenhum instantâneo de replicação. Para obter mais informações, consulte [Instantâneos de banco de dados &#40;SQL Server&#41;](../databases/database-snapshots-sql-server.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Desabilite a publicação e a distribuição usando o Assistente para Desabilitar Publicação e Distribuição.  
  
#### <a name="to-disable-publishing-and-distribution"></a>Para desabilitar a publicação e a distribuição  
  
1.  Conecte-se ao Publicador ou Distribuidor que você quer desabilitar no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e então expanda o nó de servidor.  
  
2.  Clique com o botão direito do mouse na pasta **Replicação** e, então, clique em **Desabilitar Publicação e Distribuição**.  
  
3.  Complete as etapas no Assistente para Desabilitar Publicação e Distribuição.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 A publicação e a distribuição podem ser desabilitadas programaticamente usando procedimentos armazenados de replicação.  
  
#### <a name="to-disable-publishing-and-distribution"></a>Para desabilitar a publicação e a distribuição  
  
1.  Pare todos os trabalhos relacionados a replicação. Para uma relação de nomes de trabalho, consulte a seção "Segurança do Agente sob o SQL Server Agent" do [Modelo de Segurança do Agente de Replicação](security/replication-agent-security-model.md).  
  
2.  Em cada Assinante do banco de dados de assinatura, execute [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) para remover objetos de replicação do banco de dados. Esse procedimento armazenado não removerá trabalhos de replicação no Distribuidor.  
  
3.  No Publicador do banco de dados de publicação, execute [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) para remover objetos de replicação do banco de dados.  
  
4.  Se o Publicador usar um Distribuidor remoto, execute [sp_dropdistributor](/sql/relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql).  
  
5.  No Distribuidor, execute [sp_dropdistpublisher](/sql/relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql). Esse procedimento armazenado deverá ser executado uma vez para cada Publicador registrado no Distribuidor.  
  
6.  No Distribuidor, execute [sp_dropdistributiondb](/sql/relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql) para excluir o banco de dados de distribuição. Esse procedimento armazenado deverá ser executado uma vez para cada banco de dados de distribuição no Distribuidor. Isto também removerá qualquer trabalho do Queue Reader Agent associado com o banco de dados de distribuição.  
  
7.  No Distribuidor, execute [sp_dropdistributor](/sql/relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql) para remover a designação Distribuidor do servidor.  
  
    > [!NOTE]  
    >  Se todos os objetos de publicação e distribuição não forem descartados antes que você execute [sp_dropdistpublisher](/sql/relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql) e [sp_dropdistributor](/sql/relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql), estes procedimentos retornarão com um erro. Para descartar todos os objetos relacionados à replicação quando um Publicador ou distribuidor ** \@** é Descartado, o parâmetro no_checks deve ser definido como **1**. Se um Publicador ou distribuidor estiver offline ou inacessível, o ** \@parâmetro ignore_distributor** poderá ser definido como **1** para que eles possam ser descartados; no entanto, qualquer objeto de publicação e de distribuição deixado para trás deve ser removido manualmente.  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Este script de exemplo remove objetos de replicação do banco de dados de assinatura.  
  
 [!code-sql[HowTo#sp_removedbreplication](../../snippets/tsql/SQL15/replication/howto/tsql/dropdistpub.sql#sp_removedbreplication)]  
  
 Esse script de exemplo desabilita a publicação e a distribuição em um servidor que é um Publicador e Distribuidor e descarta o banco de dados de distribuição.  
  
 [!code-sql[HowTo#sp_DropDistPub](../../snippets/tsql/SQL15/replication/howto/tsql/dropdistpub.sql#sp_dropdistpub)]  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
  
#### <a name="to-disable-publishing-and-distribution"></a>Para desabilitar a publicação e a distribuição  
  
1.  Remova todas as assinaturas das publicações que usam o Distribuidor. Para obter mais informações, consulte [Delete a Pull Subscription](delete-a-pull-subscription.md) e [Delete a Push Subscription](delete-a-push-subscription.md).  
  
2.  Se o Publicador e o Distribuidor estiverem no mesmo servidor, remova todas as publicações que usam o Distribuidor e desabilite a publicação em todos os bancos de dados. Para obter mais informações, consulte [Delete a Publication](publish/delete-a-publication.md).  
  
3.  Crie uma conexão com o Distribuidor usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
4.  Criar uma instância da classe <xref:Microsoft.SqlServer.Replication.DistributionPublisher>. Especifique a propriedade <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> e passe o objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 3.  
  
5.  (Opcional) Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto e para verificar se o Publicador existe. Se esse método retornar `false`, o nome do Publicador definido na etapa 4 estava incorreto ou o Publicador não está sendo usado pelo Distribuidor.  
  
6.  Chame o método <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Remove%2A> . Passe um valor de `true` for *Force* se o Publicador e o distribuidor estiverem em servidores diferentes e quando o Publicador for desinstalado no distribuidor sem primeiro verificar se as publicações não existem mais no Publicador.  
  
7.  Criar uma instância da classe <xref:Microsoft.SqlServer.Replication.ReplicationServer>. Passe o objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 3.  
  
8.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationServer.UninstallDistributor%2A> . Passe um valor de `true` for *Force* para remover todos os objetos de replicação no distribuidor, sem primeiro verificar se todos os bancos de dados de publicação local foram desabilitados e se os bancos de dados de distribuição foram desinstalados.  
  
###  <a name="examples-rmo"></a><a name="PShellExample"></a> Exemplos (RMO)  
 Esse exemplo remove o registro do Publicador no Distribuidor, descarta o banco de dados de distribuição e desinstala o Distribuidor.  
  
 [!code-csharp[HowTo#rmo_DropDistPub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_dropdistpub)]  
  
 [!code-vb[HowTo#rmo_vb_DropDistPub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_dropdistpub)]  
  
 Esse exemplo desinstala o Distribuidor sem desabilitar primeiro os bancos de dados de publicação locais ou descartar o banco de dados de distribuição.  
  
 [!code-csharp[HowTo#rmo_DropDistPubForce](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_dropdistpubforce)]  
  
 [!code-vb[HowTo#rmo_vb_DropDistPubForce](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_dropdistpubforce)]  
  
## <a name="see-also"></a>Consulte Também  
 [Replication Management Objects Concepts](concepts/replication-management-objects-concepts.md)   
 [Replication System Stored Procedures Concepts](concepts/replication-system-stored-procedures-concepts.md)  
  
  
