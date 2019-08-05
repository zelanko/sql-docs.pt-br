---
title: Criar e aplicar o instantâneo inicial | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], creating
- snapshot replication [SQL Server], initial snapshots
ms.assetid: 742727a1-5189-44ec-b3ae-6fd7aa1f5347
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 65d0b89dfc2862c63d9fbb8f81d4145aba9d391f
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768639"
---
# <a name="create-and-apply-the-initial-snapshot"></a>Criar e aplicar o instantâneo inicial
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
Este tópico descreve como criar e aplicar o instantâneo inicial no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)]ou o RMO (Replication Management Objects). Publicações de mesclagem que usam filtros com parâmetros exigem um instantâneo de duas partes. Para obter mais informações, consulte [Criar um instantâneo para uma publicação de mesclagem com filtros com parâmetros](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  Instantâneos são gerados pelo Agente de Instantâneo depois que uma publicação for criada. Eles podem ser gerados:  
  
-   Imediatamente. Por padrão, um instantâneo para uma publicação de mesclagem é gerado imediatamente depois que a publicação seja criada no Assistente para Nova Publicação.    
-   Em um momento agendado. Especifique um agendamento na página **Agente de Instantâneo** do Assistente para Nova Publicação ou ao usar procedimentos armazenados no RMO (Replication Management Object).    
-   Manualmente Execute o Agente de Instantâneo no prompt de comando ou de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações sobre a execução de agentes, consulte [Conceitos dos executáveis do Replication Agent](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) ou [Iniciar e interromper um Agente de Replicação &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
Para replicação de mesclagem, é gerado um instantâneo toda vez que o Agente de Instantâneo é executado. Para replicação transacional, a geração de instantâneo depende da configuração da propriedade de publicação de **immediate_sync**. Se a propriedade estiver definida como TRUE (padrão ao usar o Assistente para Nova Publicação), um instantâneo é gerado toda vez que o Agente de Instantâneo for executado e pode ser aplicado ao Assinante a qualquer momento. Se a propriedade estiver definida como FALSE (padrão ao usar **sp_addpublication**), o instantâneo só é gerado se uma assinatura nova for adicionada desde a última execução do Agente de Instantâneo; Assinantes devem esperar que o Agente de Instantâneo termine antes de poder sincronizar-se.  
  
Por padrão, quando são gerados instantâneos, eles são salvados na pasta de instantâneo padrão localizada no Distribuidor. Você também pode salvar os arquivos de instantâneo em mídia removível, como discos removíveis, CD-ROMs ou em locais diferentes da pasta padrão do instantâneo. Adicionalmente, você poderá comprimir os arquivos para que sejam mais fáceis de armazenar e transferir, e executar os scripts antes ou depois de o instantâneo ser aplicado ao Assinante. Para obter mais informações sobre essas opções, consulte [Snapshot Options](../../relational-databases/replication/snapshot-options.md).  
  
Se o instantâneo for uma publicação de mesclagem que usa filtros com parâmetros, o instantâneo será criado usando um processo de duas partes. Primeiro é criado um instantâneo do esquema que contém os scripts de replicação e o esquema dos objetos publicados, mas não os dados. Cada assinatura é então inicializada com um instantâneo que inclui os scripts e o esquema copiados do instantâneo do esquema e os dados pertencentes à partição de assinatura. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
Se o instantâneo for criado no Publicador e armazenado em um local padrão ou local alternativo de instantâneo, este poderá ser transferido ao Assinante e aplicado. O Agente de Distribuição (para replicação transacional ou de instantâneo) ou Agente de Mesclagem (para replicação de mesclagem) transferem o instantâneo e aplica o esquema e arquivos de dados ao banco de dados da assinatura no Assinante durante a sincronização inicial. Por padrão, a sincronização inicial acontecerá imediatamente depois que uma assinatura seja criada se você usar o Assistente para Nova Assinatura. Este comportamento é controlado pela opção **Inicializar Quando** na página **Inicializar Assinaturas** do assistente. Quando os instantâneos forem criados após a assinatura ser inicializada, eles não serão aplicados ao Assinante, a menos que a assinatura esteja marcada para reinicialização. Para obter mais informações, consulte [Reinicializar as assinaturas](../../relational-databases/replication/reinitialize-subscriptions.md).  
  
Após o Agente de Distribuição ou Agente de Mesclagem aplicar o instantâneo inicial, o agente propaga atualizações subsequentes e outras modificações de dados. Quando instantâneos são distribuídos e aplicados a Assinantes, só esses Assinantes que estão à espera de instantâneos iniciais ou novos são afetados. Outros Assinantes daquela publicação (aqueles que já estejam recebendo inserções, atualizações, exclusões ou outras modificações aos dados publicados) não serão afetados.  

Para exibir ou modificar o local padrão de pasta de instantâneo, consulte  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Modificar opções de instantâneo](../../relational-databases/replication/snapshot-options.md)  
  
-   Programação de Replicação e programação de RMO: [Configurar a publicação e a distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md)  

## <a name="default-snapshot-location"></a>Localização do instantâneo padrão

 Especifique o local de instantâneo padrão na página **Pasta de Instantâneo** do Assistente para Configurar Distribuição. Para obter mais informações sobre como usar o assistente, consulte [Configurar a publicação e a distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md). Se você criar uma publicação em um servidor que não esteja configurada como Distributor, especifique um local de instantâneo padrão na página **Pasta de Instantâneo** do Assistente para Novas Publicações. Para obter mais informações sobre como usar esse assistente, consulte [Criar uma publicação](../../relational-databases/replication/publish/create-a-publication.md).  
  
 Modifique o local do instantâneo padrão na página **Publicadores** da caixa de diálogo **Propriedades do Distribuidor – \<Distribuidor>** . Para obter mais informações, consulte [Exibir e modificar as propriedades do Distribuidor e do Publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md). Defina a pasta de instantâneo para cada publicação na caixa de diálogo **Propriedades da Publicação – \<Publicação>** . Para obter mais informações, consulte [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### <a name="modify-the-default-snapshot-location"></a>Modificar a localização do instantâneo padrão  
  
1.  Na página **Publicadores** da caixa de diálogo **Propriedades do Distribuidor – \<Distribuidor>** , clique no botão de propriedades ( **...** ) para o Publicador para o qual você deseja alterar a localização do instantâneo padrão.  
  
2.  Na caixa de diálogo **Propriedades do Publicador – \<Publisher>** , digite um valor para a propriedade **Pasta de Instantâneo Padrão**.  
  
    > [!NOTE]  
    >  O Snapshot Agent deve ter permissões de gravação para o diretório que você especificar, e o Distribution Agent ou Merge Agent devem ter permissões de leitura. Se as assinaturas pull forem usadas, será necessário especificar um diretório compartilhado como um caminho UNC, como \\\computername\snapshot. Para obter mais informações, consulte [Proteger a pasta de instantâneos](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="create-snapshot"></a>Criar instantâneo
Por padrão, se o SQL Server Agent estiver sendo executado, um instantâneo será gerado imediatamente pelo Agente de Instantâneo depois que a publicação seja criada com o Assistente para Nova Publicação. Por padrão, isso é então aplicado pelo Distribution Agent (para replicações transacionais e instantâneas) ou o Merge Agent (para assinaturas de mesclagem) para todas as assinaturas. Um instantâneo também pode ser gerado usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e o Replication Monitor. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor).  

### <a name="using-sql-server-management-studio"></a>Usando o SQL Server Management Studio

1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó de servidor.    
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .    
3.  Clique com o botão direito do mouse na publicação para a qual você quer criar um instantâneo e, então, clique em **Exibir Status do Snapshot Agent**.    
4.  Na caixa de diálogo **Exibir Status do Snapshot Agent – \<Publicação>** , clique em **Iniciar**.    
 Quando Snapshot Agent terminar de gerar o instantâneo, uma mensagem será exibida, tal como "[100%] Um instantâneo de 17 artigo(s) foi gerado."  
  
### <a name="in-replication-monitor"></a>No Replication Monitor  
  
1.  No Replication Monitor, expanda um Grupo do publicador no painel esquerdo e, depois, expanda um Publicador.    
2.  Clique com o botão direito do mouse na publicação para a qual você quer gerar um instantâneo e, então, clique em **Gerar Instantâneo**.    
3.  Para exibir o status do Snapshot Agent, clique na guia **Agentes** . Para obter informações mais detalhadas, clique com o botão direito do mouse no Snapshot Agent na grade e, então, clique em **Exibir Detalhes**.  

## <a name="using-transact-sql"></a>Usando Transact-SQL
Instantâneos iniciais podem ser criados de forma programada criando e executando um trabalho do Agente de Instantâneo ou executando o arquivo executável do Agente de Instantâneo de um arquivo em lote. Depois da geração de um instantâneo inicial, ele é transferido para e aplicado no Assinante quando a assinatura é sincronizada pela primeira vez. Se o Agente de Instantâneo for executado de um prompt de comando ou um arquivo em lote, será preciso executar novamente o agente sempre que o instantâneo existente se tornar inválido.  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  

1.  Crie uma publicação de instantâneo, transacional ou de mesclagem. Para obter mais informações, consulte [Criar uma assinatura](../../relational-databases/replication/publish/create-a-publication.md).  
  
2.  Execute [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especifique **@publication** e os seguintes parâmetros:  
  
    -   **O @job_login, que especifica** as credenciais de Autenticação do Windows com as quais o Snapshot Agent é executado no Distribuidor.  
  
    -   **O @job_password** , que é a senha para as credenciais fornecidas pelo Windows.  
  
    -   (Opcional) Um valor **0** para **@publisher_security_mode** se o agente usar Autenticação do SQL Server ao se conectar ao Publicador. Nesse caso, deve-se especificar também a informação de logon da Autenticação do SQL Server para **@publisher_login** e **@publisher_password** .  
  
    -   (Opcional) Uma agenda de sincronização para o trabalho do Snapshot Agent. Para obter mais informações, consulte [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
    > [!IMPORTANT]  
    >  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
3.  Adicione artigos à publicação. Para obter mais informações, consulte [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
4.  No Publicador do banco de dados de publicação, execute [sp_startpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql.md), especificando o valor de **@publication** da etapa 1.  
  
## <a name="apply-a-snapshot"></a>Aplicar um instantâneo  

### <a name="using-sql-server-management-studio"></a>Usando o SQL Server Management Studio
  
1.  Depois que um instantâneo for gerado, ele é aplicado pela sincronização da assinatura com o Distribution Agent ou Merge Agent:   
    -   Se o agente é definido para ser executado continuamente (o padrão para replicação transacional), o instantâneo é automaticamente aplicado após ser gerado.   
    -   Se o agente tiver execução agendada, o instantâneo será aplicado na próxima execução agendada do agente.    
    -   Se o agente tiver execução sob demanda, o instantâneo será aplicado na próxima vez que você executar o agente.  
  
     Para obter mais informações sobre assinaturas de sincronização, consulte [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md) e [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
###   <a name="use-transact-sql"></a>Usar o Transact-SQL  
 
1.  Crie uma publicação de instantâneo, transacional ou de mesclagem. Para obter mais informações, consulte [Criar uma assinatura](../../relational-databases/replication/publish/create-a-publication.md).  
  
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
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for preciso armazenar credenciais, use os serviços [criptográficos](https://go.microsoft.com/fwlink/?LinkId=34733) fornecidos pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework do Windows.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)   
 [Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Replication Management Objects Concepts](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Replication System Stored Procedures Concepts](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Usar sqlcmd com variáveis de script](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)  
  
  
