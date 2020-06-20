---
title: Iniciar, parar, pausar, retomar, reiniciar o Mecanismo de Banco de Dados, SQL Server Agent ou SQL Server Browser serviço | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Configuration Manager, start and stop services
- stopping SQL Server Agent
- parameters [SQL Server], startup options
- SQL Server, startup options
- Database Engine [SQL Server], starting and stopping services
- pausing SQL Server
- PowerShell [SQL Server], starting and stopping services
- single-user mode [SQL Server], starting in
- SQL Server Management Studio [SQL Server], starting or stopping services
- stopping SQL Server Browser service
- starting SQL Server Agent
- default instances [SQL Server], starting and stopping
- SQL Server Agent, starting and stopping
- command prompt [SQL Server], starting and stopping SQL Server services
- continuing SQL Server
- starting SQL Server Database Engine
- net stop commands [SQL Server]
- command prompt [SQL Server], SQL Browser service
- Configuration Manager, start and stop services
- resuming SQL Server
- startup options [SQL Server]
- named instances [SQL Server], starting and stopping
- net start commands [SQL Server]
- SQL Server, starting and stopping
- stopping SQL Server
- starting SQL Server Browser service
- SQL Server Database Engine setting startup options
- administering SQL Server, starting and stopping services
- Management Studio [SQL Server], starting or stopping services
ms.assetid: 32660a02-e5a1-411a-9e57-7066ca459df6
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f4b102c8fd81923d7386c8e556896e715311a07e
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934767"
---
# <a name="start-stop-pause-resume-restart-the-database-engine-sql-server-agent-or-sql-server-browser-service"></a>Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser
  Este tópico descreve como iniciar, parar, pausar, retomar ou reiniciar o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente ou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço navegador do usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , comandos **net** em um prompt de comando, [!INCLUDE[tsql](../../includes/tsql-md.md)] ou PowerShell.  
  
