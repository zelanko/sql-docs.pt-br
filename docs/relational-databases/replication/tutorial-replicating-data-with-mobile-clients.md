---
title: 'Tutorial: Configurar a replicação entre um servidor e clientes móveis (mesclagem) | Microsoft Docs'
ms.custom: ''
ms.date: 04/03/2018
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
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
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4627eeb473ba1b2075ea4de12b0b5770e4f44447
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38983088"
---
# <a name="tutorial-configure-replication-between-a-server-and-mobile-clients-merge"></a>Tutorial: Configurar a replicação entre um servidor e clientes móveis (mesclagem)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
A replicação de mesclagem é uma boa solução para o problema de movimentação de dados entre um servidor central e clientes móveis que são conectados apenas ocasionalmente. Usando os assistentes de replicação, é possível configurar e administrar uma topologia de replicação de mesclagem com facilidade. 

Este tutorial mostra como você deve configurar uma topologia de replicação para clientes móveis. Para obter mais informações sobre a replicação de mesclagem, consulte a [visão geral da replicação de mesclagem](https://docs.microsoft.com/sql/relational-databases/replication/merge/merge-replication).
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
Este tutorial ensina você a usar a replicação de mesclagem para publicar dados de um banco de dados central para um ou mais usuários móveis, de forma que cada usuário obtenha um subconjunto dos dados filtrado exclusivamente. 

Neste tutorial, você aprenderá a:
> [!div class="checklist"]
> * Configurar um editor para a replicação de mesclagem.
> * Adicionar um assinante móvel à publicação de mesclagem.
> * Sincronizar a assinatura com a publicação de mesclagem.
  
## <a name="prerequisites"></a>Prerequisites  
Este tutorial é destinado a usuários familiarizados com operações fundamentais de bancos de dados, mas que têm pouca experiência com replicação. Antes de iniciar este tutorial, é necessário concluir o [Tutorial: Preparar o SQL Server para replicação](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md).  
  
Para concluir este tutorial, são necessários o SQL Server, o SSMS (SQL Server Management Studio) e um banco de dados do AdventureWorks: 
  
- No servidor do editor (origem), instale:  
  
   - Qualquer edição do SQL Server, exceto o SQL Server Express ou o SQL Server Compact. Essas edições não podem ser um editor de replicação.   
   - O banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Para reforçar a segurança, os bancos de dados de exemplo não são instalados por padrão.  
  
- No servidor do assinante (destino), instale qualquer edição do SQL Server, exceto para [!INCLUDE[ssEW](../../includes/ssew-md.md)]. A publicação criada neste tutorial não é compatível com [!INCLUDE[ssEW](../../includes/ssew-md.md)]. 

- Instalar o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Instale o [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).
- Baixe o [banco de dados de exemplo do AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases). Para obter instruções sobre como restaurar um banco de dados no SSMS, veja [Como restaurar um banco de dados](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms).  
 
  
>[!NOTE]
> - A replicação não é compatível em instâncias do SQL Server que tenham um intervalo de mais de duas versões. Para saber mais, veja [Supported SQL Server Versions in Replication Topology](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/) (Versões do SQL Server compatíveis na topologia de replicação).
> - No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], é necessário conectar-se ao editor e ao assinante usando um logon que seja membro da função de servidor fixa **sysadmin**. Para saber mais sobre essa função, veja [Funções de nível de servidor](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/server-level-roles).  
  
  
**Tempo estimado para concluir este tutorial: 60 minutos**  
  
## <a name="configure-a-publisher-for-merge-replication"></a>Configurar um editor para a replicação de mesclagem
Nesta seção, você criará uma publicação de mesclagem usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para publicar um subconjunto das tabelas **Employee**, **SalesOrderHeader** e **SalesOrderDetail** no banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Essas tabelas são filtradas com filtros de linha com parâmetros de modo que cada assinatura contenha uma partição exclusiva dos dados. Você também adicionará o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado pelo Agente de Mesclagem à PAL (lista de acesso à publicação).  
  
### <a name="create-merge-publication-and-define-articles"></a>Criar uma publicação de mesclagem e definir artigos  
  
