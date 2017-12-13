---
title: "Criar e aplicar o instantâneo inicial | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], creating
- snapshot replication [SQL Server], initial snapshots
ms.assetid: 742727a1-5189-44ec-b3ae-6fd7aa1f5347
caps.latest.revision: "44"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6d9be4d647441a82413c908a5207adec8efdf3e4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="create-and-apply-the-initial-snapshot"></a>Criar e aplicar o instantâneo inicial
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Este tópico descreve como criar e aplicar o instantâneo inicial no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)] ou o RMO (Replication Management Objects). Publicações de mesclagem que usam filtros com parâmetros exigem um instantâneo de duas partes. Para obter mais informações, consulte [Criar um instantâneo para uma publicação de mesclagem com filtros com parâmetros](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
 **Neste tópico**  
  
-   **Para criar e aplicar o instantâneo inicial, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Por padrão, se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent está sendo executado, um instantâneo é gerado imediatamente pelo Agente de Instantâneo depois que a publicação seja criada com o Assistente para Nova Publicação. Por padrão, isso é então aplicado pelo Distribution Agent (para replicações transacionais e instantâneas) ou o Merge Agent (para assinaturas de mesclagem) para todas as assinaturas. Um instantâneo também pode ser gerado usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e o Replication Monitor. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
#### <a name="to-create-a-snapshot-in-management-studio"></a>Para criar um instantâneo no Management Studio  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Clique com o botão direito do mouse na publicação para a qual você quer criar um instantâneo e, então, clique em **Exibir Status do Snapshot Agent**.  
  
4.  Na caixa de diálogo **Exibir Status do Snapshot Agent – \<Publicação>**, clique em **Iniciar**.  
  
 Quando Snapshot Agent terminar de gerar o instantâneo, uma mensagem será exibida, tal como "[100%] Um instantâneo de 17 artigo(s) foi gerado."  
  
#### <a name="to-create-a-snapshot-in-replication-monitor"></a>Para criar um instantâneo no Replication Monitor  
  
1.  No Replication Monitor, expanda um Grupo do publicador no painel esquerdo e, depois, expanda um Publicador.  
  
2.  Clique com o botão direito do mouse na publicação para a qual você quer gerar um instantâneo e, então, clique em **Gerar Instantâneo**.  
  
3.  Para exibir o status do Snapshot Agent, clique na guia **Agentes** . Para obter informações mais detalhadas, clique com o botão direito do mouse no Snapshot Agent na grade e, então, clique em **Exibir Detalhes**.  
  
#### <a name="to-apply-a-snapshot"></a>Para aplicar um instantâneo  
  
1.  Depois que um instantâneo for gerado, ele é aplicado pela sincronização da assinatura com o Distribution Agent ou Merge Agent:  
  
    -   Se o agente é definido para ser executado continuamente (o padrão para replicação transacional), o instantâneo é automaticamente aplicado após ser gerado.  
  
    -   Se o agente tiver execução agendada, o instantâneo será aplicado na próxima execução agendada do agente.  
  
    -   Se o agente tiver execução sob demanda, o instantâneo será aplicado na próxima vez que você executar o agente.  
  
     Para obter mais informações sobre assinaturas de sincronização, consulte [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md) e [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Instantâneos iniciais podem ser criados de forma programada criando e executando um trabalho do Agente de Instantâneo ou executando o arquivo executável do Agente de Instantâneo de um arquivo em lote. Depois da geração de um instantâneo inicial, ele é transferido para e aplicado no Assinante quando a assinatura é sincronizada pela primeira vez. Se o Agente de Instantâneo for executado de um prompt de comando ou um arquivo em lote, será preciso executar novamente o agente sempre que o instantâneo existente se tornar inválido.  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
#### <a name="to-create-and-run-a-snapshot-agent-job-to-generate-the-initial-snapshot"></a>Para criar e executar um trabalho do Snapshot Agent a fim de gerar o instantâneo inicial  
  
1.  Crie uma publicação de instantâneo, transacional ou de mesclagem. Para obter mais informações, consulte [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
2.  Execute [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especifique **@publication** e os seguintes parâmetros:  
  
    -   **O @job_login, que especifica** as credenciais de Autenticação do Windows com as quais o Snapshot Agent é executado no Distribuidor.  
  
    -   **O @job_password**, que é a senha para as credenciais fornecidas pelo Windows.  
  
    -   (Opcional) Um valor **0** para **@publisher_security_mode** se o agente usar Autenticação do SQL Server ao se conectar ao Publicador. Nesse caso, deve-se especificar também a informação de logon da Autenticação do SQL Server para **@publisher_login** e **@publisher_password**.  
  
    -   (Opcional) Uma agenda de sincronização para o trabalho do Snapshot Agent. Para obter mais informações, consulte [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
    > [!IMPORTANT]  
    >  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
3.  Adicione artigos à publicação. Para obter mais informações, consulte [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
4.  No Publicador do banco de dados de publicação, execute [sp_startpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql.md), especificando o valor de **@publication** da etapa 1.  
  
#### <a name="to-run-the-snapshot-agent-to-generate-the-initial-snapshot"></a>Para executar o Snapshot Agent para gerar o instantâneo inicial.  
  
1.  Crie uma publicação de instantâneo, transacional ou de mesclagem. Para obter mais informações, consulte [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
2.  Adicione artigos à publicação. Para obter mais informações, consulte [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
3.  Do prompt de comando ou em um arquivo em lote, inicie o [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md) executando **snapshot.exe**, especificando os seguintes argumentos de linha de comando:  
  
    -   **-Publication**  
  
    -   **-Publisher**  
  
    -   **-Distributor**  
  
    -   **-PublisherDB**  
  
    -   **-ReplicationType**  
  
     Se você estiver usando Autenticação do SQL Server, deve-se também especificar os seguintes argumentos:  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** = **0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** = **0**  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Esse exemplo mostra como criar uma publicação transacional e adicionar um trabalho do Agente de Instantâneo para a nova publicação (usando variáveis de script **sqlcmd** ). O exemplo também inicia o trabalho.  
  
 [!code-sql[HowTo#sp_trangenerate_snapshot](../../relational-databases/replication/codesnippet/tsql/create-and-apply-the-ini_1.sql)]  
  
 Esse exemplo cria uma publicação de mesclagem e adiciona um trabalho do Snapshot Agent (usando variáveis **sqlcmd** ) para a publicação. Esse exemplo também inicia o trabalho.  
  
 [!code-sql[HowTo#sp_mergegenerate_snapshot](../../relational-databases/replication/codesnippet/tsql/create-and-apply-the-ini_2.sql)]  
  
 Os seguintes argumentos de linha de comando iniciam o Snapshot Agent para gerar o instantâneo para uma publicação de mesclagem.  
  
> [!NOTE]  
>  Quebras de linhas foram adicionadas para melhorar a legibilidade. Em um arquivo em lotes, devem ser feitos comandos em uma única linha.  
  
```  
  
REM -- Declare variables  
SET Publisher=%InstanceName%  
SET PublicationDB=AdventureWorks2012   
SET Publication=AdvWorksSalesOrdersMerge   
  
REM --Start the Snapshot Agent to generate the snapshot for AdvWorksSalesOrdersMerge.  
"C:\Program Files\Microsoft SQL Server\120\COM\SNAPSHOT.EXE" -Publication %Publication%   
-Publisher %Publisher% -Distributor %Publisher% -PublisherDB %PublicationDB%   
-ReplicationType 2 -OutputVerboseLevel 1 -DistributorSecurityMode 1  
  
```  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 O Agente de Instantâneo gera instantâneos depois da criação da publicação. É possível gerar esses instantâneos de forma programada usando o RMO (Replication Management Objects) e o acesso de código direto para as funcionalidades do agente de replicação. Os objetos usados dependem do tipo de replicação. O Snapshot Agent pode ser iniciado usando o objeto <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> ou usando de forma assíncrona o trabalho do agente. Depois da geração do instantâneo inicial, ele é transferido para o Assinante, onde é aplicado quando a assinatura é sincronizada pela primeira vez. Será necessário executar novamente o agente sempre que o instantâneo existente não mais contiver dados válidos e atualizados. Para obter mais informações, consulte [Maintain Publications](../../relational-databases/replication/publish/maintain-publications.md) (Manter publicações).  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for preciso armazenar credenciais, use os serviços [criptográficos](http://go.microsoft.com/fwlink/?LinkId=34733) fornecidos pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework do Windows.  
  
#### <a name="to-generate-the-initial-snapshot-for-a-snapshot-or-transactional-publication-by-starting-the-snapshot-agent-job-asynchronous"></a>Para gerar o instantâneo inicial de uma publicação de instantâneo ou transacional por meio da iniciação do trabalho do Snapshot Agent (assíncrono)  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransPublication> . Defina as propriedades <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> para a publicação, e a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> para a conexão criada na etapa 1.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para carregar as propriedades remanescentes do objeto. Se esse método retornar **false**, as propriedades de publicação na etapa 2 foram definidas incorretamente ou a publicação não existe.  
  
4.  Se o valor de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> for **false**, chame <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> para criar o trabalho do Snapshot Agent para essa publicação.  
  
5.  Chame o método <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> para iniciar o trabalho de agente que gera o instantâneo para essa publicação.  
  
6.  (Opcional) Quando o valor de <xref:Microsoft.SqlServer.Replication.TransPublication.SnapshotAvailable%2A> for **true**, o instantâneo estará disponível a Assinantes.  
  
#### <a name="to-generate-the-initial-snapshot-for-a-snapshot-or-transactional-publication-by-running-the-snapshot-agent-synchronous"></a>Para gerar o instantâneo inicial de uma publicação de instantâneo ou transacional por meio da execução do Snapshot Agent (síncrono)  
  
1.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> e defina as seguintes propriedades necessárias:  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> - nome do Publicador  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> - nome do banco de dados de publicação  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> - nome da publicação  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> - nome do Distribuidor  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> - um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> para usar a Autenticação do Windows para conexão com o Publicador ou um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> e valores de <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherLogin%2A> e <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherPassword%2A> para usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em conexões com o Publicador. A Autenticação do Windows é recomendável.  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> - valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> para usar a Autenticação do Windows para conexão com o Distribuidor ou um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> e valores de <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorLogin%2A> e <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorPassword%2A> para usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em conexões com o Distribuidor. A Autenticação do Windows é recomendável.  
  
2.  Defina um valor de <xref:Microsoft.SqlServer.Replication.ReplicationType.Transactional> ou <xref:Microsoft.SqlServer.Replication.ReplicationType.Snapshot> para <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> .  
  
#### <a name="to-generate-the-initial-snapshot-for-a-merge-publication-by-starting-the-snapshot-agent-job-asynchronous"></a>Para gerar o instantâneo inicial para uma publicação de mesclagem iniciando o trabalho do Snapshot Agent (assíncrono)  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePublication> . Defina as propriedades <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> para a publicação, e a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> para a conexão criada na etapa 1.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para carregar as propriedades remanescentes do objeto. Se esse método retornar **false**, as propriedades de publicação na etapa 2 foram definidas incorretamente ou a publicação não existe.  
  
4.  Se o valor de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> for **false**, chame <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> para criar o trabalho do Snapshot Agent para essa publicação.  
  
5.  Chame o método <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> para iniciar o trabalho de agente que gera o instantâneo para essa publicação.  
  
6.  (Opcional) Quando o valor de <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> for **true**, o instantâneo estará disponível a Assinantes.  
  
#### <a name="to-generate-the-initial-snapshot-for-a-merge-publication-by-running-the-snapshot-agent-synchronous"></a>Para gerar o instantâneo inicial de uma publicação de mesclagem pela execução do Snapshot Agent (síncrono)  
  
1.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> e defina as seguintes propriedades necessárias:  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> - nome do Publicador  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> - nome do banco de dados de publicação  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> - nome da publicação  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> - nome do Distribuidor  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> - um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> para usar a Autenticação do Windows para conexão com o Publicador ou um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> e valores de <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherLogin%2A> e <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherPassword%2A> para usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em conexões com o Publicador. A Autenticação do Windows é recomendável.  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> - valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> para usar a Autenticação do Windows para conexão com o Distribuidor ou um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> e valores de <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorLogin%2A> e <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorPassword%2A> para usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em conexões com o Distribuidor. A Autenticação do Windows é recomendável.  
  
2.  Defina um valor de <xref:Microsoft.SqlServer.Replication.ReplicationType.Merge> para <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> .  
  
###  <a name="PShellExample"></a> Exemplos (RMO)  
 Esse exemplo executa o Agente de Instantâneo sincronicamente para gerar o instantâneo inicial para uma publicação transacional.  
  
 [!code-cs[HowTo#rmo_GenerateSnapshot](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_generatesnapshot)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_generatesnapshot)]  
  
 Esse exemplo inicia de forma assíncrona o trabalho do agente sincronicamente para gerar o instantâneo inicial para uma publicação transacional.  
  
 [!code-cs[HowTo#rmo_GenerateSnapshot_WithJob](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_generatesnapshot_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot_WithJob](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_generatesnapshot_withjob)]  
  
## <a name="see-also"></a>Consulte também  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Criar uma assinatura pull](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)   
 [Criar e aplicar o instantâneo](../../relational-databases/replication/create-and-apply-the-snapshot.md)   
 [Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Replication Management Objects Concepts](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Melhores práticas de segurança da replicação](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Replication System Stored Procedures Concepts](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Usar sqlcmd com variáveis de script](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)  
  
  
