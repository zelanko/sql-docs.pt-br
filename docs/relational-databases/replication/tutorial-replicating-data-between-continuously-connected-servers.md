---
title: 'Tutorial: Configurar a replicação transacional'
description: Este tutorial ensina a configurar a replicação transacional entre dois SQL Servers totalmente conectados.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- tutorials [SQL Server replication]
- replication [SQL Server], tutorials
- wizards [SQL Server replication]
ms.assetid: 7b18a04a-2c3d-4efe-a0bc-c3f92be72fd0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 603846718e4e21c7af8ee81d94210d12242c35c7
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75321923"
---
# <a name="tutorial-configure-replication-between-two-fully-connected-servers-transactional"></a>Tutorial: Configurar a replicação entre dois servidores totalmente conectados (transacional)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
A Replicação transacional é uma boa solução ao problema de movimentação de dados entre servidores que estão continuamente conectados. Como usar o Assistente de Replicação, você pode configurar e administrar uma topologia de replicação com facilidade. 

Este tutorial mostra como configurar uma topologia de Replicação transacional para servidores continuamente conectados. Para saber mais sobre como funciona a replicação transacional, veja a [visão geral da replicação transacional](https://docs.microsoft.com/sql/relational-databases/replication/transactional/transactional-replication). 
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
Este tutorial ensina você a publicar dados de um banco de dados para outro usando replicação transacional.  

Neste tutorial, você aprenderá a:
> [!div class="checklist"]
> * Criar um editor por meio da replicação transacional.
> * Criar um assinante para o editor transacional.
> * Validar a assinatura e a latência da medida.
  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tutorial é destinado a usuários que estão familiarizados com operações básicas de banco de dados, mas que possuem pouca experiência com replicação. Antes de iniciar este tutorial, você deve concluir o [Tutorial: Preparar o SQL Server para replicação](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md).  
  
Para concluir este tutorial, são necessários o SQL Server, o SSMS (SQL Server Management Studio) e um banco de dados do AdventureWorks:  
  
- No servidor do editor (origem), instale:  
  
   - Qualquer edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], exceto o SQL Server Express ou o SQL Server Compact. Estas edições não podem ser editores de replicação.   
   - O banco de dados de exemplo [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] . Para reforçar a segurança, os bancos de dados de exemplo não são instalados por padrão.  
  
- No servidor do assinante (destino), instale qualquer edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], exceto [!INCLUDE[ssEW](../../includes/ssew-md.md)]. [!INCLUDE[ssEW](../../includes/ssew-md.md)] não pode ser um assinante em uma replicação transacional.  
  
- Instale o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Instale o [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- Baixe o [banco de dados de exemplo do AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases). Para obter instruções sobre como restaurar um banco de dados no SSMS, veja [Como restaurar um banco de dados](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms). 
 
>[!NOTE]
> - A replicação não é compatível em instâncias do SQL Server que tenham um intervalo de mais de duas versões. Para saber mais, veja [Supported SQL Server Versions in Replication Topology](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/) (Versões do SQL Server compatíveis na topologia de replicação).
> - No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], é necessário conectar-se ao editor e ao assinante usando um logon que seja membro da função de servidor fixa **sysadmin**. Para saber mais sobre essa função, veja [Funções de nível de servidor](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/server-level-roles).  
  
  
**Tempo estimado para concluir este tutorial: 60 minutos**  
  
## <a name="configure-the-publisher-for-transactional-replication"></a>Configurar o editor para a replicação transacional
Nesta seção, você criará uma publicação transacional usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para publicar um subconjunto filtrado da tabela **Product** no banco de dados de exemplo do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Você também adicionará o logon do SQL Server usado pelo Distribution Agent à PAL (lista de acesso à publicação).


### <a name="create-a-publication-and-define-articles"></a>Criar uma publicação e definir artigos
1. Conecte-se ao editor no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e expanda o nó de servidor.  
  
2. Clique com o botão direito do mouse no **SQL Server Agent** e selecione **Iniciar**. O SQL Server Agent deve estar em execução antes da criação da publicação. Se essa etapa não iniciar o agente, você precisará fazer isso manualmente no SQL Server Configuration Manager. 
3. Expanda a pasta **Replicação**, clique com o botão direito do mouse na pasta **Publicações Locais** e selecione **Nova Publicação**. Essa etapa inicia o Assistente para Nova Publicação:  

   ![Seleções para iniciar o Assistente para Nova Publicação](media/tutorial-replicating-data-between-continuously-connected-servers/newpublication.png)
  
  
