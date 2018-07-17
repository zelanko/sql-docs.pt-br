---
title: 'Tutorial: Preparar o SQL Server para replicação (editor, distribuidor, assinante) | Microsoft Docs'
ms.custom: ''
ms.date: 04/02/2018
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
ms.assetid: ce30a095-2975-4387-9377-94a461ac78ee
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 672b5c5f8011572994c6c611430f72982c418101
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37350378"
---
# <a name="tutorial-prepare-sql-server-for-replication-publisher-distributor-subscriber"></a>Tutorial: Preparar o SQL Server para replicação (editor, distribuidor, assinante)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
É importante planejar a segurança antes de configurar a topologia de replicação. Este tutorial mostra como você deve proteger melhor uma topologia de replicação. Ele também mostra como configurar a distribuição, que é a primeira etapa na replicação de dados. É preciso concluir este tutorial antes de qualquer outro.  
  
> [!NOTE]  
> Para replicar dados com segurança entre servidores, é necessário implementar todas as recomendações em [Práticas recomendadas em relação à segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
Este tutorial ensina você a preparar um servidor para que a replicação possa ser executada de modo seguro com privilégios mínimos.  

Neste tutorial, você aprenderá a:
> [!div class="checklist"]
> * Crie contas do Windows para replicação.
> * Prepare a pasta de instantâneos.
> * Configure a distribuição.

## <a name="prerequisites"></a>Prerequisites
Este tutorial é destinado a usuários que estão familiarizados com operações fundamentais de bancos de dados, mas que têm pouca experiência com replicação. 

Para concluir este tutorial, são necessários o SQL Server, o SSMS (SQL Server Management Studio) e um banco de dados do AdventureWorks:  
  
- No servidor do editor (origem), instale:  
  
   - Qualquer edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], exceto o SQL Server Express ou o SQL Server Compact. Estas edições não podem ser editores de replicação.   
   - O banco de dados de exemplo [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] . Para reforçar a segurança, os bancos de dados de exemplo não são instalados por padrão.  
  
- No servidor do assinante (destino), instale qualquer edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], exceto [!INCLUDE[ssEW](../../includes/ssew-md.md)]. [!INCLUDE[ssEW](../../includes/ssew-md.md)] não pode ser um assinante em uma replicação transacional.  
  