-   **Antes de começar:**  
  
    -   [O que são estes serviços?](#Services)  
  
    -   [Informações adicionais](#MoreInformation)  
  
    -   [Segurança](#Security)  
  
-   **Instruções usando:**  
  
    -   [SQL Server Configuration Manager](#SSCMProcedure)  
  
    -   [SQL Server Management Studio](#SSMSProcedure)  
  
    -   [Comandos net em uma janela do prompt de comando](#CommandPrompt)  
  
    -   [Transact-SQL](#TsqlProcedure)  
  
    -   [PowerShell](#PowerShellProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="what-is-the-ssdenoversion-service-the-ssnoversion-agent-service-and-the-ssnoversion-browser-service"></a><a name="Services"></a> O que é o serviço [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser?  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são programas executáveis usados como um serviço do Windows. Programas executados como um serviço do Windows podem continuar operando sem exibir qualquer atividade na tela do computador.  
  
 **[!INCLUDE[ssDE](../../includes/ssde-md.md)]serviço**  
 O processo executável que é o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] pode ser a instância padrão (limite de uma por computador) ou pode ser uma de muitas instâncias nomeadas do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Use o Gerenciador de Configurações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para determinar quais instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)] são instaladas no computador. A instância padrão (se você a instala) está listada como ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER)**. As instâncias nomeadas (se você instalá-las) são listadas como ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (<instance_name>)**. Por padrão, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Express é instalado como ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQLExpress)**.  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Serviço do agente**  
 Um serviço Windows que executa tarefas administrativas agendadas, chamadas trabalhos e alertas. Para obter mais informações, consulte [SQL Server Agent](../../ssms/agent/sql-server-agent.md). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não está disponível em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Serviço browser**  
 Um serviço Windows que escuta solicitações de entrada para recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e fornece informações de clientes sobre instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas no computador. Uma única instância do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser é usada para todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas no computador.  
  
###  <a name="additional-information"></a><a name="MoreInformation"></a>Informações adicionais  
  
-   Pausar o serviço [!INCLUDE[ssDE](../../includes/ssde-md.md)] impede que novos usuários se conectem ao [!INCLUDE[ssDE](../../includes/ssde-md.md)], mas os usuários que já estão conectados podem continuar trabalhando até que suas conexões sejam interrompidas. Use a pausa quando você quiser esperar que os usuários concluam o trabalho antes de parar o serviço. Isso os permite que eles concluam as transações em andamento. Retomar permite que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] aceite novas conexões novamente. Não é possível pausar ou retomar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Service.  
  
-   O Gerenciador de Configurações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] exibem o status atual dos serviços usando os ícones a seguir.  
  
     **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Configuration Manager**  
  
    -   Uma seta verde no ícone próximo ao nome do serviço indica que ele foi iniciado.  
  
    -   Um quadrado vermelho no ícone próximo ao nome do serviço indica que ele foi parado.  
  
    -   Duas linhas azuis verticais no ícone próximo ao nome do serviço indicam que ele foi pausado.  
  
    -   Quando o [!INCLUDE[ssDE](../../includes/ssde-md.md)]for reiniciado, um quadrado vermelho indicará que o serviço parou e uma seta verde indicará que ele foi iniciado com êxito.  
  
     **[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
    -   Uma seta branca em um ícone de círculo verde próximo ao nome do serviço indica que ele foi iniciado.  
  
    -   Um quadrado branco nem um ícone de círculo vermelho próximo ao nome do serviço indica que ele foi parado.  
  
    -   Duas linhas brancas verticais em um ícone de círculo azul próximo ao nome do serviço indicam que ele foi pausado.  
  
-   Ao usar o Gerenciador de Configurações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], somente opções que são possíveis estarão disponíveis. Por exemplo, se o serviço já foi iniciado, **Iniciar** estará indisponível.  
  
-   Durante a execução em um cluster, o serviço [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] é gerenciador melhor com o uso do Administrador de Cluster.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Por padrão, apenas membros do grupo de administradores local podem iniciar, interromper, pausar, retomar ou reiniciar um serviço. Para conceder a capacidade de gerenciar serviços a não administradores, consulte [Como conceder aos usuários direitos para gerenciar serviços no Windows Server 2003](https://support.microsoft.com/kb/325349). (O processo é semelhante em outras versões do Windows.)  
  
 Parar o usando [!INCLUDE[ssDE](../../includes/ssde-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)] `SHUTDOWN` comando requer a associação nas funções de servidor fixas **sysadmin** ou **ServerAdmin** e não é transferível.  
  
##  <a name="using-ssnoversion-configuration-manager"></a><a name="SSCMProcedure"></a> Usando o Gerenciador de Configurações [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-an-instance-of-the-ssdenoversion"></a>Para iniciar, parar, pausar, retomar ou reiniciar a instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
2.  (Se a caixa de diálogo **Controle de Conta de Usuário** aparecer, clique em **Sim**.  
  
3.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, no painel esquerdo, clique em **Serviços do SQL Server**.  
  
4.  No painel de resultados, clique com o botão direito do mouse em **SQL Server (MSSQLServer)** ou em uma instância nomeada e clique em **Iniciar**, **Parar**, **Pausar**, **Retomar**ou **Reiniciar**.  
  
5.  Clique em **OK** para fechar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
> [!NOTE]  
>  Para iniciar uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] com opções de inicialização, consulte [Configurar opções de inicialização do servidor &#40;SQL Server Configuration Manager&#41;](scm-services-configure-server-startup-options.md).  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-ssnoversion-browser-or-an-instance-of-the-ssnoversion-agent"></a>Para iniciar, parar, pausar, retomar ou reiniciar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser ou uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
2.  (Se a caixa de diálogo **Controle de Conta de Usuário** aparecer, clique em **Sim**.  
  
3.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, no painel esquerdo, clique em **Serviços do SQL Server**.  
  
4.  No painel de resultados, clique com o botão direito do mouse em ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] navegador**ou ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente (MSSQLServer)** ou ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente (<instance_name>)** para uma instância nomeada e, em seguida, clique em **Iniciar**, **parar**, **Pausar**, **retomar**ou **reiniciar**.  
  
5.  Clique em **OK** para fechar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
> [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não pode ser colocado em pausa.  
  
##  <a name="using-ssnoversion-management-studio"></a><a name="SSMSProcedure"></a> Usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-an-instance-of-the-ssdenoversion"></a>Para iniciar, parar, pausar, retomar ou reiniciar a instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]  
  
1.  No Pesquisador de Objetos, conecte-se à instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)], clique com o botão direito do mouse na instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que você deseja iniciar e clique em **Iniciar**, **Parar**, **Pausar**, **Retomar**ou **Reiniciar**.  
  
     Ou, em Servidores Registrados, clique com o botão direito do mouse na instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que você deseja iniciar, aponte para **Controle de Serviço**e clique em **Iniciar**, **Parar**, **Pausar**, **Retomar**ou **Reiniciar**.  
  
2.  (Se a caixa de diálogo **Controle de Conta de Usuário** aparecer, clique em **Sim**.  
  
3.  Quando solicitado a indicar se você deseja executar a ação, clique em **Sim**.  
  
#### <a name="to-start-stop-or-restart-the-an-instance-of-the-ssnoversion-agent"></a>Para iniciar, parar ou reiniciar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
1.  No Pesquisador de objetos, conecte-se à instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] , clique com o botão direito do mouse em ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente**e clique em **Iniciar**, **parar**ou **reiniciar**.  
  
2.  (Se a caixa de diálogo **Controle de Conta de Usuário** aparecer, clique em **Sim**.  
  
3.  Quando solicitado a indicar se você deseja executar a ação, clique em **Sim**.  
  
##  <a name="from-the-command-prompt-window-using-net-commands"></a><a name="CommandPrompt"></a>Na janela do prompt de comando usando comandos net  
 Os serviços do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser iniciados, interrompidos ou colocados em pausa com os comandos **net** do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
###  <a name="to-start-the-default-instance-of-the-ssde"></a><a name="dbDefault"></a>Para iniciar a instância padrão do[!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   Em um prompt de comando, digite um dos seguintes comandos:  
  
     **net start "SQL Server (MSSQLSERVER)"**  
  
     -ou-  
  
     **net start MSSQLSERVER**  
  
###  <a name="to-start-a-named-instance-of-the-ssde"></a><a name="dbNamed"></a> Para iniciar uma instância nomeada do [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   Em um prompt de comando, digite um dos comandos a seguir. Substituir *\<instancename>* pelo nome da instância que você deseja gerenciar.  
  
     **net start "SQL Server (** *instancename* **)"**  
  
     -ou-  
  
     **net start MSSQL$** *instancename*  
  
###  <a name="to-start-the-ssde-with-startup-options"></a><a name="dbStartup"></a> Para iniciar o [!INCLUDE[ssDE](../../includes/ssde-md.md)] com opções de inicialização  
  
-   Adicione opções de inicialização ao final da instrução **net start "SQL Server (MSSQLSERVER)"** , separadas por espaço. Quando começar usando **net start**, as opções de inicialização usam uma barra (/) em vez de um hífen (-).  
  
     **net start "SQL Server (MSSQLSERVER)" /f /m**  
  
     -ou-  
  
     **net start MSSQLSERVER /f /m**  
  
    > [!NOTE]  
    >  Para obter mais informações sobre as opções de inicialização, consulte [Opções de inicialização do serviço Mecanismo de Banco de Dados](database-engine-service-startup-options.md).  
  
###  <a name="to-start-the-ssnoversion-agent-on-the-default-instance-of-ssnoversion"></a><a name="agDefault"></a> Para iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent na instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Em um prompt de comando, digite um dos seguintes comandos:  
  
     **net start "SQL Server Agent (MSSQLSERVER)"**  
  
     -ou-  
  
     **net start SQLSERVERAGENT**  
  
###  <a name="to-start-the-ssnoversion-agent-on-a-named-instance-of-ssnoversion"></a><a name="agNamed"></a> Para iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent em uma instância nomeada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Em um prompt de comando, digite um dos comandos a seguir. Substitua *instancename* pelo nome da instância que você deseja gerenciar.  
  
     **net start "SQL Server Agent(** *instancename* **)"**  
  
     -ou-  
  
     **net start SQLAgent$** *instancename*  
  
 Para obter informações sobre como executar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent em modo detalhado para solução de problemas, consulte [sqlagent90 Application](../../tools/sqlagent90-application.md).  
  
###  <a name="to-start-the-ssnoversion-browser"></a><a name="Browser"></a> Para iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser  
  
-   Em um prompt de comando, digite um dos seguintes comandos:  
  
     **net start "SQL Server Browser"**  
  
     -ou-  
  
     **net start SQLBrowser**  
  
###  <a name="to-pause-or-stop-services-from-the-command-prompt-window"></a><a name="pauseStop"></a> Para pausar ou parar os serviços na janela Prompt de Comando  
  
-   Para pausar ou parar serviços, modifique os comandos das maneiras a seguir.  
  
    -   Para pausar um serviço, substitua **net start** por **net pause**.  
  
    -   Para pausar um serviço, substitua **net start** com **net pause**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] pode ser parado com a instrução `SHUTDOWN`.  
  
#### <a name="to-stop-the-ssde-using-tsql"></a>Para parar o [!INCLUDE[ssDE](../../includes/ssde-md.md)] usando [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
-   Para aguardar a conclusão de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] e procedimentos armazenados em execução atualmente e parar o [!INCLUDE[ssDE](../../includes/ssde-md.md)], execute a instrução a seguir.  
  
    ```sql  
    SHUTDOWN;   
    ```  
  
-   Para parar o [!INCLUDE[ssDE](../../includes/ssde-md.md)] imediatamente, execute a instrução a seguir.  
  
    ```sql  
    SHUTDOWN WITH NOWAIT;   
    ```  
  
 Para obter mais informações sobre a `SHUTDOWN` instrução, consulte [Shutdown &#40;TRANSACT-SQL&#41;](/sql/t-sql/language-elements/shutdown-transact-sql).  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Usando o PowerShell  
  
#### <a name="to-start-and-stop-ssde-services"></a>Para iniciar e parar os serviços [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
1.  Em uma janela Prompt de Comando, inicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell executando o comando a seguir.  
  
    ```ms-dos  
    sqlps  
    ```  
  
2.  Em um prompt de comando do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell, executando o comando a seguir. Substitua `computername` pelo nome do seu computador.  
  
    ```powershell  
    # Get a reference to the ManagedComputer class.  
    CD SQLSERVER:\SQL\computername  
    $Wmi = (Get-Item .).ManagedComputer
    ```  
  
3.  Identifique o serviço que você deseja parar ou iniciar. Escolha uma das linhas a seguir. Substitua `instancename` pelo nome da instância nomeada.  
  
    -   Para obter uma referência à instância padrão do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['MSSQLSERVER']  
        ```  
  
    -   Para obter uma referência a uma instância nomeada do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['MSSQL$instancename']  
        ```  
  
    -   Para obter uma referência ao serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent na instância padrão do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLSERVERAGENT']  
        ```  
  
    -   Para obter uma referência ao serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent em uma instância nomeada do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLAGENT$instancename']  
        ```  
  
    -   Para obter uma referência ao serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser.  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLBROWSER']  
        ```  
  
4.  Conclua o exemplo para iniciar e parar o serviço selecionado.  
  
    ```powershell  
    # Display the state of the service.  
    $DfltInstance  
    # Start the service.  
    $DfltInstance.Start();  
    # Wait until the service has time to start.  
    # Refresh the cache.  
    $DfltInstance.Refresh();   
    # Display the state of the service.  
    $DfltInstance  
    # Stop the service.  
    $DfltInstance.Stop();  
    # Wait until the service has time to stop.  
    # Refresh the cache.  
    $DfltInstance.Refresh();   
    # Display the state of the service.  
    $DfltInstance  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar SQL Server com configuração mínima](start-sql-server-with-minimal-configuration.md)   
 [Recursos com suporte nas edições do SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