1. Conecte-se ao editor no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e expanda o nó de servidor.  
  
2. Inicie o SQL Server Agent clicando com o botão direito do mouse no Pesquisador de Objetos e selecionando **Iniciar**. Se essa etapa não iniciar o agente, será necessário fazer isso manualmente no SQL Server Configuration Manager.  
3. Expanda a pasta **Replicação**, clique com o botão direito do mouse em **Publicações Locais** e selecione **Nova Publicação**. O Assistente para Nova Publicação é iniciado:  

   ![Seleções para iniciar o Assistente para Nova Publicação](media/tutorial-replicating-data-between-continuously-connected-servers/newpublication.png)
  
3. Na página **Banco de dados de publicação**, selecione [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] e, em seguida, selecione **Avançar**. 

      
4. Na página **Tipo de Publicação**, selecione **Publicação de mesclagem** e, em seguida, **Avançar**.  
   
5. Na página **Tipos de Assinante**, verifique se somente o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou posterior está selecionado e, em seguida, selecione **Avançar**: 

    ![Páginas "Tipo de publicação" e "Tipos de assinante"](media/tutorial-replicating-data-with-mobile-clients/mergerpl.png)
  
   
6. Na página **Artigos**, expanda o nó **Tabelas**. Selecione as três tabelas a seguir: **Employee**, **SalesOrderHeader** e **SalesOrderDetail**. Selecione **Avançar**.  

   ![Seleções de tabela na página "artigos"](media/tutorial-replicating-data-with-mobile-clients/mergearticles.png)

   >[!NOTE]
   > A tabela **Employee** contém uma coluna (**OrganizationNode**) que tem o tipo de dados **hierarchyid**. Esse tipo de dados é compatível com a replicação somente no SQL Server 2017. 
   >
   > Se estiver usando um build anterior ao SQL Server 2017, será exibida uma mensagem na parte inferior da tela para notificá-lo de potencial perda de dados por usar essa coluna na replicação bidirecional. Para os fins deste tutorial, é possível ignorar essa mensagem. No entanto, esse tipo de dados não deve ser replicado em um ambiente de produção, a menos que você esteja usando um build compatível.
   > 
   > Para obter mais informações sobre como replicar o tipo de dados **hierarchyid**, consulte [Using hierarchyid columns in replication](https://docs.microsoft.com/sql/t-sql/data-types/hierarchyid-data-type-method-reference#using-hierarchyid-columns-in-replicated-tables) (Usando colunas hierarchyid na replicação).
    
  
7. Na página **Filtrar Linhas da Tabela**, selecione **Adicionar** e, em seguida, **Adicionar Filtro**.  
  
8. Na caixa de diálogo **Adicionar Filtro**, selecione **Funcionário (HumanResources)** em **Selecionar a tabela a ser filtrada**. Selecione a coluna **LoginID**, selecione a seta para a direita para adicionar a coluna à cláusula WHERE da consulta de filtro e modifique a cláusula WHERE da seguinte maneira:  
  
   ```sql 
    WHERE [LoginID] = HOST_NAME()  
   ```  
  
   Selecione **Uma linha desta tabela vai para apenas uma assinatura** e **OK**.  
 
   ![Seleções para adicionar um filtro](media/tutorial-replicating-data-with-mobile-clients/mergeaddfilter.png)

    
  
10. Na página **Filtrar Linhas da Tabela**, selecione **Funcionário (Recursos Humanos)**, **Adicionar** e, em seguida, **Adicionar Junção para Estender o Filtro Selecionado**.  
  
    A. Na caixa de diálogo **Adicionar Junção**, selecione **Sales.SalesOrderHeader** em **Tabela unida**. Selecione **Gravar a instrução de junção manualmente** e conclua a instrução de junção da seguinte maneira:  
  
    ```sql  
    ON [Employee].[BusinessEntityID] =  [SalesOrderHeader].[SalesPersonID] 
    ```  
  
    B. Em **Especificar opções de junção**, selecione **Chave exclusiva** e, em seguida, selecione **OK**.

    ![Seleções para adicionar uma junção ao filtro](media/tutorial-replicating-data-with-mobile-clients/mergeaddjoin.png)

  
13. Na página **Filtrar Linhas da Tabela**, selecione **SalesOrderHeader**, **Adicionar** e, em seguida, **Adicionar Junção para Estender o Filtro Selecionado**.  
  
    A. Na caixa de diálogo **Adicionar Junção** , selecione **Sales.SalesOrderDetail** sob **Tabela unida**.    
    B. Selecione **Usar o construtor para criar a instrução**.  
    c. Na caixa **Visualização**, confirme se a instrução de junção é da seguinte maneira:  
  
    ```sql  
    ON [SalesOrderHeader].[SalesOrderID] = [SalesOrderDetail].[SalesOrderID] 
    ```  
  
    d. Em **Especificar opções de junção**, selecione **Chave exclusiva** e, em seguida, selecione **OK**. Selecione **Avançar**. 

    ![Seleções para adicionar outra junção para ordens de venda](media/tutorial-replicating-data-with-mobile-clients/joinsalestables.png)
  
21. Selecione **Criar um instantâneo imediatamente**, desmarque a opção **Agendar o agente de instantâneo para ser executado nos seguintes horários** e selecione **Avançar**:  

    ![Seleção para criar um instantâneo imediatamente](media/tutorial-replicating-data-with-mobile-clients/snapshotagent.png)
  
22. Na página **Segurança do Agente**, selecione **Configurações de Segurança**. Insira <*Nome_do_Computador_do_Editor*>**\repl_snapshot** na caixa **Conta de Processo**, forneça a senha para essa conta e selecione **OK**. Selecione **Avançar**.  

    ![Seleções para configurar a segurança do Agente de Instantâneo](media/tutorial-replicating-data-with-mobile-clients/snapshotagentsecurity.png)
  
23. Na página **Concluir o Assistente**, insira **AdvWorksSalesOrdersMerge** na caixa **Nome da publicação** e selecione **Concluir**:  

    ![Página "Concluir o Assistente" com o nome da publicação](media/tutorial-replicating-data-with-mobile-clients/namemergerepl.png)
  
24. Depois que a publicação for criada, selecione **Fechar**. No nó **Replicação** no **Pesquisador de Objetos**, clique com o botão direito do mouse em **Publicações Locais** e selecione **Atualizar** para exibir sua nova replicação de mesclagem.  
  
### <a name="view-the-status-of-snapshot-generation"></a>Exibir o status de geração do instantâneo  
  
1. Conecte-se ao editor no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó de servidor e depois expanda a pasta **Replicação**.  
  
2. Na pasta **Publicações Locais**, clique com o botão direito do mouse em **AdvWorksSalesOrdersMerge** e selecione **Exibir Status do Agente de Instantâneo**:  

   ![Seleções para exibir o status do Agente de Instantâneo](media/tutorial-replicating-data-with-mobile-clients/viewsnapshotagentstatus.png)
  
3. O status atual do trabalho do Agente de Instantâneo para a publicação é exibido. Certifique-se de que o trabalho de instantâneo teve sucesso antes de passar à próxima lição.  
  
### <a name="add-the-merge-agent-login-to-the-pal"></a>Adicionar o logon do Agente de Mesclagem à PAL  
  
1. Conecte-se ao editor no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó de servidor e depois expanda a pasta **Replicação**.  
  
2. Na pasta **Publicações Locais**, clique com o botão direito do mouse em **AdvWorksSalesOrdersMerge** e, em seguida, selecione **Propriedades**.  
  
   A. Selecione a página **Lista de Acesso à Publicação** e **Adicionar**. 
  
   B. Na caixa de diálogo **Adicionar Acesso à Publicação**, selecione <*Nome_do_Computador_do_Publicador*>**\repl_merge** e selecione **OK**. Selecione **OK** novamente. 

   ![Seleções para adicionar o logon do Agente de Mesclagem](media/tutorial-replicating-data-with-mobile-clients/mergepal.png) 

  
Para obter mais informações, consulte:  
- [Filtrar os dados publicados](../../relational-databases/replication/publish/filter-published-data.md) 
- [Filtros de linha com parâmetros](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
- [Definir um artigo](../../relational-databases/replication/publish/define-an-article.md)  
  
  
## <a name="create-a-subscription-to-the-merge-publication"></a>Criar uma assinatura para a publicação de mesclagem
Nesta seção, você adicionará uma assinatura à publicação de mesclagem criada anteriormente. Este tutorial usa o assinante remoto (NODE2\SQL2016). Em seguida, definirá permissões no banco de dados de assinatura e gerará manualmente o instantâneo de dados filtrados para a nova assinatura.   
  
### <a name="add-a-subscriber-for-merge-publication"></a>Adicionar um assinante à publicação de mesclagem
  
1. Conecte-se ao assinante no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e expanda o nó de servidor. Expanda a pasta **Replicação**, clique com o botão direito do mouse na pasta **Assinaturas Locais** e, em seguida, selecione **Novas Assinaturas** . O Assistente para Nova Assinatura é iniciado:

   ![Seleções para iniciar o Assistente para Nova Assinatura](media/tutorial-replicating-data-with-mobile-clients/newsub.png)
  
2. Na página **Publicação**, selecione **Encontrar Publicador do SQL Server** na lista **Publicador**.  
  
   Na caixa de diálogo **Conectar ao Servidor**, insira o nome da instância de Publicador na caixa **Nome do servidor** e selecione **Conectar**. 

   ![Seleções para adicionar um publicador](media/tutorial-replicating-data-with-mobile-clients/publication.png)
  
4. Selecione **AdvWorksSalesOrdersMerge** e **Avançar**.  
  
5. Na página **Local do Agente de Mesclagem**, selecione **Executar cada agente em seu Assinante** e, em seguida, selecione **Avançar**:  

   ![Opção "Executar cada agente em seu Assinante"](media/tutorial-replicating-data-with-mobile-clients/pullsub.png)
  
6. Na página **Assinantes**, selecione o nome da instância do servidor do assinante. Em **Banco de Dados de Assinatura**, selecione **Novo Banco de Dados** na lista.  
  
   Na caixa de diálogo **Novo Banco de Dados**, insira **SalesOrdersReplica** na caixa **Nome do banco de dados**. Selecione **OK**e selecione **Avançar**. 

   ![Seleções para adicionar um banco de dados ao assinante](media/tutorial-replicating-data-with-mobile-clients/addsubdb.png)
  
8. Na página **Segurança do Agente de Mesclagem**, selecione o botão de reticências (**...**). Digite <*Nome_do_Computador_do_Assinante*>**\repl_merge** na caixa **Conta de processo** e forneça a senha para essa conta. Selecione **OK**, **Avançar** e, em seguida, **Avançar** novamente.  

   ![Seleções para segurança do Agente de Mesclagem](media/tutorial-replicating-data-with-mobile-clients/mergeagentsecurity.png)

9. Na página **Agenda de Sincronização**, defina a **Agenda do Agente** como **Executar somente sob demanda**. Selecione **Avançar**.  

   ![Seleção "Executar somente sob demanda" para o agente](media/tutorial-replicating-data-with-mobile-clients/mergesyncschedule.png)
  
9. Na página **Inicializar Assinaturas**, selecione **Na primeira sincronização** da lista **Inicializar quando**. Selecione **Avançar** para ir para a página **Tipo de Assinatura** e, em seguida, selecione o tipo de assinatura adequado. Este tutorial usa o **Cliente**. Depois de selecionar o tipo de assinatura, selecione **Avançar** novamente. 

   ![Seleções para inicializar assinaturas na primeira sincronização](media/tutorial-replicating-data-with-mobile-clients/firstsync.png)

10. Na página **Valores de HOST_NAME**, insira um valor de **adventure-works\pamela0** na caixa **Valor de HOST_NAME**. Em seguida, selecione **Concluir**.  

    ![Página "Valores de HOST_NAME"](media/tutorial-replicating-data-with-mobile-clients/hostname.png)
  
11. Selecione **Concluir** novamente. Depois que a assinatura for criada, selecione **Fechar**.  

### <a name="set-server-permissions-at-the-subscriber"></a>Definir permissões de servidor no assinante  
  
1. Conecte-se ao assinante no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Expanda **Segurança**, clique com o botão direito do mouse em **Logons** e, em seguida, selecione **Novo Logon**.  
  
   Na página **Geral**, selecione **Pesquisar** e, em seguida, insira <*Nome_do_Computador_do_Assinante*>**\repl_merge** na caixa **Insira o Nome do Objeto**. Selecione **Verificar Nomes** e, em seguida, selecione **OK**. 
    
   ![Seleções para configurar o logon](media/tutorial-replicating-data-with-mobile-clients/sublogin.png)
  
1. Na página **Mapeamento de Usuário**, selecione o banco de dados **SalesOrdersReplica** e a função **db_owner**. Na página **Protegíveis**, conceda a permissão **Explícita** para **Alterar Rastreamento**. Escolha **OK**.

   ![Páginas "Mapeamento de usuário" e "Protegíveis"](media/tutorial-replicating-data-with-mobile-clients/setdbo.png)
  
### <a name="create-the-filtered-data-snapshot-for-the-subscription"></a>Criar o instantâneo de dados filtrados para a assinatura  
  
1. Conecte-se ao editor no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó de servidor e depois expanda a pasta **Replicação**.  
  
2. Na pasta **Publicações Locais**, clique com o botão direito do mouse na publicação **AdvWorksSalesOrdersMerge** e, em seguida, selecione **Propriedades**.  
   
   A. Selecione a página **Partições de Dados** e **Adicionar**.   
   B. Na caixa de diálogo **Adicionar Partição de Dados**, insira **adventure-works\pamela0** na caixa **Valor de HOST_NAME** e, em seguida, selecione **OK**.  
   c. Selecione a partição recém-adicionada, selecione **Gerar os instantâneos selecionados agora** e, em seguida, **OK**. 

   ![Seleções para adicionar uma partição](media/tutorial-replicating-data-with-mobile-clients/partition.png)
  
  
Para obter mais informações, consulte:  
- [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
- [Criar uma assinatura pull](../../relational-databases/replication/create-a-pull-subscription.md)  
- [Instantâneos para publicações de mesclagem com filtros com parâmetro](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  

## <a name="synchronize-the-subscription-to-the-merge-publication"></a>Sincronizar a assinatura com a publicação de mesclagem

Nesta seção, você iniciará o Agente de Mesclagem para inicializar a assinatura usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você também usará este procedimento para sincronizar-se com o publicador.   
  
### <a name="start-synchronization-and-initialize-the-subscription"></a>Iniciar a sincronização e inicializar a assinatura  
  
1. Conecte-se ao assinante no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
2. Certifique-se de que o SQL Server Agent está em execução. Se não estiver, clique com o botão direito do mouse no SQL Server Agent no Pesquisador de Objetos e selecione **Iniciar**. Se essa etapa não iniciar o agente, você precisará fazer isso manualmente usando o SQL Server Configuration Manager. 
  
2. Expanda o nó **Replicação**. Na pasta **Assinaturas Locais**, clique com o botão direito do mouse na assinatura no banco de dados **SalesOrdersReplica** e, em seguida, selecione **Exibir Status da Sincronização**.  
  
   Selecione **Iniciar** para inicializar a assinatura. 

   ![Status de sincronização com o botão "Iniciar"](media/tutorial-replicating-data-with-mobile-clients/mergesyncstatus.png)
    
  
  
## <a name="next-steps"></a>Próximas etapas  
Você configurou com sucesso seu publicador e seu assinante para sua replicação de mesclagem. Também é possível:

1. Inserir, atualizar ou excluir dados na tabela **SalesOrderHeader** ou **SalesOrderDetail** no publicador ou no assinante.
2. Repetir esse procedimento quando a conectividade de rede está disponível para sincronizar dados entre o publicador e o assinante.
3. Consultar a tabela **SalesOrderHeader** ou **SalesOrderDetail** no outro servidor para exibir as alterações replicadas.  
  
Para obter mais informações, consulte:   
- [Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
- [Sincronizar dados](../../relational-databases/replication/synchronize-data.md)  
- [Sincronizar uma assinatura pull](../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
  
  
  