3. Na página **Banco de Dados de Publicação**, selecione [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] e, em seguida, **Avançar**.  
  
4. Na página **Tipo de Publicação**, selecione **Publicação transacional** e, em seguida, **Avançar**:  

   ![Página "Tipo de publicação" com o tipo de publicação selecionado](media/tutorial-replicating-data-between-continuously-connected-servers/tranrepl.png)
  
5. Na página **Artigos**, expanda o nó **Tabelas** e marque a caixa de seleção **Product**. Em seguida, expanda **Product** e desmarque as caixas de seleção ao lado de **ListPrice** e **StandardCost**. Selecione **Avançar**.  

   ![Página "Artigos", com artigos selecionados para publicação](media/tutorial-replicating-data-between-continuously-connected-servers/replarticles.png)
  
6. Na página **Filtrar Linhas da Tabela**, selecione **Adicionar**.   
  
7. Na caixa de diálogo **Adicionar Filtro**, selecione a coluna **SafetyStockLevel**. Selecione a seta para a direita para adicionar a coluna à cláusula WHERE da instrução filter da consulta de filtro. Em seguida, digite manualmente o modificador da cláusula WHERE da seguinte maneira:  
  
   ```sql  
   WHERE [SafetyStockLevel] < 500  
   ```
  
   ![Página "Filtrar fluxos de tabela" e caixa de diálogo "Adicionar Filtro"](media/tutorial-replicating-data-between-continuously-connected-servers/filter.png)
  
8. Selecione **OK** e, em seguida, selecione **Avançar**.  
  
9. Marque a caixa de seleção **Criar um instantâneo imediatamente e mantê-lo disponível para inicializar assinaturas** e selecione **Avançar**:  

   ![Página "Agente de instantâneo" com a caixa de seleção marcada](media/tutorial-replicating-data-between-continuously-connected-servers/snapshot.png)
  
10. Na página **Segurança do Agente**, desmarque a caixa de seleção **Usar as configurações de segurança do Agente de Instantâneo**.   
  
    Selecione **Configurações de segurança** para o Agente de Instantâneo. Insira <*Nome_do_Computador_do_Editor*> **\repl_snapshot** na caixa **Conta de Processo**, forneça a senha para essa conta e selecione **OK**.  

    ![Página "Segurança do Agente" e caixa de diálogo "Segurança do Agente de Instantâneo"](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagentsecurity.png)
  
12. Repita a etapa anterior para definir <*Nome_do_Computador_do_Editor*> **\repl_logreader** como a conta de processo do Agente de Leitor de Log. Depois, selecione **OK**.  

    ![Caixa de diálogo "Segurança do Agente de Leitor de Log" e página "Segurança do Agente"](media/tutorial-replicating-data-between-continuously-connected-servers/logreaderagentsecurity.png)   

  
13. Na página **Concluir o Assistente**, digite **AdvWorksProductTrans** na caixa **Nome da publicação** e selecione **Concluir**:  

    ![Página "Concluir o Assistente" com o nome da publicação](media/tutorial-replicating-data-between-continuously-connected-servers/advworksproducttrans.png)
  
14. Depois que a publicação for criada, selecione **Fechar** para concluir o assistente. 

Você poderá receber o erro a seguir se o SQL Server Agent não estiver em execução quando você tentar criar a publicação. Esse erro indica que a publicação foi criada com êxito, mas o Agente de Instantâneo não pôde ser iniciado. Se isso acontecer, você precisará iniciar o SQL Server Agent e, em seguida, iniciar o Agente de Instantâneo manualmente. A próxima seção fornece instruções. 

![Aviso de que o Agente de Instantâneo não conseguiu iniciar](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagenterror.png)
    
  
### <a name="view-the-status-of-snapshot-generation"></a>Exibir o status de geração do instantâneo  
  
1. Conecte-se ao editor no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó de servidor e depois expanda a pasta **Replicação**.  
  
2. Na pasta **Publicações Locais**, clique com o botão direito do mouse em **AdvWorksProductTrans** e, em seguida, selecione **Exibir Status do Agente de Instantâneo**:  
   ![Comando no menu de atalho para exibir o status do Agente de Instantâneo](media/tutorial-replicating-data-between-continuously-connected-servers/viewsnapshot.png)
  
3. O status atual do trabalho do Agente de Instantâneo para a publicação é exibido. Verifique se o trabalho de instantâneo teve êxito antes de continuar para a próxima seção.
          