- Instalar o [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
- Instale o [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).
- Baixe o [banco de dados de exemplo do AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases). Para obter instruções sobre como restaurar um banco de dados no SSMS, veja [Como restaurar um banco de dados](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms). 
    
>[!NOTE]
> - A replicação não é compatível em instâncias do SQL Server que tenham um intervalo de mais de duas versões. Para saber mais, veja [Supported SQL Server Versions in Replication Topology](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/) (Versões do SQL Server compatíveis na topologia de replicação).
> - No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], é necessário conectar-se ao editor e ao assinante usando um logon que seja membro da função de servidor fixa **sysadmin**. Para saber mais sobre essa função, veja [Funções de nível de servidor](https://docs.microsoft.com/en-us/sql/relational-databases/security/authentication-access/server-level-roles).  


**Tempo estimado para concluir este tutorial: 30 minutos**
  
## <a name="create-windows-accounts-for-replication"></a>Criar contas do Windows para replicação
Nesta seção, você criará contas do Windows para executar os agentes de replicação. Você criará uma conta de Windows separada no servidor local para os seguintes agentes:  
  
|Agente|Local|Nome da conta|  
|---------|------------|----------------|  
|Snapshot Agent|Publicador|<*machine_name*>\repl_snapshot|  
|Agente de Leitor de Log|Publicador|<*machine_name*>\repl_logreader|  
|Agente de Distribuição|Publicador e assinante|<*machine_name*>\repl_distribution|  
|Merge Agent|Publicador e assinante|<*machine_name*>\repl_merge|  
  
> [!NOTE]  
> Nos tutoriais de replicação, o editor e o distribuidor compartilham a mesma instância (NODE1\SQL2016) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A instância de assinante (NODE2\SQL2016) é remota. O editor e o assinante podem compartilhar a mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas isso não é um requisito. Se o editor e o assinante compartilharem a mesma instância, as etapas usadas para criar contas no assinante não são necessárias.  

### <a name="create-local-windows-accounts-for-replication-agents-at-the-publisher"></a>Criar contas locais do Windows para agentes de replicação no editor
  
1. No editor, abra **Gerenciamento do Computador** em **Ferramentas Administrativas** no Painel de Controle.  
  
2. Em **Ferramentas do Sistema**, expanda **Usuários e Grupos Locais**.  
  
3. Clique com o botão direito do mouse em **Usuários** e, em seguida, selecione **Novo Usuário**.  
     
4. Insira **repl_snapshot** na caixa **Nome de usuário**, forneça a senha e outras informações relevantes e, em seguida, selecione **Criar** para criar a conta repl_snapshot: 

   ![Caixa de diálogo "Novo Usuário"](media/tutorial-preparing-the-server-for-replication/newuser.png)
  
5. Repita a etapa anterior para criar as contas de repl_logreader, repl_distribution e repl_merge:  
 
   ![Lista de usuários de replicação](media/tutorial-preparing-the-server-for-replication/replusers.png)
  
6. Selecione **Fechar**.  
  
### <a name="create-local-windows-accounts-for-replication-agents-at-the-subscriber"></a>Crie contas locais do Windows para agentes de replicação no assinante  
  
1. No assinante, abra **Gerenciamento do Computador** em **Ferramentas Administrativas** no Painel de Controle.  
  
2. Em **Ferramentas do Sistema**, expanda **Usuários e Grupos Locais**.  
  
3. Clique com o botão direito do mouse em **Usuários** e, em seguida, selecione **Novo Usuário**.  
  
4. Insira **repl_distribution** na caixa **Nome de usuário**, forneça a senha e outras informações relevantes e, em seguida, selecione **Criar** para criar a conta repl_distribution.  
  
5. Repita a etapa anterior para criar a conta de repl_merge.  
  
6. Selecione **Fechar**.  

Para saber mais, veja [Visão geral dos agentes de replicação](../../relational-databases/replication/agents/replication-agents-overview.md).  

## <a name="prepare-the-snapshot-folder"></a>Preparar a pasta de instantâneos
Nesta seção, você configurará a pasta de instantâneos, usada para criar e armazenar o instantâneo de publicação. 

### <a name="create-a-share-for-the-snapshot-folder-and-assign-permissions"></a>Criar um compartilhamento para a pasta de instantâneos e atribuir permissões  
  
1. No Explorador de Arquivos, navegue até a pasta de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O local padrão é C:\Arquivos de Programa\Microsoft SQL Server\MSSQL.X\MSSQL\Data.  
  
2. Crie uma nova pasta chamada **repldata**.  
  
3. Clique com o botão direito do mouse nessa pasta e selecione **Propriedades**.  
  
   A. Na guia **Compartilhamento** da caixa de diálogo **Propriedades de repldata**, selecione **Compartilhamento Avançado**.  
  
   B. Na caixa de diálogo **Compartilhamento Avançado**, selecione **Compartilhar esta Pasta** e, em seguida, selecione **Permissões**.  

   ![Seleções para compartilhar a pasta repldata](media/tutorial-preparing-the-server-for-replication/repldata.png)

6. Na caixa de diálogo **Permissões para repldata**, selecione **Adicionar**. Na caixa de texto **Selecionar Usuário, Computadores, Conta de Serviço ou Grupos**, digite o nome da conta do Agente de Instantâneo criado anteriormente, como <*Nome_do_Computador_do_Editor*>**\repl_snapshot**. Selecione **Verificar Nomes** e, em seguida, **OK**.  

   ![Seleções para adicionar permissões de compartilhamento](media/tutorial-preparing-the-server-for-replication/addshareperms.png)

7. Repita a etapa 6 para adicionar as outras duas contas que você criou anteriormente: <*Nome_do_Computador_do_Editor*>**\repl_merge** e <*Nome_do_Computador_do_Editor*>**\repl_distribution**.

8. Depois de adicionar as três contas, atribua as seguintes permissões:      
   - repl_distribution: **Leitura**  
   - repl_merge: **Leitura**  
   - repl_snapshot: **Controle Total**    

   ![Permissões compartilhadas para cada conta](media/tutorial-preparing-the-server-for-replication/sharedpermissions.png)

9. Depois que as permissões de compartilhamento forem configuradas corretamente, selecione **OK** para fechar a caixa de diálogo **Permissões para repldata**. Selecione **OK** para fechar a caixa de diálogo **Compartilhamento Avançado**. 

10. Na caixa de diálogo **Propriedades de repldata**, selecione a guia **Segurança** e **Editar**:  

    ![Botão "Editar" na guia "Segurança"](media/tutorial-preparing-the-server-for-replication/editsecurity.png)   

11. Na caixa de diálogo **Permissões para repldata**, selecione **Adicionar**. Na caixa de texto **Selecionar Usuários, Computadores, Conta de Serviço ou Grupos**, digite o nome da conta do Agente de Instantâneo criado anteriormente, como <*Nome_do_Computador_do_Editor*>**\repl_snapshot**. Selecione **Verificar Nomes** e, em seguida, **OK**.  

    ![Seleções para adicionar permissões de segurança](media/tutorial-preparing-the-server-for-replication/addsecuritypermissions.png)

  
12. Repita a etapa anterior para adicionar permissões para o Agente de Distribuição, como <*Nome_do_Computador_do_Editor*>**\repl_distribution**, e para o Agente de Mesclagem, como <*Nome_do_Computador_do_Editor*>**\repl_merge**.  
    
  
13. Verifique se as permissões a seguir são permitidas:  
  
    - repl_distribution: **Leitura**
    - repl_merge: **Leitura**
    - repl_snapshot: **Controle Total**   
 
    ![Permissões de usuário para replicação de dados](media/tutorial-preparing-the-server-for-replication/replpermissions.png) 

14. Selecione a guia **Compartilhamento** novamente e anote o **Caminho da Rede** para o compartilhamento. Você precisará desse caminho posteriormente quando estiver configurando a pasta de instantâneos.  

    ![Caminho de rede na guia "Compartilhamento"](media/tutorial-replicating-data-between-continuously-connected-servers/networkpath.png)

15. Selecione **OK** para fechar a caixa de diálogo **Propriedades de repldata**. 
 
Para saber mais, veja [Proteger a pasta de instantâneos](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  

## <a name="configure-distribution"></a>Configurar distribuição
Nesta seção, você configurará a distribuição no editor e definirá as permissões necessárias nos bancos de dados de publicação e distribuição. Se você já tiver configurado o distribuidor, será necessário desabilitar a publicação e a distribuição antes de iniciar esta seção. Não faça isto se for preciso manter uma topologia de replicação existente, especialmente em produção.   
  
A configuração de um editor com um distribuidor remoto está fora do escopo deste tutorial.  

### <a name="configure-distribution-at-the-publisher"></a>Configurar a distribuição no editor  
  
1. Conecte-se ao editor no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e expanda o nó de servidor.  
  
2. Clique com o botão direito do mouse na pasta **Replicação** e selecione **Configurar Distribuição**:  

   ![Comando "Configurar Distribuição" no menu de atalho](media/tutorial-preparing-the-server-for-replication/configuredistribution.png)
  
   > [!NOTE]  
   > Se você se conectou ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando **localhost** em vez do nome do servidor real, receberá um aviso de que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode se conectar ao **localhost**. Selecione **OK** na caixa de diálogo de aviso. Na caixa de diálogo **Conectar ao Servidor**, altere o **Nome do Servidor** de **localhost** para o nome do seu servidor. Depois, selecione **Conectar**.  
  
   O Assistente para Configuração de Distribuição é iniciado.  
  
3. Na página **Distribuidor**, selecionar <*'ServerName'*>  **atuará como seu próprio Distribuidor; o SQL Server criará um banco de dados de distribuição e um log**. Em seguida, selecione **Avançar**.  

   ![Opção para fazer o servidor agir como seu próprio distribuidor](media/tutorial-preparing-the-server-for-replication/serverdistributor.png)
  
4. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não estiver em execução, na página Inicial do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Agent**, selecione **Sim[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para configurar o serviço**  Agent para ser iniciado automaticamente. Selecione **Avançar**.  

     
5. Insira o caminho \\\\<*Nome_do_Computador_do_Editor*>**\repldata** na caixa de texto **Pasta de instantâneos** e, em seguida, selecione **Avançar**. Esse caminho deve corresponder ao que você viu anteriormente em **Caminho da Rede** para a pasta de propriedades de repldata depois de configurar as propriedades de compartilhamento. 

   ![Comparação de caminhos de rede na caixa de diálogo "propriedades de repldata" e no Assistente para configurar distribuição](media/tutorial-preparing-the-server-for-replication/repldatasnapshot.png)
  
6. Aceite os valores padrão das páginas restantes do assistente.  
    
   ![Última página do assistente](media/tutorial-preparing-the-server-for-replication/distributionwizarddefaults.png)
  
7. Selecione **Concluir** para habilitar a distribuição. 

Você poderá ver esse erro a seguir ao configurar o distribuidor. É uma indicação de que a conta usada para iniciar a conta do SQL Server Agent não é um administrador do sistema. Você precisará iniciar o SQL Server Agent manualmente, conceder as permissões para a conta existente ou modificar a conta que está sendo usada pelo SQL Server Agent. 

![Mensagem de erro para configurar o SQL Server Agent](media/tutorial-preparing-the-server-for-replication/startingagenterror.png)

Se a instância do SQL Server Management Studio estiver sendo executada com direitos administrativos, você poderá iniciar o SQL Agent manualmente no SSMS:  
    
![Selecione "Iniciar" no menu de atalho para o agente no SSMS](media/tutorial-preparing-the-server-for-replication/ssmsstartagent.png) 

>[!NOTE]
> Se o SQL Agent não for visivelmente iniciado, clique com o botão direito do mouse no SQL Server Agent no SSMS e selecione **Atualizar**. Se ele ainda estiver em um estado interrompido, você precisará iniciá-lo manualmente no SQL Server Configuration Manager.    
  
### <a name="set-database-permissions-at-the-publisher"></a>Definir permissões de banco de dados no editor  
  
1. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda **Segurança**, clique com o botão direito do mouse em **Logons** e, em seguida, selecione **Novo Logon**:  

   ![Comando "Novo logon" no menu de atalho](media/tutorial-preparing-the-server-for-replication/newlogin.png)
  
2. Na página **Geral**, selecione **Pesquisar**. Insira <*Nome_do_Computador_do_Editor*>**\repl_snapshot** na caixa **Inserir o nome do objeto a ser selecionado**, selecione **Verificar Nomes** e **OK**.  

   ![Seleções para inserir o nome do objeto](media/tutorial-preparing-the-server-for-replication/addsnapshotlogin.png)
  
3. Na página **Mapeamento de Usuário**, na lista **Usuários mapeados para este logon**, selecione os bancos de dados de **distribuição** e de [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
   Na lista associação à função de banco de dados, selecione a função **db_owner** para o logon de ambos os bancos de dados.  

   ![Selecionar os bancos de dados e sua função](media/tutorial-preparing-the-server-for-replication/dbowner.png)
  
4. Selecione **OK** para criar o logon.  
  
5. Repita as etapas 1 a 4 para criar um logon para outras contas locais (repl_distribution, repl_logreader e repl_merge). Esses logons também devem ser mapeados para usuários que são membros da função de banco de dados fixa **db_owner** nos bancos de dados de **distribuição** e **AdventureWorks**.  

   ![Exibição de todas as quatro contas no Pesquisador de Objetos](media/tutorial-preparing-the-server-for-replication/usersinssms.png)
  
  
Para obter mais informações, consulte:
- [Configurar distribuição](../../relational-databases/replication/configure-distribution.md) 
- [Modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md)  

## <a name="next-steps"></a>Próximas etapas
Agora você preparou com êxito o servidor para replicação. O próximo artigo ensina como configurar a Replicação Transacional: 

> [!div class="nextstepaction"]
> [Tutorial: Configurar a replicação entre dois servidores totalmente conectados (Transacional)](tutorial-replicating-data-between-continuously-connected-servers.md)

  
  
