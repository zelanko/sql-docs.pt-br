---
title: 'Tutorial: Preparar o SQL Server para replicação – Publicador, Distribuidor, Assinante | Microsoft Docs'
ms.custom: ''
ms.date: 04/02/2018
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
ms.assetid: ce30a095-2975-4387-9377-94a461ac78ee
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1468095ba959f7baf383b68cfaab65dab2591af6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="tutorial-prepare-sql-server-for-replication---publisher-distributor-subscriber"></a>Tutorial: Preparar o SQL Server para replicação – Publicador, Distribuidor, Assinante
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
É importante planejar a segurança antes de configurar a topologia de replicação. Este tutorial mostra a melhor forma de garantir a segurança de uma topologia de replicação e também como configurar a distribuição, que é a primeira etapa na replicação de dados. É preciso concluir este tutorial antes de qualquer outro.  
  
> [!NOTE]  
> Para replicar dados com segurança entre servidores, é necessário implementar todas as recomendações em [Práticas recomendadas em relação à segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
Este tutorial ensina você a preparar um servidor para que a replicação possa ser executada de modo seguro com privilégios mínimos.  

Neste tutorial, você aprenderá a:
> [!div class="checklist"]
> * Criar contas do Windows para replicação
> * Preparar a pasta de Instantâneos
> * Configurar a distribuição

## <a name="prerequisites"></a>Prerequisites
Este Tutorial é destinado a usuários que estão familiarizados com operações fundamentais de bancos de dados, mas que têm pouca experiência com replicação. 

Para concluir este Tutorial, o sistema deve ter o SSMS (SQL Server Management Studio) e estes componentes:  
  
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


**Tempo estimado para concluir este tutorial: 30 minutos**
  
## <a name="create-windows-accounts-for-replication"></a>Criar contas do Windows para replicação
Nesta seção, você criará contas do Windows para executar os agentes de replicação. Você criará uma conta de Windows separada no servidor local para os seguintes agentes:  
  
|Agente|Local|Nome da conta|  
|---------|------------|----------------|  
|Snapshot Agent|Publicador|<*machine_name*>\repl_snapshot|  
|Agente de Leitor de Log|Publicador|<*machine_name*>\repl_logreader|  
|Agente de Distribuição|Publicador e assinante|<*machine_name*>\repl_distribution|  
|Agente de Mesclagem|Publicador e assinante|<*machine_name*>\repl_merge|  
  
> [!NOTE]  
> Nos tutoriais sobre replicação, o Publicador e o Distribuidor compartilham a mesma instância (NODE1\SQL2016) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], enquanto a instância de Assinante (NODE2\SQL2016) é remota. O Publicador e o Assinante podem compartilhar a mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas isso não é um requisito. Se o Publicador e o Assinante compartilharem a mesma instância, as etapas usadas para criar contas no Assinante não são necessárias.  

### <a name="create-local-windows-accounts-for-replication-agents-at-the-publisher"></a>Criar contas locais do Windows para agentes de replicação no Publicador
  
1.  No Publicador, abra **Gerenciamento do Computador** em **Ferramentas Administrativas** no Painel de Controle.  
  
2.  Em **Ferramentas do Sistema**, expanda **Usuários e Grupos Locais**.  
  
3.  Clique com o botão direito do mouse em **Usuários** e, em seguida, selecione **Novo Usuário**.  
     
4.  Insira **repl_snapshot** na caixa **Nome de usuário**, forneça a senha e outras informações relevantes e, em seguida, selecione **Criar** para criar a conta repl_snapshot: 

       ![Novo usuário](media/tutorial-preparing-the-server-for-replication/newuser.png)
  
5.  Repita a etapa anterior para criar as contas de repl_logreader, repl_distribution e repl_merge:  
 
    ![Usuários de replicação](media/tutorial-preparing-the-server-for-replication/replusers.png)
  
6.  Selecione **Fechar**.  
  
### <a name="to-create-local-windows-accounts-for-replication-agents-at-the-subscriber"></a>Para criar contas locais do Windows para agentes de replicação no Assinante  
  
1.  No Assinante, abra **Gerenciamento do Computador** em **Ferramentas Administrativas** no Painel de Controle.  
  
2.  Em **Ferramentas do Sistema**, expanda **Usuários e Grupos Locais**.  
  
3.  Clique com o botão direito do mouse em **Usuários** e, em seguida, selecione **Novo Usuário**.  
  
4.  Insira **repl_distribution** na caixa **Nome de usuário**, forneça a senha e outras informações relevantes e, em seguida, selecione **Criar** para criar a conta repl_distribution.  
  
5.  Repita a etapa anterior para criar a conta de repl_merge.  
  
6.  Selecione **Fechar**.  

**Consulte também**: [Visão geral dos agentes de replicação](../../relational-databases/replication/agents/replication-agents-overview.md)  