Se o SQL Server Agent não estava em execução quando a publicação foi criada, você verá que o Agente de Instantâneo "nunca foi executado" ao verificar o Status do agente de Instantâneo da publicação. Se esse for o caso, selecione **Iniciar** para iniciar o Agente de Instantâneo: 

![Botão "Iniciar" e a alteração na mensagem de status para mostrar que o Agente de Instantâneo foi executado](media/tutorial-replicating-data-between-continuously-connected-servers/startsnapshotagent.png)
     
Se encontrar um erro aqui, confira [Solução de problemas de erro com o Agente de Instantâneo](troubleshoot-tran-repl-errors.md#find-errors-with-the-snapshot-agent).


  
### <a name="add-the-distribution-agent-login-to-the-pal"></a>Adicionar o logon Distribution Agent à PAL  
  
1. Conecte-se ao editor no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó de servidor e depois expanda a pasta **Replicação**.  
  
2. Na pasta **Publicações Locais**, clique com o botão direito do mouse em **AdvWorksProductTrans** e, em seguida, selecione **Propriedades**.  A caixa de diálogo **Propriedades da Publicação** é exibida.    
  
   a. Selecione a página **Lista de Acesso à Publicação** e **Adicionar**.  
   b. Na caixa de diálogo **Adicionar Acesso à Publicação**, selecione <*Nome_do_Computador_do_Editor*> **\repl_distribution** e selecione **OK**.
   
   ![Seleções para adicionar o logon à lista de acesso à publicação](media/tutorial-replicating-data-between-continuously-connected-servers/tranreplproperties.png)

Para saber mais, veja [Conceitos de programação de replicação](../../relational-databases/replication/concepts/replication-programming-concepts.md).  
  

## <a name="create-a-subscription-to-the-transactional-publication"></a>Criar uma assinatura na publicação Transacional
Nesta seção, você adicionará um assinante à Publicação criada anteriormente. Este tutorial usa um assinante remoto (NODE2\SQL2016), mas você também pode adicionar localmente ao editor. 

### <a name="create-the-subscription"></a>Criar a assinatura  
  
1. Conecte-se ao editor no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó de servidor e depois expanda a pasta **Replicação**.  
  
2. Na pasta **Publicações Locais**, clique com o botão direito do mouse na publicação **AdvWorksProductTrans** e, em seguida, selecione **Novas Assinaturas**. O Assistente para Nova Assinatura é iniciado: 
 
   ![Seleções para iniciar o Assistente para Nova Assinatura](media/tutorial-replicating-data-between-continuously-connected-servers/newsub.png)     
  
3. Na página **Publicação**, selecione **AdvWorksProductTrans** e, em seguida, **Avançar**:  

   ![Página "Publicação" com a publicação selecionada](media/tutorial-replicating-data-between-continuously-connected-servers/selectpub.png)
  
4. Na página **Local do Agente de Distribuição**, selecione **Executar todos os agentes no Distribuidor** e, em seguida, selecione **Avançar**.  Para saber mais sobre assinaturas pull e push, veja [Assinar publicações](https://docs.microsoft.com/sql/relational-databases/replication/subscribe-to-publications).

   ![Página "Local do Agente de Distribuição" com a opção selecionada para executar todos os agentes no distribuidor](media/tutorial-replicating-data-between-continuously-connected-servers/runagentsatdist.png)
  
5. Na página **Assinantes**, se o nome da instância de Assinante não for exibido, selecione **Adicionar Assinante** e, em seguida, **Adicionar Assinante do SQL Server** na lista suspensa. Essa etapa abre a caixa de diálogo **Conectar ao Servidor**. Insira o nome da instância de assinante e, em seguida, selecione **Conectar**.  
    
   Depois que o Assinante for adicionado, marque a caixa ao lado do nome de instância da assinatura. Em seguida, selecione **Novo Banco de Dados** em **Banco de Dados de Assinatura**.   

   ![Página "Assinantes" com as seleções para adicionar um servidor de assinante](media/tutorial-replicating-data-between-continuously-connected-servers/addsub.png)

7. A caixa de diálogo **Novo Banco de Dados** é exibida. Insira **ProductReplica** na caixa **Nome do banco de dados**, selecione **OK** e, em seguida, **Avançar**: 
  
   ![Inserindo um nome ao banco de dados de assinatura](media/tutorial-replicating-data-between-continuously-connected-servers/productreplica.png)
  
8. Na página **Segurança do Agente de Distribuição**, selecione o botão de reticências ( **...** ). Insira <*Nome_do_Computador_do_Editor*> **\repl_distribution** na caixa **Conta do processo**, insira a senha da conta, selecione **OK** e, em seguida, selecione **Avançar**.

   ![Informações da conta de distribuição na caixa de diálogo "Segurança do Agente de Distribuição"](media/tutorial-replicating-data-between-continuously-connected-servers/adddistaccount.png)
  
9. Selecione **Concluir** para aceitar os valores padrão nas páginas restantes e conclua o assistente.  
  
### <a name="set-database-permissions-at-the-subscriber"></a>Definir permissões de banco de dados no assinante  
  
1. Conecte-se ao assinante no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Expanda **Segurança**, clique com o botão direito do mouse em **Logons** e, em seguida, selecione **Novo Logon**.     
  
   a. Na página **Geral**, em **Nome de Logon**, selecione **Pesquisar** e adicione o logon a <*Subscriber_Machine_Name*> **\repl_distribution**.

   b. Na página **Mapeamentos de Usuário**, conceda o logon de associação **db_owner** ao banco de dados **ProductReplica**. 

   ![Seleções para configurar o logon no assinante](media/tutorial-replicating-data-between-continuously-connected-servers/loginforsub.png)

2. Selecione **OK** para fechar a caixa de diálogo **Novo Logon**. 

  
### <a name="view-the-synchronization-status-of-the-subscription"></a>Exibir o status da sincronização da assinatura  
  
1. Conectar ao Editor em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Expanda o nó de servidor e depois expanda a pasta **Replicação**.  
  
2. Na pasta **Publicações Locais**, expanda a publicação **AdvWorksProductTrans**, clique com o botão direito do mouse na assinatura no banco de dados **ProductReplica** e, em seguida, selecione **Exibir Status da Sincronização**. O status atual da sincronização da assinatura é exibido:

   ![Seleções para abrir a caixa de diálogo "Exibir Status da Sincronização"](media/tutorial-replicating-data-between-continuously-connected-servers/viewsyncstatus.png)
3. Se a assinatura não for visível sob **AdvWorksProductTrans**, selecione a tecla F5 para atualizar a lista.  
  
Para obter mais informações, consulte:  
- [Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
- [Criar uma assinatura push](../../relational-databases/replication/create-a-push-subscription.md)  
- [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  

## <a name="measure-replication-latency"></a>Medir a latência da replicação
Nesta seção, você usará os tokens de rastreamento para verificar se as alterações estão sendo replicadas para o assinante e para determinar a latência. Latência é o tempo necessário para que uma alteração feita no editor seja exibida no assinante.
  
1. Conectar ao Editor em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Expanda o nó de servidor, clique com o botão direito do mouse na pasta **Replicação** e, em seguida, selecione **Iniciar o Replication Monitor**:

   ![Comando "Iniciar o Monitor de replicação" no menu de atalho](media/tutorial-replicating-data-between-continuously-connected-servers/launchreplmonitor.png)

2. Expanda um grupo editor no painel esquerdo, expanda a instância de editor e, em seguida, selecione a publicação **AdvWorksProductTrans**.  
  
   a. Selecione a guia **Tokens de Rastreamento**.  
   b. Selecione **Inserir Rastreamento**.    
   c. Exibição de tempo decorrido para o token de rastreamento nas seguintes colunas: **Editor para Distribuidor**, **Distribuidor para Editor**, **Latência Total**. Um valor de **Pendente** indica que o token não alcançou determinado ponto.

   ![Informações para o token de rastreamento](media/tutorial-replicating-data-between-continuously-connected-servers/tracertoken.png)


Para obter mais informações, consulte: 
- [Medir a latência e validar as conexões para a replicação transacional](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)
- [Localizar erros com os agentes de replicação transacional](troubleshoot-tran-repl-errors.md)


## <a name="next-steps"></a>Próximas etapas
Você configurou com êxito o editor e o assinante para a replicação transacional. Agora você pode inserir, atualizar ou excluir dados da tabela **Product** no editor. Em seguida, você pode consultar a tabela **Product** no assinante para exibir as alterações replicadas. 

O próximo artigo ensinará como configurar a replicação de mesclagem:  

> [!div class="nextstepaction"]
> [Tutorial: Configurar a replicação entre um servidor e clientes móveis (mesclagem)](tutorial-replicating-data-with-mobile-clients.md)
