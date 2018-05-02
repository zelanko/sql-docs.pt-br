---
title: 'Tutorial: Configurar a replicação entre dois servidores totalmente conectados (Transacional) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- tutorials [SQL Server replication]
- replication [SQL Server], tutorials
- wizards [SQL Server replication]
ms.assetid: 7b18a04a-2c3d-4efe-a0bc-c3f92be72fd0
caps.latest.revision: 21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: de374f4372f62741ff3c49a9433cf339cecf3d26
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="tutorial-configure-replication-between-two-fully-connected-servers-transactional"></a>Tutorial: Configurar a replicação entre dois servidores totalmente conectados (Transacional)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
A Replicação Transacional é uma boa solução ao problema de movimentação de dados entre servidores que estão continuamente conectados. Usando o Assistente de Replicação, você pode configurar e administrar uma topologia de replicação com facilidade. Este tutorial mostra como configurar uma topologia de Replicação Transacional para servidores continuamente conectados. Para obter mais informações sobre como funciona a Replicação Transacional, consulte [Visão geral da Replicação Transacional](https://docs.microsoft.com/en-us/sql/relational-databases/replication/transactional/transactional-replication). 
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
Este tutorial mostrará a você como publicar dados de um banco de dados para outro usando replicação transacional. 

Neste tutorial, você aprenderá a:
> [!div class="checklist"]
> * Criar um publicador por meio da Replicação Transacional
> * Criar um assinante para o publicador Transacional
> * Validar a Assinatura e a latência da medida
> * Metodologia de solução de erros
  
  
## <a name="prerequisites"></a>Prerequisites  
Este tutorial é destinado a usuários que estão familiarizados com operações básicas de banco de dados, mas que possuem pouca experiência com replicação. Este tutorial exige a conclusão do tutorial anterior, [Preparando o servidor para replicação](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md).  
  
Para usar este Tutorial, o sistema deve ter o SSMS (SQL Server Management Studio) e estes componentes:  
  
-   No servidor do Publicador (fonte):  
  
    -   Qualquer edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], exceto o SQL Server Express ou o SQL Compact. Estas edições não podem ser Publicadores de replicação.   
    -   [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] banco de dados de exemplo. Para reforçar a segurança, os bancos de dados de exemplo não são instalados por padrão.  
  
-   Servidor de assinante (destino):  
  
    -   Qualquer edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], exceto [!INCLUDE[ssEW](../../includes/ssew-md.md)]. [!INCLUDE[ssEW](../../includes/ssew-md.md)] não pode ser um Assinante em uma replicação transacional.  
  