## <a name="prepare-the-snapshot-folder"></a>Preparar a pasta de instantâneos
Nesta seção, você aprenderá a configurar a pasta de instantâneos, usada para criar e armazenar o instantâneo de publicação. 

### <a name="create-a-share-for-the-snapshot-folder-and-assign-permissions"></a>Criar um compartilhamento para a pasta de instantâneos e atribuir permissões  
  
1.  No Windows Explorer, vá para a pasta de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O local padrão é C:\Arquivos de Programa\Microsoft SQL Server\MSSQL.X\MSSQL\Data.  
  
2.  Crie uma nova pasta chamada **repldata**.  
  
3.  Clique com o botão direito do mouse nessa pasta e selecione **Propriedades**.  
  
    A. Na guia **Compartilhamento** da caixa de diálogo **Propriedades de repldata**, selecione **Compartilhamento Avançado**.  
  
    B. Na caixa de diálogo **Compartilhamento Avançado**, selecione **Compartilhar esta Pasta** e, em seguida, selecione **Permissões**:  

       ![Compartilhando dados de repl](media/tutorial-preparing-the-server-for-replication/repldata.png)

6.  Na caixa de diálogo **Permissões para repldata**, selecione **Adicionar**. Na caixa de texto **Selecionar Usuário, Computadores, Conta de Serviço ou Grupos**, digite o nome da conta do Agente de Instantâneo criado anteriormente, como <*Publisher_Machine_Name>***\repl_snapshot**. Selecione **Verificar Nomes** e, em seguida, **OK**:  

    ![Adicionar permissões de compartilhamento](media/tutorial-preparing-the-server-for-replication/addshareperms.png)

7. Repita a etapa 6 para adicionar as outras duas contas que foram criadas anteriormente: <*Publisher_Machine_Name>***\repl_merge** e <*Publisher_Machine_Name>***\repl_distribution**

8. Depois de adicionar essas três contas, atribua as seguintes permissões:      
    - repl_distribution - Leitura  
    - repl_merge - Leitura  
    - repl_snapshot - Controle total    

  ![Permissões compartilhadas](media/tutorial-preparing-the-server-for-replication/sharedpermissions.png)

9. Depois que as permissões de compartilhamento forem configuradas corretamente, selecione **OK** para fechar a caixa de diálogo **Permissões para repldata**. Selecione **OK** para fechar a caixa de diálogo **Compartilhamento Avançado**. 

10.  Nas **Propriedades de repldata**, selecione a guia **Segurança** e **Editar**:  

       ![Editar a segurança](media/tutorial-preparing-the-server-for-replication/editsecurity.png)   

11. Na caixa de diálogo **Permissões para repldata**, selecione **Adicionar...**. Na caixa de texto **Selecionar Usuário, Computadores, Conta de Serviço ou Grupos**, digite o nome da conta do Agente de Instantâneo criado anteriormente, como <*Publisher_Machine_Name>***\repl_snapshot**. Selecione **Verificar Nomes** e, em seguida, **OK**:  

    ![Adicionar permissões de segurança](media/tutorial-preparing-the-server-for-replication/addsecuritypermissions.png)

  
12.  Repita a etapa anterior para adicionar permissões para o Agente de Distribuição, como <*Publisher_Machine_Name>***\repl_distribution**, e para o Agente de Mesclagem, como <* Publisher_Machine_Name>***\repl_merge**.  
    
  
13. Verifique se as permissões a seguir são permitidas:  
  
    - repl_distribution - Leitura
    - repl_merge - Leitura
    - repl_snapshot - Controle total   
 
    ![Permissões de usuário de dados de replicação](media/tutorial-preparing-the-server-for-replication/replpermissions.png) 

14. Selecione a guia **Compartilhamento** novamente e anote o **Caminho da Rede** para o compartilhamento. Você precisará desse caminho posteriormente quando estiver configurando a **Pasta de Instantâneos**:  

    ![Caminho da rede](media/tutorial-replicating-data-between-continuously-connected-servers/networkpath.png)

15. Selecione **OK** para fechar a caixa de diálogo **Propriedades de repldata**. 
 
