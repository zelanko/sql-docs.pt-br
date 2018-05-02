---
title: 'Tutorial: Configurar a replicação entre um servidor e clientes móveis (Mesclagem) | Microsoft Docs'
ms.custom: ''
ms.date: 04/03/2018
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: af673514-30c7-403a-9d18-d01e1a095115
caps.latest.revision: 24
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d9751b7adc3d2cd4169bcd6b3a174de720c05eb9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="tutorial-configure-replication-between-a-server-and-mobile-clients-merge"></a>Tutorial: Configurar a replicação entre um servidor e clientes móveis (Mesclagem)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
A replicação de mesclagem é uma boa solução para o problema de movimentação de dados entre um servidor central e clientes móveis que são conectados apenas ocasionalmente. Usando os assistentes de replicação, você pode configurar e administrar uma topologia de Replicação de Mesclagem com facilidade. Este tutorial mostra como você deve configurar uma topologia de replicação para clientes móveis.  Para obter mais informações sobre a Replicação de Mesclagem, consulte [Uma visão geral da Replicação de Mesclagem](https://docs.microsoft.com/en-us/sql/relational-databases/replication/merge/merge-replication)
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
Este Tutorial ensina você a usar a Replicação de Mesclagem para publicar dados de um banco de dados central para um ou mais usuários móveis, de forma que cada usuário obtenha um subconjunto dos dados filtrado exclusivamente. 

Neste tutorial, você aprenderá a:
> [!div class="checklist"]
> * Configurar um Publicador para a Replicação de Mesclagem
> * Adicionar um Assinante móvel à Publicação de Mesclagem
> * Sincronizar a assinatura com a Publicação de Mesclagem
  
## <a name="prerequisites"></a>Prerequisites  
Este Tutorial é destinado a usuários que estão familiarizados com operações fundamentais de bancos de dados, mas que têm pouca experiência com replicação. Antes de iniciar este Tutorial, é necessário concluir o [Tutorial: Preparando o servidor para replicação](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md).  
  
Para usar este tutorial, o sistema deve ter o SQL Server Management Studio e os seguintes componentes instalados:  
  
-   No servidor do Publicador (fonte):  
  
    -   Qualquer edição do SQL Server, exceto o SQL Server Express ou o SQL Server Compact. Essas edições não podem ser Publicadores de replicação.   
    -   O banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Para reforçar a segurança, os bancos de dados de exemplo não são instalados por padrão.  
  
-   Servidor de assinante (destino):  
  
    -   Qualquer edição do SQL Server, exceto o [!INCLUDE[ssEW](../../includes/ssew-md.md)]. [!INCLUDE[ssEW](../../includes/ssew-md.md)] . 

- Instalar o [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
- Instalar o [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).
- Baixar [Bancos de dados de exemplo do AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases). Para obter instruções sobre como restaurar um banco de dados no SSMS, consulte [Restaurando um banco de dados](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms).  
 
  
>[!NOTE]
> - Não há suporte para replicação em SQL Servers que têm um intervalo de mais de duas versões. Para obter mais informações, consulte [Versões do SQL compatíveis na topologia de replicação](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/).
> - No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], você deve se conectar ao Publicador e ao Assinante usando um logon que seja membro da função de servidor fixa **sysadmin** . Para obter mais informações sobre a função sysadmin, consulte [Funções de nível de servidor](https://docs.microsoft.com/en-us/sql/relational-databases/security/authentication-access/server-level-roles).  
  
  
**Tempo estimado para concluir este tutorial: 60 minutos.**  
  
## <a name="configure-a-publisher-for-merge-replication"></a>Configurar um Publicador para a Replicação de Mesclagem
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Nesta seção, você criará uma publicação de Mesclagem usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para publicar um subconjunto das tabelas **Employee**, **SalesOrderHeader** e **SalesOrderDetail** no banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Essas tabelas são filtradas com filtros de linha com parâmetros de modo que cada assinatura contenha uma partição exclusiva dos dados. Você também adicionará o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado pelo Agente de Mesclagem à PAL (lista de acesso à publicação).  
  
### <a name="create-merge-publication-and-define-articles"></a>Criar uma Publicação de Mesclagem e definir artigos  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó de servidor.  
  
2. Inicie o **SQL Server Agent** clicando com o botão direito do mouse no **Pesquisador de Objetos** e selecionando **Iniciar**. Se isso não iniciar o Agent, você precisará fazer isso manualmente no **SQL Server Configuration Manager**.  
3. Expanda a pasta **Replicação**, clique com o botão direito do mouse em **Publicações Locais** e selecione **Nova Publicação**.  O Assistente de Configuração de Publicação é iniciado:  

    ![Iniciar Assistente para Nova Publicação](media/tutorial-replicating-data-between-continuously-connected-servers/newpublication.png)
  
3.  Na página Banco de Dados de Publicação, selecione [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] e, em seguida, **Avançar**. 

      
4.  Na página Tipo de Publicação, selecione **Publicação de mesclagem** e, em seguida, **Avançar**.  
    A. Na página Tipos de Assinante, verifique se somente o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou posterior está selecionado e, em seguida, selecione **Avançar**: 

    ![Replicação de mesclagem](media/tutorial-replicating-data-with-mobile-clients/mergerpl.png)
  
   
6.  Na página Artigos, expanda o nó **Tabelas** e selecione as três seguintes tabelas: **Employee**, **SalesOrderHeader** e **SalesOrderDetail**. Selecione **Avançar**:  

    ![Mesclar artigos](media/tutorial-replicating-data-with-mobile-clients/mergearticles.png)

    >[!NOTE]
    > A tabela Employee contém uma coluna (OrganizationNode) que tem o tipo de dados hierarchyid, compatível apenas com a replicação no SQL 2017. Se estiver usando um build inferior ao SQL 2017, você verá uma mensagem na parte inferior da tela notificando da potencial perda de dados com o uso dessa coluna na replicação bidirecional. Para fins deste tutorial, essa mensagem pode ser ignorada. No entanto, esse tipo de dados não deve ser replicado em um ambiente de produção, a menos que você esteja usando um build compatível. Para obter mais informações sobre como replicar o tipo de dados hierarchyid, consulte [Usando colunas hierarchyid na replicação](https://docs.microsoft.com/en-us/sql/t-sql/data-types/hierarchyid-data-type-method-reference#using-hierarchyid-columns-in-replicated-tables)
    
  
7.  Na página Filtrar Linhas da Tabela, selecione **Adicionar** e, em seguida, **Adicionar Filtro**.  
  
8.  Na caixa de diálogo **Adicionar Filtro**, selecione **Funcionário (HumanResources)** em **Selecionar a tabela a ser filtrada**. Selecione a coluna **LoginID**, selecione a seta para a direita para adicionar a coluna à cláusula WHERE da consulta de filtro e modifique a cláusula WHERE da seguinte maneira:  
  
    ```sql 
    WHERE [LoginID] = HOST_NAME()  
    ```  
  
    A. Selecione **Uma linha desta tabela vai para apenas uma assinatura** e **OK**:  
 
    ![Adicionar Filtro](media/tutorial-replicating-data-with-mobile-clients/mergeaddfilter.png)

    
  
10. Na página **Filtrar Linhas da Tabela**, selecione **Funcionário (Recursos Humanos)**, **Adicionar** e, em seguida, **Adicionar Junção para Estender o Filtro Selecionado**.  
  
    A. Na caixa de diálogo **Adicionar Junção**, selecione **Sales.SalesOrderHeader** em **Tabela unida**. Selecione **Gravar a instrução de junção manualmente** e conclua a instrução de junção da seguinte maneira:  
  
    ```sql  
    ON [Employee].[BusinessEntityID] =  [SalesOrderHeader].[SalesPersonID] 
    ```  
  
    B. Em **Especificar opções de junção**, selecione **Chave exclusiva** e, em seguida, selecione **OK**:

    ![Adicionar junção ao filtro](media/tutorial-replicating-data-with-mobile-clients/mergeaddjoin.png)

  
13. Na página Filtrar Linhas da Tabela, selecione **SalesOrderHeader**, **Adicionar** e, em seguida, **Adicionar Junção para Estender o Filtro Selecionado**.  
  
    A. Na caixa de diálogo **Adicionar Junção** , selecione **Sales.SalesOrderDetail** sob **Tabela unida**.    
    B. Selecione **Usar o construtor para criar a instrução**.  
    c. Na caixa **Visualização**, confirme se a instrução de junção é da seguinte maneira:  
  
    ```sql  
    ON [SalesOrderHeader].[SalesOrderID] = [SalesOrderDetail].[SalesOrderID] 
    ```  
  
    d. Em **Especificar opções de junção**, selecione **Chave exclusiva** e, em seguida, selecione **OK**. Selecione **Avançar**: 

       ![Unir tabelas de Ordem de Venda](media/tutorial-replicating-data-with-mobile-clients/joinsalestables.png)
  
21. Selecione **Criar um instantâneo imediatamente**, desmarque a opção **Agendar o agente de instantâneo para ser executado nos seguintes horários** e selecione **Avançar**:  

    ![Criar um instantâneo imediatamente](media/tutorial-replicating-data-with-mobile-clients/snapshotagent.png)
  
22. Na página Segurança do Agente, selecione **Configurações de Segurança**, digite <*Publisher_Machine_Name>***\repl_snapshot** na caixa **Conta de processo**, forneça a senha dessa conta e, em seguida, selecione **OK**. Selecione **Avançar**:  

    ![Segurança do Snapshot Agent](media/tutorial-replicating-data-with-mobile-clients/snapshotagentsecurity.png)
  
23. Na página **Concluir o Assistente**, insira **AdvWorksSalesOrdersMerge** na caixa **Nome da publicação** e selecione **Concluir**:  

    ![Nomear replicação de mesclagem](media/tutorial-replicating-data-with-mobile-clients/namemergerepl.png)
  
24. Depois que a publicação for criada, selecione **Fechar**. No nó **Replicação** no **Pesquisador de Objetos**, clique com o botão direito do mouse em **Publicações Locais** e selecione **Atualizar** para exibir a nova Replicação de Mesclagem.  
  
### <a name="to-view-the-status-of-snapshot-generation"></a>Para exibir o status de geração do instantâneo  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó do servidor e depois expanda a pasta **Replicação** .  
  
2.  Na pasta Publicações Locais, clique com o botão direito do mouse em **AdvWorksSalesOrdersMerge** e, em seguida, selecione **Exibir Status do Agente de Instantâneo**:  

    ![Exibir status do Agente de Instantâneo](media/tutorial-replicating-data-with-mobile-clients/viewsnapshotagentstatus.png)
  
3.  O status atual do trabalho do Snapshot Agent para a publicação é exibido. Certifique-se de que o trabalho de instantâneo teve sucesso antes de passar à próxima lição.  
  
### <a name="to-add-the-merge-agent-login-to-the-pal"></a>Para adicionar o logon do Merge Agent à PAL  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó do servidor e depois expanda a pasta **Replicação** .  
  
2.  Na pasta Publicações Locais, clique com o botão direito do mouse em **AdvWorksSalesOrdersMerge** e, em seguida, selecione **Propriedades**.  
  
    A. Selecione a página **Lista de Acesso à Publicação** e **Adicionar**. 
  
    B. Na caixa de diálogo Adicionar Acesso à Publicação, selecione <*Publisher_Machine_Name>***\repl_merge** e selecione **OK**. Selecione **OK**: 

    ![Mesclar PAL](media/tutorial-replicating-data-with-mobile-clients/mergepal.png) 

  
**Consulte também**:  
[Filtrar os dados publicados](../../relational-databases/replication/publish/filter-published-data.md)  
[Filtros de linha com parâmetros](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
[Defina um Artigo](../../relational-databases/replication/publish/define-an-article.md)  
  
  
## <a name="creating-a-subscription-to-the-merge-publication"></a>Criando uma assinatura na publicação de mesclagem
Nesta seção, você adicionará uma assinatura à Publicação de Mesclagem criada anteriormente. Este tutorial usa o assinante remoto (NODE2\SQL2016). Em seguida, definirá permissões no banco de dados da assinatura e gerará manualmente o instantâneo de dados filtrados para a nova assinatura.   
  
### <a name="add-a-subscriber-for-merge-publication"></a>Adicionar um Assinante à Publicação de Mesclagem
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó de servidor. Expanda a pasta **Replicação**, clique com o botão direito do mouse na pasta **Assinaturas Locais** e, em seguida, selecione **Novas Assinaturas** . O Assistente para Nova Assinatura é iniciado:

    ![Nova Assinatura](media/tutorial-replicating-data-with-mobile-clients/newsub.png)
  
2.  Na página **Publicação**, selecione **Encontrar Publicador do SQL Server** na lista **Publicador**.  
  
    A. Na caixa de diálogo **Conectar ao Servidor**, insira o nome da instância de Publicador na caixa **Nome do servidor** e selecione **Conectar**: 

    ![Adicionar um Publicador à publicação](media/tutorial-replicating-data-with-mobile-clients/publication.png)
  
4.  Selecione **AdvWorksSalesOrdersMerge** e **Avançar**.  
  
5.  Na página Local do Agente de Mesclagem, selecione **Executar cada agente em seu Assinante** e, em seguida, **Avançar**:  

    ![Assinatura pull](media/tutorial-replicating-data-with-mobile-clients/pullsub.png)
  
6.  Na página Assinantes, selecione o nome da instância do servidor Assinante e, em **Banco de Dados de Assinatura**, selecione **Novo Banco de Dados** na lista.  
  
    A. Na caixa de diálogo **Novo Banco de Dados**, insira **SalesOrdersReplica** na caixa **Nome do banco de dados**, selecione **OK** e, em seguida, **Avançar**: 

    ![Adicionar um BD ao sub](media/tutorial-replicating-data-with-mobile-clients/addsubdb.png)
  
8.  Na página Segurança do Agente de Mesclagem, selecione o botão de reticências (**…**), insira <*Subscriber_Machine_Name>***\repl_merge** na caixa **Conta de processo** e forneça a senha dessa conta. Em seguida, selecione **OK**, **Avançar** e **Avançar** novamente:  

    ![Segurança do Merge Agent](media/tutorial-replicating-data-with-mobile-clients/mergeagentsecurity.png)

9. No **Agendamento de Sincronização**, defina o **Agendamento do Agente** para **Executar somente sob demanda**. Selecione **Avançar**:  

    ![Agendamento de sincronização](media/tutorial-replicating-data-with-mobile-clients/mergesyncschedule.png)
  
9. Na página Inicializar Assinaturas, selecione **Na primeira sincronização** na lista **Inicializar Quando**, selecione **Avançar** e, em seguida, **Avançar** novamente: 

    ![Primeira sincronização](media/tutorial-replicating-data-with-mobile-clients/firstsync.png)

10. Na página Valores de HOST_NAME, insira um valor de **adventure-works\pamela0** na caixa **Valor de HOST_NAME** e selecione **Concluir**:  

    ![Nome_do_host](media/tutorial-replicating-data-with-mobile-clients/hostname.png)
  
11. Selecione **Concluir** novamente e, após a criação da assinatura, selecione **Fechar**.  

### <a name="setting-server-permissions-at-the-subscriber"></a>Definição de permissões de servidor no Assinante  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda **Segurança**, clique com o botão direito do mouse em **Logons** e, em seguida, selecione **Novo Logon**.  
  
    A. Na página **Geral**, selecione **Pesquisar** e, em seguida, insira <*Subscriber_ Machine_Name>***\repl_merge** no campo **Inserir o Nome do Objeto**. Em seguida, selecione **Verificar Nomes** e **OK**: 
    
    ![Logon no Assinante](media/tutorial-replicating-data-with-mobile-clients/sublogin.png)
  
1. Na página **Mapeamento de Usuário**, selecione o banco de dados **SalesOrdersReplica** e a função **db_owner**.  Na página **Protegíveis**, conceda a permissão "Explícita" para **Alterar Rastreamento**. Selecione **OK**:

    ![Definir o logon como DBO no Sub](media/tutorial-replicating-data-with-mobile-clients/setdbo.png)
  
### <a name="to-create-the-filtered-data-snapshot-for-the-subscription"></a>Para criar o instantâneo de dados filtrados para a assinatura  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó do servidor e depois expanda a pasta **Replicação** .  
  
2.  Na pasta **Publicações Locais**, clique com o botão direito do mouse na publicação **AdvWorksSalesOrdersMerge** e, em seguida, selecione **Propriedades**.  
   
    A. Selecione a página **Partições de Dados** e **Adicionar**.   
    B. Na caixa de diálogo **Adicionar Partição de Dados**, digite **adventure-works\pamela0** na caixa **Valor de HOST_NAME** e, em seguida, selecione **OK**.  
    c. Selecione a partição recém-adicionada, selecione **Gerar os instantâneos selecionados agora** e, em seguida, **OK**: 

    ![Adicionar partição](media/tutorial-replicating-data-with-mobile-clients/partition.png)
  
  
**Consulte também**:  
[Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
[Criar uma assinatura pull](../../relational-databases/replication/create-a-pull-subscription.md)  
[Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  

## <a name="synchronize-the-subscription-to-the-merge-publication"></a>Sincronizar a assinatura com a Publicação de Mesclagem

Nesta seção, você iniciará o Agente de Mesclagem para inicializar a assinatura usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você também usa este procedimento para sincronizar-se com o Publicador.   
  
### <a name="to-start-synchronization-and-initialize-the-subscription"></a>Para iniciar a sincronização e inicializar a assinatura  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
2. Verifique se o **SQL Server Agent** está em execução. Se não estiver, clique com o botão direito do mouse no **SQL Server Agent** no **Pesquisador de Objetos** e selecione **Iniciar**. Se isso não iniciar o Agent, você precisará fazer isso manualmente no **SQL Server Configuration Manager**. 
  
2.  Expanda o nó **Replicação**. Na pasta **Assinaturas Locais**, clique com o botão direito do mouse na assinatura no banco de dados **SalesOrdersReplica** e, em seguida, selecione **Exibir Status da Sincronização**.  
  
    A. Selecione **Iniciar** para inicializar a assinatura: 

    ![Status de sincronização](media/tutorial-replicating-data-with-mobile-clients/mergesyncstatus.png)
    
  
  
### <a name="next-steps"></a>Next Steps  
Você configurou com êxito o Publicador e o Assinante para a Replicação de Mesclagem.  Você também pode inserir, atualizar ou excluir dados nas tabelas **SalesOrderHeader** ou **SalesOrderDetail** no Publicador ou Assinante, repita esse procedimento quando a conectividade da rede estiver disponível para sincronizar dados entre o Publicador e o Assinante e, em seguida, consulte as tabelas **SalesOrderHeader** ou **SalesOrderDetail** no outro servidor para visualizar as alterações replicadas.  
  
**Consulte também**:   
[Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
[Sincronizar dados](../../relational-databases/replication/synchronize-data.md)  
[Sincronizar uma assinatura pull](../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
  
  
  