- Instalar o [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
- Instalar o [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).
- Baixar [Bancos de dados de exemplo do AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases). Para obter instruções sobre como restaurar um banco de dados no SSMS, consulte [Restaurando um banco de dados](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms). 
 
>[!NOTE]
> - Não há suporte para replicação em SQL Servers que têm um intervalo de mais de duas versões. Para obter mais informações, consulte [Versões do SQL compatíveis na topologia de replicação](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/).
> - No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], você deve se conectar ao Publicador e ao Assinante usando um logon que seja membro da função de servidor fixa **sysadmin** . Para obter mais informações sobre a função sysadmin, consulte [Funções de nível de servidor](https://docs.microsoft.com/en-us/sql/relational-databases/security/authentication-access/server-level-roles).  
  
  
**Tempo estimado para concluir este tutorial: 60 minutos.**  
  
## <a name="configure-the-publisher-for-transactional-replication"></a>Configurar o Publicador para a Replicação Transacional
Nesta seção, você criará uma publicação transacional usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para publicar um subconjunto filtrado da tabela **Product** no banco de dados de exemplo do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Você também adicionará o logon do SQL Server usado pelo Distribution Agent à PAL (lista de acesso à publicação). Antes de iniciar este tutorial, você deverá ter completado o tutorial anterior, [Preparando o servidor para replicação](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md).


### <a name="create-a-publication-and-define-articles"></a>Criar uma publicação e definir artigos
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó de servidor.  
  
2. Clique com o botão direito do mouse no **SQL Server Agent** e selecione **Iniciar**. O SQL Server Agent deve estar em execução antes da criação da publicação. Se isso não iniciar o agente, você precisará fazer isso manualmente no **SQL Server Configuration Manager**. 
3. Expanda a pasta **Replicação**, clique com o botão direito do mouse na pasta **Publicações Locais** e selecione **Nova Publicação**.  Isso iniciará o Assistente de Configuração de Publicação:  

    ![Nova publicação](media/tutorial-replicating-data-between-continuously-connected-servers/newpublication.png)
  
  
3. Na página Banco de Dados de Publicação, selecione [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] e, em seguida, **Avançar**.  
  
4. Na página Tipo de Publicação, selecione **Publicação transacional** e, em seguida, **Avançar**:  

    ![Replicação transacional](media/tutorial-replicating-data-between-continuously-connected-servers/tranrepl.png)
  
5. Na página Artigos, expanda o nó **Tabelas** e marque a caixa de seleção **Product**. Em seguida, expanda **Product** e desmarque as caixas de seleção ao lado de **ListPrice** e **StandardCost**. Selecione **Avançar**:  

    ![Artigos para publicação](media/tutorial-replicating-data-between-continuously-connected-servers/replarticles.png)
  
6. Na página Filtrar Linhas da Tabela, selecione **Adicionar**.   
  
7. Na caixa de diálogo **Adicionar Filtro**, selecione a coluna **SafetyStockLevel**, selecione a seta para a direita para adicionar a coluna à cláusula WHERE da instrução Filter da consulta de filtro. Em seguida, digite manualmente o modificador da cláusula WHERE da seguinte maneira:  
  
    ```sql  
    WHERE [SafetyStockLevel] < 500  
    ```
  
    ![Instrução de filtro](media/tutorial-replicating-data-between-continuously-connected-servers/filter.png)
  
8. Selecione **OK**e selecione **Avançar**.  
  
9. Marque a caixa de seleção **Criar um instantâneo imediatamente e mantê-lo disponível para inicializar assinaturas** e selecione **Avançar**:  

    ![Snapshot Agent](media/tutorial-replicating-data-between-continuously-connected-servers/snapshot.png)
  
10. Na página Segurança do Agente, desmarque a caixa de seleção **Usar as configurações de segurança do Agente de Instantâneo** .   
  
    A. Selecione **Configurações de Segurança** do Agente de Instantâneo, insira <*Publisher_Machine_Name>***\repl_snapshot** na caixa **Conta de processo**, forneça a senha dessa conta e, em seguida, selecione **OK**:  

    ![Segurança do Snapshot Agent](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagentsecurity.png)
  
12. Repita a etapa anterior para definir <*Publisher_Machine_Name*>**\repl_logreader** como a conta de processo do Agente de Leitor de Log e, em seguida, selecione **OK**:  

    ![Segurança do Log Reader Agent](media/tutorial-replicating-data-between-continuously-connected-servers/logreaderagentsecurity.png)   

  
13. Na página Concluir o Assistente, digite **AdvWorksProductTrans** na caixa **Nome da publicação** e selecione **Concluir**:  

    ![Nomear a publicação](media/tutorial-replicating-data-between-continuously-connected-servers/advworksproducttrans.png)
  
14. Depois que a publicação for criada, selecione **Fechar** para concluir o assistente. 

    Você poderá receber o erro a seguir se o SQL Server Agent não estiver em execução quando você tentar criar a publicação. Essa é uma indicação de que a publicação foi criada com êxito, mas o Agente de Instantâneo não pôde ser iniciado. Se isso acontecer, você precisará iniciar o SQL Server Agent e, em seguida, iniciar o Agente de Instantâneo manualmente. As instruções para resolver esse problema são abordadas na próxima seção: 

    ![O Agente de Instantâneo não pode ser iniciado](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagenterror.png)
    
  
### <a name="to-view-the-status-of-snapshot-generation"></a>Para exibir o status de geração do instantâneo  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó do servidor e depois expanda a pasta **Replicação** .  
  
2.  Na pasta **Publicações Locais**, clique com o botão direito do mouse em **AdvWorksProductTrans** e, em seguida, selecione **Exibir Status do Agente de Instantâneo**:  

    ![Status do Agente de Instantâneo](media/tutorial-replicating-data-between-continuously-connected-servers/viewsnapshot.png)
  
3.  O status atual do trabalho do Snapshot Agent para a publicação é exibido. Verifique se o trabalho de instantâneo teve êxito antes de continuar para a próxima seção.
          
    Se o SQL Server Agent não estava em execução quando a publicação foi criada pela primeira vez, você verá que o Agente de Instantâneo "nunca foi executado" ao verificar o **Status do Agente de Instantâneo** da publicação. Se esse for o caso, selecione **Iniciar** para iniciar o Agente de Instantâneo: 

       ![Iniciar Agente de Instantâneo](media/tutorial-replicating-data-between-continuously-connected-servers/startsnapshotagent.png)
     
       Se encontrar um erro, consulte [Solução de erros com o Agente de Instantâneo](#troubleshoot-erros-with-snapshot-agent). 

  
### <a name="to-add-the-distribution-agent-login-to-the-pal"></a>Para adicionar o logon Distribution Agent à PAL  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó do servidor e depois expanda a pasta **Replicação** .  
  
2.  Na pasta **Publicações Locais**, clique com o botão direito do mouse em **AdvWorksProductTrans** e, em seguida, selecione **Propriedades**.  A caixa de diálogo **Propriedades da Publicação** é exibida.    
  
    A. Selecione a página **Lista de Acesso à Publicação** e **Adicionar**.  
    B. Na caixa de diálogo **Adicionar Acesso à Publicação**, selecione <*Publisher_Machine_Name>***\repl_distribution** e selecione **OK**. Selecione **OK**:

   
   ![Adicionar logon à lista PAL](media/tutorial-replicating-data-between-continuously-connected-servers/tranreplproperties.png)

**Consulte também**:  
[Conceitos de programação da replicação](../../relational-databases/replication/concepts/replication-programming-concepts.md)  
  

## <a name="create-a-subscription-to-the-transactional-publication"></a>Criar uma assinatura na publicação Transacional
Nesta seção, você adicionará um assinante à Publicação criada anteriormente. Este tutorial usa um assinante remoto (NODE2\SQL2016), mas uma assinatura também pode ser adicionada localmente ao publicador. 

### <a name="to-create-the-subscription"></a>Para criar a assinatura  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó do servidor e depois expanda a pasta **Replicação** .  
  
2.  Na pasta **Publicações Locais**, clique com o botão direito do mouse na publicação **AdvWorksProductTrans** e, em seguida, selecione **Novas Assinaturas**.  O Assistente para Nova Assinatura é iniciado: 
 
    ![Nova Assinatura](media/tutorial-replicating-data-between-continuously-connected-servers/newsub.png)     
  
3.  Na página Publicação, selecione **AdvWorksProductTrans** e, em seguida, **Avançar**:  

    ![Selecionar o publicador Tran](media/tutorial-replicating-data-between-continuously-connected-servers/selectpub.png)
  
4.  Na página Local do Agente de Distribuição, selecione **Executar todos os agentes no Distribuidor** e, em seguida, selecione **Avançar**.  Para obter mais informações sobre assinaturas pull e push, consulte [Assinar publicações](https://docs.microsoft.com/en-us/sql/relational-databases/replication/subscribe-to-publications):

    ![Executar agentes em Dist](media/tutorial-replicating-data-between-continuously-connected-servers/runagentsatdist.png)
  
5.  Na página Assinantes, se o nome da instância de Assinante não for exibido, selecione **Adicionar Assinante** e, em seguida, **Adicionar Assinante do SQL Server** na lista suspensa. Isso iniciará a caixa de diálogo **Conectar ao Servidor**. Insira o nome da instância de Assinante e, em seguida, selecione **Conectar**.  
    
    A. Depois que o Assinante for adicionado, marque a caixa ao lado do nome de instância da assinatura. Em seguida, selecione **Novo Banco de Dados** em **Banco de Dados de Assinatura**:   

  ![Adicionar servidor de assinante](media/tutorial-replicating-data-between-continuously-connected-servers/addsub.png)

7. Isso iniciará a caixa de diálogo **Novo Banco de Dados**. Insira **ProductReplica** na caixa **Nome do banco de dados**, selecione **OK** e, em seguida, **Avançar**: 
  
    ![Banco de dados de réplica de produto](media/tutorial-replicating-data-between-continuously-connected-servers/productreplica.png)
  
8.  Na caixa de diálogo **Segurança do Agente de Distribuição**, selecione o botão de reticências (**...**). Insira <*Publisher_Machine_Name>***\repl_distribution** na caixa **Conta do processo**, insira a senha da conta, selecione **OK** e, em seguida, selecione  **Avançar**:

    ![Adicionar conta de distribuição](media/tutorial-replicating-data-between-continuously-connected-servers/adddistaccount.png)
  
9. Selecione **Concluir** para aceitar os valores padrão nas páginas restantes e conclua o assistente.  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>Definindo permissões de banco de dados no Assinante  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda **Segurança**, clique com o botão direito do mouse em **Logons** e, em seguida, selecione **Novo Logon**.     
  
    A. Na página **Geral**, em **Nome de Logon**, selecione **Pesquisar** e adicione o logon a <*Subscriber_Machine_Name>***\repl_distribution**.
    B. Na página **Mapeamentos de Usuário**, conceda o logon **db_owner** ao banco de dados **ProductReplica**: 

    ![Logon no Assinante](media/tutorial-replicating-data-between-continuously-connected-servers/loginforsub.png)

2. Selecione **OK** para fechar a caixa de diálogo **Novo Logon**. 

  
### <a name="to-view-the-synchronization-status-of-the-subscription"></a>Para exibir o status da sincronização da assinatura  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó do servidor e depois expanda a pasta **Replicação** .  
  
2.  Na pasta **Publicações Locais**, expanda a publicação **AdvWorksProductTrans**, clique com o botão direito do mouse na assinatura no banco de dados **ProductReplica** e, em seguida, selecione **Exibir Status da Sincronização**. O status atual da sincronização da assinatura é exibido:  
    ![Exibir status da sincronização](media/tutorial-replicating-data-between-continuously-connected-servers/viewsyncstatus.png)
3.  Se a assinatura não for visível sob **AdvWorksProductTrans**, pressione F5 para atualizar a lista.  
  
**Consulte também**:  
[Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
[Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)  
[Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  

## <a name="measuring-replication-latency"></a>Medindo a latência de replicação
Nesta seção, você usará os tokens de rastreamento para verificar se as alterações estão sendo replicadas para o Assinante e para determinar a latência. Latência é o tempo necessário para que uma alteração feita no Publicador seja exibida no Assinante.
  
1. Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó de servidor, clique com o botão direito do mouse na pasta **Replicação** e, em seguida, selecione **Iniciar o Replication Monitor**:

    ![Iniciar o Replication Monitor](media/tutorial-replicating-data-between-continuously-connected-servers/launchreplmonitor.png)

2. Expanda um grupo Publicador no painel esquerdo, expanda a instância de Publicador e, em seguida, selecione a publicação **AdvWorksProductTrans**.  
  
    A. Selecione a guia **Tokens de Rastreamento**.  
    B. Selecione **Inserir Rastreamento**.    
    c. Exiba o tempo decorrido para o token de rastreamento nas seguintes colunas: **Publicador para Distribuidor**, **Distribuidor para Assinante**, **Latência Total**. Um valor de **Pendente** indica que o token não alcançou determinado ponto:


   ![Token de rastreamento](media/tutorial-replicating-data-between-continuously-connected-servers/tracertoken.png)


**Consulte também**   
[Measure Latency and Validate Connections for Transactional Replication](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)

## <a name="error-troubleshooting-methodology"></a>Metodologia de solução de erros
Esta seção ensina como solucionar falhas básicas de sincronização de replicação. Esta seção se destina a apresentar a navegação pelos componentes de replicação com o objetivo de solução de problemas. No entanto, os erros reais que você encontrar podem ser diferentes daqueles mostrados aqui e talvez você precise de outra resolução. Se esse for o caso, uma solução de problemas mais detalhada será necessária, mas isso está fora do escopo deste tutorial. 


### <a name="troubleshoot-errors-with-snapshot-agent"></a>Solução de erros com o Agente de Instantâneo
O **Agente de Instantâneo** é o agente que gera o instantâneo e grava-o na pasta de instantâneos especificada. 

1. Para exibir o status do agente de instantâneo, expanda o nó **Publicação Local** na replicação, selecione com o botão direito na publicação **AdvWorksProductTrans** > **Exibir Status do Agente de Instantâneo**. 
2. Se um erro for relatado no **Status do Agente de Instantâneo**, mais detalhes poderão ser encontrados no histórico de trabalhos do **Agente de Instantâneo**. Para acessá-lo, expanda **SQL Server Agent** no **Pesquisador de Objetos** e abra o **Monitor de Atividade do Trabalho**. 

    A. Classifique por **Categoria** e identifique o **Agente de Instantâneo** pela categoria 'REPL-Snapshot'. 

    B. Clique com o botão direito do mouse no **Agente de Instantâneo** e selecione **Exibir Histórico**: 

   ![Histórico do Agente de Instantâneo](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagenthistory.png)
    
1. No **Histórico do Agente de Instantâneo**, selecione a entrada de log relevante. Isso geralmente será uma linha ou duas *antes* que a entrada relate o erro (os erros são indicados com um X vermelho).  Examine o texto da mensagem na caixa de texto abaixo dos logs: 

    ![Acesso negado do Agente de Instantâneo](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotaccessdenied.png)

        The replication agent had encountered an exception.
        Exception Message: Access to path '\\node1\repldata.....' is denied.


  Se as permissões do Windows não estiverem configuradas corretamente para a pasta de instantâneos, você verá um erro "acesso negado" para o **Agente de Instantâneo**. Você precisará verificar as permissões para a conta <*Publisher_Machine_Name>***\repl_snapshot** na pasta de repldata. Para obter mais informações, consulte [Criar um compartilhamento para a pasta de instantâneos e atribuir permissões](tutorial-preparing-the-server-for-replication.md#create-a-share-for-the-snapshot-folder-and-assign-permissions).

### <a name="troubleshoot-errors-with-log-reader-agent"></a>Solução de erros com o Agente de Leitor de Log
O **Agente de Leitor de Log** se conecta ao banco de dados publicador e verifica o log de transações em busca de todas as transações marcadas como "para replicação". Em seguida, ele adiciona as transações ao banco de dados de **Distribuição**. 

1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó de servidor, clique com o botão direito do mouse na pasta **Replicação** e, em seguida, selecione **Iniciar o Replication Monitor**:  

    ![Iniciar o Repl Monitor](media/tutorial-replicating-data-between-continuously-connected-servers/launchreplmonitor.png)
  
    O Replication Monitor é iniciado: ![Replication Monitor](media/tutorial-replicating-data-between-continuously-connected-servers/replmonitor.png) 
   
2. O X vermelho é uma indicação de que a publicação não está sendo sincronizada. Expanda **Meus Publicadores** no lado esquerdo e, em seguida, expanda o servidor do publicador relevante.  
  
3.  Selecione a publicação **AdvWorksProductTrans** à esquerda e, em seguida, procure o X vermelho em uma das guias identificar onde está o problema. Nesse caso, o X vermelho é a **Guia Agentes**, indicando que um dos Agentes está apresentando um erro: 

    ![Erro do agente](media/tutorial-replicating-data-between-continuously-connected-servers/agenterror.png)

4. Selecione a **Guia Agentes** para identificar qual agente está encontrando o erro: 

    ![Falha do Leitor de Log](media/tutorial-replicating-data-between-continuously-connected-servers/logreaderagentfailure.png)


5. Esta exibição mostra dois agentes, o **Agente de Instantâneo** e o **Agente de Leitor de Log**. Aquele que apresentou um erro terá o X vermelho. Nesse caso, o **Agente de Leitor de Log** é aquele com o X vermelho, o que indica que há um problema com ele. Clique duas vezes na linha que está relatando o erro, nesse caso, o **Agente de Leitor de Log**. Isso iniciará o **Histórico do Agente** do Agente selecionado, nesse caso, o histórico do **Agente de Leitor de Log**. Isso fornece mais informações sobre o erro: 
    
    ![Erro do Leitor de Log](media/tutorial-replicating-data-between-continuously-connected-servers/logreadererror.png)

       Status: 0, code: 20011, text: 'The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.'.
       The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.
       Status: 0, code: 15517, text: 'Cannot execute as the database principal because the principal "dbo" does not exist, this type of principal cannot be impersonated, or you do not have permission.'.
       Status: 0, code: 22037, text: 'The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.'.        

6. O erro mencionado anteriormente é geralmente causado porque o proprietário do banco de dados publicador não está definido corretamente. Isso geralmente acontece quando um banco de dados foi restaurado. Para verificar isso, expanda **Bancos de Dados** no **Pesquisador de Objetos** > clique com o botão direito do mouse em **AdventureWorks2012** > **Propriedades**. Verifique se existe um proprietário na página **Arquivos**. Se esse campo estiver vazio, esta será a causa provável do problema: 

    ![Propriedades do BD](media/tutorial-replicating-data-between-continuously-connected-servers/dbproperties.png)

7. Se o proprietário estiver em branco na página **Arquivos**, abra um **Novo Período de Consulta** dentro do contexto do banco de dados **AdventureWorks2012**. Execute o seguinte trecho de código T-SQL:

    ```sql
    -- set the owner of the database to 'sa' or a specific user account, without the brackets. 
    EXEC sp_changedbowner '<useraccount>'
    -- example for sa: exec sp_changedbowner 'sa'
    -- example for user account: exec sp_changedbowner 'sqlrepro\administrator' 
    ```

8. Você precisará reiniciar o **Agente de Leitor de Log**. Para fazer isso, expanda o nó **SQL Server Agent** no **Pesquisador de Objetos** e abra o **Monitor de Atividade do Trabalho**. Classifique por **Categoria** e identifique o **Agente de Leitor de Log** pela categoria **'REPL-LogReader'**. Clique com o botão direito do mouse no trabalho do **Agente de Leitor de Log** e selecione **Iniciar Trabalho na Etapa**: 

    ![Reiniciar o Agente de Leitor de Log](media/tutorial-replicating-data-between-continuously-connected-servers/startjobatstep.png)

9. Valide se agora a publicação está sincronizando abrindo o **Replication Monitor** novamente. Se ainda não estiver aberto, ele poderá ser encontrado clicando com o botão direito do mouse em **Replicação** no **Pesquisador de Objetos**. 
10. Selecione a publicação **AdvWorksProductTrans**, selecione a guia **Agentes** e selecione duas vezes o **Agente de Leitor de Log** para abrir o histórico do agente. Agora você deverá ver que o **Agente de Leitor de Log** está em execução e replicando comandos ou que ele mostra a mensagem "Nenhuma Transação Replicada":

    ![Leitor de Log em Execução](media/tutorial-replicating-data-between-continuously-connected-servers/logreaderrunning.png)

### <a name="troubleshoot-errors-with-distribution-agent"></a>Solução de erros com o Agente de Distribuição
O **Agente de Distribuição** usa os dados encontrados no banco de dados **Distribuição** e, em seguida, aplica-os ao Assinante. 

1. Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó de servidor, clique com o botão direito do mouse na pasta **Replicação** e, em seguida, selecione **Iniciar o Replication Monitor**.  
2. Em **Replication Monitor**, selecione a publicação **AdvWorksProductTrans** e a guia **Todas as Assinaturas**. Clique com o botão direito do mouse na Assinatura e selecione **Exibir Detalhes**:

    ![Exibir detalhes de Dist](media/tutorial-replicating-data-between-continuously-connected-servers/viewdetails.png)

2. A caixa de diálogo do histórico do **Distribuidor para Assinante** é aberta e esclarece o erro que o agente está apresentando: 

     ![Erro de histórico do agente de distribuição](media/tutorial-replicating-data-between-continuously-connected-servers/disthistoryerror.png)
    
        Error messages:
        Agent 'NODE1\SQL2016-AdventureWorks2012-AdvWorksProductTrans-NODE2\SQL2016-7' is retrying after an error. 89 retries attempted. See agent job history in the Jobs folder for more details.

3. O erro indica que o **Agente de Distribuição** está tentando novamente. Para obter mais informações, expanda **SQL Server Agent** no **Pesquisador de Objetos** > **Monitor de Atividade do Trabalho**. Classifique os trabalhos por **Categoria**. 

    A. Identifique o **Agente de Distribuição** pela categoria **'REPL-Distribution'**. Clique com o botão direito do mouse no agente e selecione **Exibir Histórico**:

    ![Exibir o histórico do agente de distribuição](media/tutorial-replicating-data-between-continuously-connected-servers/viewdistagenthistory.png)

5. Selecione uma das entradas de erro e exiba o texto de erro na parte inferior da janela:  

    ![Senha incorreta para o agente de distribuição](media/tutorial-replicating-data-between-continuously-connected-servers/distpwwrong.png)
    
        Message:
        Unable to start execution of step 2 (reason: Error authenticating proxy NODE1\repl_distribution, system error: The user name or password is incorrect.)

6. Esse erro é uma indicação de que a senha usada pelo **Agente de Distribuição** está incorreta. Para resolver esse problema, expanda o nó **Replicação** no **Pesquisador de Objetos** e clique com o botão direito do mouse na assinatura > **Propriedades**. Selecione as reticências (...) ao lado de **Conta de Processo do Agente** e modifique a senha:

    ![Modificar o PW para o Agente de Distribuição](media/tutorial-replicating-data-between-continuously-connected-servers/distagentpwchange.png)

7. Verifique o **Replication Monitor** novamente, que pode ser encontrado clicando com o botão direito do mouse em **Replicação** no **Pesquisador de Objetos**. Um X vermelho em **Todas as Assinaturas** indica que nosso **Agente de Distribuição** ainda está encontrando um erro. Abra o histórico de **Distribuição ao Assinante** clicando com o botão direito do mouse na Assinatura em **Replication Monitor** > **Exibir Detalhes**. Aqui, o erro agora é diferente: 

    ![O agente de distribuição não pode se conectar](media/tutorial-replicating-data-between-continuously-connected-servers/distagentcantconnect.png)
           
        Connecting to Subscriber 'NODE2\SQL2016'        
        Agent message code 20084. The process could not connect to Subscriber 'NODE2\SQL2016'.
        Number:  18456
        Message: Login failed for user 'NODE2\repl_distribution'.

8. Esse erro indica que o **Agente de Distribuição** não pôde se conectar ao assinante, pois houve uma falha de logon do usuário **NODE2\repl_distribution**. Para investigar melhor, conecte-se ao Assinante e abra o **Log de Erros do SQL** *atual* no nó **Gerenciamento** do **Pesquisador de Objetos**: 

    ![Falha de Logon para o Assinante](media/tutorial-replicating-data-between-continuously-connected-servers/loginfailed.png) Se você está vendo esse erro, o logon está ausente no assinante. Para resolver esse problema, veja [Definição de permissões de banco de dados no Assinante](#setting-database-permissions-at-the-subscriber).

9. Depois que o erro de logon for resolvido, verifique o **Replication Monitor** novamente. Se todos os problemas foram resolvidos, você deverá ver uma seta verde ao lado do **Nome da Publicação** e o status **Em execução** em **Todas as Assinaturas**. Clique com o botão direito do mouse em **Assinatura** para iniciar o histórico do **Distribuidor para Assinante** mais uma vez para verificar o êxito. Se essa é a primeira vez que o agente de distribuição é executado, você vê que o instantâneo foi copiado em massa para o assinante como indica a figura abaixo: 

     ![Êxito do agente de distribuição](media/tutorial-replicating-data-between-continuously-connected-servers/distagentsuccess.png)   

  ## <a name="next-steps"></a>Próximas etapas
Você configurou com êxito o Publicador e o Assinante para a Replicação Transacional.  Agora você pode inserir, atualizar ou excluir dados da tabela **Product** no Publicador. Em seguida, você pode consultar a tabela **Product** no Assinante para exibir as alterações replicadas. O próximo artigo ensinará como configurar a replicação de Mesclagem.  

Prossiga para o próximo artigo para saber mais
> [!div class="nextstepaction"]
> [Próximas etapas](tutorial-replicating-data-with-mobile-clients.md)

  