**Consulte também**:  
[Proteger a pasta de instantâneos](../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  

## <a name="configure-distribution"></a>Configurar a distribuição
Nesta seção, você configurará a distribuição no Publicador e definirá as permissões necessárias nos bancos de dados de publicação e distribuição. Se você já tiver configurado o Distribuidor, será necessário desabilitar primeiramente a publicação e a distribuição antes de iniciar esta seção. Não faça isto se for preciso manter uma topologia de replicação existente, especialmente em Produção.   
  
A configuração de um Publicador com um Distribuidor remoto está fora do escopo deste tutorial.  

### <a name="configure-distribution-at-the-publisher"></a>Configurar a distribuição no Publicador  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó de servidor.  
  
2.  Clique com o botão direito do mouse na pasta **Replicação** e selecione **Configurar Distribuição**:  

    ![Configurar a distribuição](media/tutorial-preparing-the-server-for-replication/configuredistribution.png)
  
    > [!NOTE]  
    > Se você se conectou ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando **localhost** em vez do nome de servidor real, receberá um aviso de que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode se conectar ao **'localhost'** do servidor. Selecione **OK** na caixa de diálogo de aviso. Na caixa de diálogo **Conectar ao Servidor** , altere o **Nome do Servidor** de **localhost** para o nome do seu servidor. Selecione **Conectar**.  
  
    O Assistente para Configuração de Distribuição é iniciado.  
  
3.  Na página **Distribuidor**, a seleção de **'ServerName' atuará como seu próprio Distribuidor; o SQL Server criará um banco de dados de distribuição e um log**. Depois, selecione **Avançar**:  

    ![O servidor atua como o próprio distribuidor](media/tutorial-preparing-the-server-for-replication/serverdistributor.png)
  
4.  Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não estiver em execução, na página Inicial do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Agent**, selecione **Sim** para configurar o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para ser iniciado automaticamente. Selecione **Avançar**.  

     
5.  Insira o caminho \\\\<*Publisher_Machine_Name>***\repldata** na caixa de texto **Pasta de instantâneos** e, em seguida, selecione **Avançar**. Esse caminho deve corresponder ao que você viu anteriormente em **Caminho da Rede** da pasta de propriedades de repldata depois de configurar as propriedades de compartilhamento: 

    ![Pasta de instantâneos de dados de replicação](media/tutorial-preparing-the-server-for-replication/repldatasnapshot.png)
  
6.  Aceite os valores padrão das páginas restantes do assistente:  
    
    ![Padrões do Assistente de Distribuição](media/tutorial-preparing-the-server-for-replication/distributionwizarddefaults.png)
  
7.  Selecione **Concluir** para habilitar a distribuição. 

    Você poderá ver esse erro ao configurar o Distribuidor. É uma indicação de que a conta usada para iniciar a conta do SQL Server Agent não é um administrador do sistema. Você precisará iniciar o SQL Server Agent manualmente, conceder as permissões para a conta existente ou modificar a conta que está sendo usada pelo SQL Server Agent: 

     ![Erro de inicialização do agente](media/tutorial-preparing-the-server-for-replication/startingagenterror.png)

    Se o SQL Server Management Studio estiver sendo executado com direitos administrativos, você poderá iniciar o SQL Agent manualmente no SSMS:  
        ![Iniciar Agente por meio do SSMS](media/tutorial-preparing-the-server-for-replication/ssmsstartagent.png) 

    >[!NOTE]
    > Se o SQL Agent não for visivelmente iniciado, clique com o botão direito do mouse no SQL Server Agent no SSMS e clique em **Atualizar**.  Se ele ainda estiver em um estado interrompido, você precisará iniciá-lo manualmente no **SQL Server Configuration Manager**.    
  
### <a name="setting-database-permissions-at-the-publisher"></a>Definindo permissões de banco de dados no Publicador  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda **Segurança**, clique com o botão direito do mouse em **Logons** e, em seguida, selecione **Novo Logon**:  

    ![Novo Logon](media/tutorial-preparing-the-server-for-replication/newlogin.png)
  
2.  Na página **Geral**, selecione **Pesquisar**, insira <*Publisher_Machine_Name>***\repl_snapshot** na caixa **Inserir o nome do objeto a ser selecionado**. Em seguida, selecione **Verificar Nomes** e **OK**:  

    ![Adicionar logon de instantâneo da replicação](media/tutorial-preparing-the-server-for-replication/addsnapshotlogin.png)
  
3.  Na página **Mapeamento de Usuário** , na lista **Usuários mapeados para este logon** , selecione os bancos de dados de **distribuição** e de [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
    Na lista Associação à função de banco de dados, selecione a função **db_owner** para o logon de ambos os bancos de dados:  

    ![Proprietário do BD de instantâneos de replicação](media/tutorial-preparing-the-server-for-replication/dbowner.png)
  
4.  Selecione **OK** para criar o logon.  
  
5.  Repita as etapas 1 a 4 para criar um logon para outras contas locais (repl_distribution, repl_logreader e repl_merge). Esses logons também devem ser mapeados para usuários que são membros da função de bancos de dados fixa **db_owner** nos bancos de dados de **distribuição** e **AdventureWorks**:  

    ![Usuários de replicação no SSMS](media/tutorial-preparing-the-server-for-replication/usersinssms.png)
  
  
**Consulte também**:  
[Configurar Distribuição](../../relational-databases/replication/configure-distribution.md)  
[Modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md)  

## <a name="next-steps"></a>Próximas etapas
Agora você preparou com êxito o servidor para replicação. O próximo artigo ensina como configurar a Replicação Transacional. 

Prossiga para o próximo artigo para saber mais
> [!div class="nextstepaction"]
> [Próximas etapas](tutorial-replicating-data-between-continuously-connected-servers.md)

  
  
