---
title: Iniciar, parar, pausar, retomar e reiniciar os serviços SQL Server
description: Descubra como iniciar, parar, pausar, retomar ou reiniciar vários serviços SQL Server. Veja como usar o Transact-SQL, o PowerShell e outras ferramentas para essas ações.
ms.custom: ''
ms.date: 03/05/2020
ms.prod: sql
ms.prod_service: high-availability
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
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: e971592b20dd2321e4265752cb8b01c38387b639
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670749"
---
# <a name="start-stop-pause-resume-restart-sql-server-services"></a>Iniciar, parar, pausar, retomar e reiniciar os serviços SQL Server

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Este tópico descreve como iniciar, parar, pausar, retomar ou reiniciar o Mecanismo de Banco de Dados do SQL Server, o SQL Server Agent ou o serviço SQL Server Browser usando o SQL Server Configuration Manager, o SSMS (SQL Server Management Studio), os comandos .NET em um prompt de comando, o Transact-SQL ou o PowerShell.

## <a name="identify-the-service"></a>Identificar o serviço

Os componentes do SQL Server são programas executáveis executados como um serviço Windows. Programas executados como um serviço do Windows podem continuar operando sem exibir qualquer atividade na tela do computador.

### <a name="database-engine-service"></a>Serviço do Mecanismo de Banco de Dados

O processo executável que é o Mecanismo de Banco de Dados do SQL Server. O Mecanismo de Banco de Dados pode ser a instância padrão (limite de uma por computador) ou pode ser uma das muitas instâncias nomeadas do Mecanismo de Banco de Dados. Use o SQL Server Configuration Manager para determinar quais instâncias do Mecanismo de Banco de Dados estão instaladas no computador. A instância padrão (se você a instalar) será listada como **SQL Server (MSSQLSERVER)** . As instâncias nomeadas (se você as instalar) serão listadas como **SQL Server (<nome_da_instância>)** . Por padrão, o SQL Server Express é instalado como **SQL Server (SQLEXPRESS)** .

### <a name="sql-server-agent-service"></a>serviço do SQL Server Agent

Um serviço Windows que executa tarefas administrativas agendadas, chamadas trabalhos e alertas. Para obter mais informações, consulte [SQL Server Agent](../../ssms/agent/sql-server-agent.md). O SQL Server Agent não está disponível em todas as edições do SQL Server. Para obter uma lista dos recursos compatíveis com as edições do SQL Server, confira [Recursos compatíveis com as edições do SQL Server 2019](../../sql-server/editions-and-components-of-sql-server-version-15.md).

### <a name="sql-server-browser-service"></a>Serviço Navegador do SQL Server

Um serviço Windows que escuta as solicitações recebidas de recursos do SQL Server e fornece informações aos clientes sobre as instâncias do SQL Server instaladas no computador. Uma só instância do serviço SQL Server Browser é usada para todas as instâncias do SQL Server instaladas no computador.

### <a name="additional-information"></a>Informações adicionais

- A pausa do serviço Mecanismo de Banco de Dados impede que novos usuários se conectem ao Mecanismo de Banco de Dados, mas os usuários que já estão conectados podem continuar trabalhando até que as respectivas conexões sejam interrompidas. Use a pausa quando você quiser esperar que os usuários concluam o trabalho antes de parar o serviço. Isso os permite que eles concluam as transações em andamento. A opção *Retomar* permite que o Mecanismo de Banco de Dados aceite novas conexões novamente. Não é possível pausar nem retomar o serviço SQL Server Agent.  

- O SQL Server Configuration Manager e o SSMS exibem o status atual dos serviços usando os ícones a seguir.  

    **SQL Server Configuration Manager**

  - Uma seta verde no ícone próximo ao nome do serviço indica que ele foi iniciado.

  - Um quadrado vermelho no ícone próximo ao nome do serviço indica que ele foi parado.

  - Duas linhas azuis verticais no ícone próximo ao nome do serviço indicam que ele foi pausado.

  - Ao reinicializar o Mecanismo de Banco de Dados, um quadrado vermelho indica que o serviço parou e, em seguida, uma seta verde indica que ele foi iniciado com êxito.

    **SQL Server Management Studio (SSMS)**

  - Uma seta branca em um ícone de círculo verde próximo ao nome do serviço indica que ele foi iniciado.  

  - Um quadrado branco nem um ícone de círculo vermelho próximo ao nome do serviço indica que ele foi parado.  

  - Duas linhas brancas verticais em um ícone de círculo azul próximo ao nome do serviço indicam que ele foi colocado em pausa.  

- Ao usar o SQL Server Configuration Manager ou o SSMS, somente as opções que são possíveis ficam disponíveis. Por exemplo, se o serviço já foi iniciado, a opção **Iniciar** fica indisponível.

- Durante a execução em um cluster, o serviço Mecanismo de Banco de Dados do SQL Server é mais bem gerenciador com o uso do Administrador de Cluster.  

### <a name="security"></a>Segurança

#### <a name="permissions"></a>Permissões

Por padrão, apenas os membros do grupo local de administradores podem iniciar, parar, pausar, retomar ou reiniciar um serviço. Para conceder a capacidade de gerenciar serviços a não administradores, consulte [Como conceder aos usuários direitos para gerenciar serviços no Windows Server 2003](https://support.microsoft.com/kb/325349). (O processo é semelhante em outras versões do Windows Server.)

A interrupção do Mecanismo de Banco de Dados usando o comando **SHUTDOWN** do Transact-SQL exige a associação às funções de servidor fixas **sysadmin** ou **serveradmin** e não é transferível.

## <a name="sql-server-configuration-manager"></a>SQL Server Configuration Manager

### <a name="starting-sql-server-configuration-manager"></a>Como iniciar o SQL Server Configuration Manager

No menu **Iniciar** , aponte para **Todos os Programas**, **Microsoft SQL Server**, **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.

Como o SQL Server Configuration Manager é um snap-in do programa Console de Gerenciamento Microsoft e não um programa autônomo, o SQL Server Configuration Manager não é exibido como um aplicativo nas versões mais recentes do Windows. Aqui estão os caminhos para as últimas quatro versões do Windows instaladas na unidade C.  

|Versão|Caminho|
|-|-|
|SQL Server 2019|C:\Windows\SysWOW64\SQLServerManager15.msc|
|Microsoft SQL Server 2017|C:\Windows\SysWOW64\SQLServerManager14.msc|
|SQL Server 2016|C:\Windows\SysWOW64\SQLServerManager13.msc|
|SQL Server 2014|C:\Windows\SysWOW64\SQLServerManager12.msc|
|SQL Server 2012|C:\Windows\SysWOW64\SQLServerManager11.msc|

#### <a name="to-start-stop-pause-resume-or-restart-an-instance-of-the-sql-server-database-engine"></a><a name="configmande"></a> Para iniciar, parar, pausar, retomar ou reiniciar uma instância do Mecanismo de Banco de Dados do SQL Server

1. Inicie o SQL Server Configuration Manager usando as instruções acima.

2. (Se a caixa de diálogo **Controle de Conta de Usuário** aparecer, clique em **Sim**.

3. No SQL Server Configuration Manager, no painel esquerdo, clique em **Serviços do SQL Server**.

4. No painel de resultados, clique com o botão direito do mouse em **SQL Server (MSSQLServer)** ou em uma instância nomeada e clique em **Iniciar**, **Parar**, **Pausar**, **Retomar**ou **Reiniciar**.

5. Clique em **OK** para fechar o SQL Server Configuration Manager.

> [!NOTE]
> Para iniciar uma instância do Mecanismo de Banco de Dados do SQL Server com opções de inicialização, confira [Configurar opções de inicialização do servidor &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md).  

#### <a name="to-start-stop-pause-resume-or-restart-the-sql-server-browser-or-an-instance-of-the-sql-server-agent"></a>Para iniciar, parar, pausar, retomar ou reiniciar o SQL Server Browser ou uma instância do SQL Server Agent

1. Inicie o SQL Server Configuration Manager usando as instruções acima.

2. (Se a caixa de diálogo **Controle de Conta de Usuário** aparecer, clique em **Sim**.

3. No SQL Server Configuration Manager, no painel esquerdo, clique em **Serviços do SQL Server**.

4. No painel de resultados, clique com o botão direito do mouse no **SQL Server Browser**, no **SQL Server Agent (MSSQLServer)** ou no **SQL Server Agent (<nome_da_instância>)** em uma instância nomeada e, em seguida, clique em **Iniciar**, **Parar**, **Pausar**, **Retomar** ou **Reiniciar**.  

5. Clique em **OK** para fechar o SQL Server Configuration Manager.  

> [!NOTE]
> O SQL Server Agent não pode ser colocado em pausa.

## <a name="sql-server-management-studio"></a>SQL Server Management Studio

### <a name="to-start-stop-pause-resume-or-restart-an-instance-of-the-sql-server-database-engine"></a><a name="ssmsde"></a> Para iniciar, parar, pausar, retomar ou reiniciar uma instância do Mecanismo de Banco de Dados do SQL Server

1. No Pesquisador de Objetos, conecte-se à instância do Mecanismo de Banco de Dados, clique com o botão direito do mouse na instância do Mecanismo de Banco de Dados que deseja iniciar e, em seguida, clique em **Iniciar**, **Parar**, **Pausar**, **Retomar** ou **Reiniciar**.

    Ou então, em Servidores Registrados, clique com o botão direito do mouse na instância do Mecanismo de Banco de Dados que deseja iniciar, aponte para **Controle de Serviço** e, em seguida, clique em **Iniciar**, **Parar**, **Pausar**, **Retomar** ou **Reiniciar**.

2. (Se a caixa de diálogo **Controle de Conta de Usuário** aparecer, clique em **Sim**.

3. Quando solicitado se você deseja executar uma ação, clique em **Sim**.  

#### <a name="to-start-stop-or-restart-an-instance-of-the-sql-server-agent"></a>Para iniciar, parar ou reiniciar uma instância do SQL Server Agent

1. No Pesquisador de Objetos, conecte-se à instância do Mecanismo de Banco de Dados, clique com o botão direito do mouse no **SQL Server Agent** e, em seguida, clique em **Iniciar**, **Parar** ou **Reiniciar**.

2. (Se a caixa de diálogo **Controle de Conta de Usuário** aparecer, clique em **Sim**.

3. Quando solicitado se você deseja executar uma ação, clique em **Sim**.

## <a name="command-prompt-window-using-net-commands"></a><a name="CommandPrompt"></a> Janela do prompt de comando usando comandos .NET

Os serviços do Microsoft SQL Server podem ser iniciados, parados ou colocados em pausa com os comandos do Microsoft Windows **.NET**.

### <a name="to-start-the-default-instance-of-the-database-engine"></a><a name="dbDefault"></a> Para iniciar a instância padrão do Mecanismo de Banco de Dados

- Em um prompt de comando, digite um dos seguintes comandos:  
  
    **net start "SQL Server (MSSQLSERVER)"**

   -ou-  

    **net start MSSQLSERVER**

### <a name="to-start-a-named-instance-of-the-database-engine"></a><a name="dbNamed"></a> Para iniciar uma instância nomeada do Mecanismo de Banco de Dados

- Em um prompt de comando, digite um dos comandos a seguir. Substitua *\<instancename>* pelo nome da instância que você deseja gerenciar.  
  
    **net start "SQL Server (** *instancename* **)"**
  
   -ou-  
  
    **net start MSSQL$** *instancename*  
  
### <a name="to-start-the-database-engine-with-startup-options"></a><a name="dbStartup"></a> Para iniciar o Mecanismo de Banco de Dados com opções de inicialização  

- Adicione opções de inicialização ao final da instrução **net start "SQL Server (MSSQLSERVER)"** , separadas por espaço. Quando começar usando **net start**, as opções de inicialização usam uma barra (/) em vez de um hífen (-).  
  
    **net start "SQL Server (MSSQLSERVER)" /f /m**
  
   -ou-  
  
    **net start MSSQLSERVER /f /m**
  
  > [!NOTE]
  >  Para obter mais informações sobre as opções de inicialização, consulte [Opções de inicialização do serviço Mecanismo de Banco de Dados](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
###  <a name="to-start-the-sql-server-agent-on-the-default-instance-of-sql-server"></a><a name="agDefault"></a> Para iniciar o SQL Server Agent na instância padrão do SQL Server
  
- Em um prompt de comando, digite um dos seguintes comandos:  
  
    **net start "SQL Server Agent (MSSQLSERVER)"**
  
   -ou-  
  
    **net start SQLSERVERAGENT**
  
###  <a name="to-start-the-sql-server-agent-on-a-named-instance-of-sql-server"></a><a name="agNamed"></a> Para iniciar o SQL Server Agent em uma instância nomeada do SQL Server  
  
- Em um prompt de comando, digite um dos comandos a seguir. Substitua *instancename* pelo nome da instância que você deseja gerenciar.  
  
    **net start "SQL Server Agent(** *instancename* **)"**
  
   -ou-  
  
    **net start SQLAgent$** *instancename*  
  
 Para obter informações sobre como executar o SQL Server Agent no modo detalhado para solução de problemas, confira [Aplicativo sqlagent90](../../tools/sqlagent90-application.md).  

### <a name="to-start-the-sql-server-browser"></a><a name="Browser"></a> Para iniciar o SQL Server Browser  

- Em um prompt de comando, digite um dos seguintes comandos:  
  
    **net start "SQL Server Browser"**
  
   -ou-  
  
    **net start SQLBrowser**
  
### <a name="to-pause-or-stop-services-from-the-command-prompt-window"></a><a name="pauseStop"></a> Para pausar ou parar os serviços na janela Prompt de Comando  

- Para pausar ou parar serviços, modifique os comandos conforme mostrado a seguir.  

- Para pausar um serviço, substitua **net start** por **net pause**.  

- Para pausar um serviço, substitua **net start** com **net pause**.  

## <a name="transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL

O Mecanismo de Banco de Dados pode ser interrompido com a instrução **SHUTDOWN**.  

### <a name="to-stop-the-database-engine-using-transact-sql"></a>Para interromper o Mecanismo de Banco de Dados usando o Transact-SQL

- Para aguardar a conclusão das instruções Transact-SQL e dos procedimentos armazenados atualmente em execução e, em seguida, parar o Mecanismo de Banco de Dados, execute a instrução a seguir.  
  
    ```sql
    SHUTDOWN;
    ```
  
- Para interromper o Mecanismo de Banco de Dados imediatamente, execute a instrução a seguir.  
  
    ```sql
    SHUTDOWN WITH NOWAIT;
    ```

Para obter mais informações sobre a instrução **SHUTDOWN**, consulte [SHUTDOWN &#40;Transact-SQL&#41;](../../t-sql/language-elements/shutdown-transact-sql.md).  

## <a name="powershell"></a><a name="PowerShellProcedure"></a> PowerShell

### <a name="to-start-and-stop-database-engine-services"></a>Para iniciar e parar serviços do Mecanismo de Banco de Dados

1. Em uma janela do prompt de comando, inicie o SQL Server PowerShell executando o comando a seguir.  

    ```cmd
    sqlps
    ```

2. Em um prompt de comando do SQL Server PowerShell, executando o comando a seguir. Substitua `computername` pelo nome do seu computador.  

    ```powershell
    # Get a reference to the ManagedComputer class.
    CD SQLSERVER:\SQL\computername
    $Wmi = (get-item .).ManagedComputer
    ```

3. Identifique o serviço que você deseja parar ou iniciar. Escolha uma das linhas a seguir. Substitua `instancename` pelo nome da instância nomeada.

    - Para obter uma referência à instância padrão do Mecanismo de Banco de Dados.

        ```powershell
        $DfltInstance = $Wmi.Services['MSSQLSERVER']
        ```

    - Para obter uma referência a uma instância nomeada do Mecanismo de Banco de Dados.

        ```powershell
        $DfltInstance = $Wmi.Services['MSSQL$instancename']
        ```

    - Para obter uma referência ao serviço SQL Server Agent na instância padrão do Mecanismo de Banco de Dados.  

        ```powershell
        $DfltInstance = $Wmi.Services['SQLSERVERAGENT']
        ```

    - Para obter uma referência ao serviço SQL Server Agent em uma instância nomeada do Mecanismo de Banco de Dados.  

        ```powershell
        $DfltInstance = $Wmi.Services['SQLAGENT$instancename']
        ```

    - Para obter uma referência ao serviço SQL Server Browser.

        ```powershell
        $DfltInstance = $Wmi.Services['SQLBROWSER']
        ```

4. Conclua o exemplo para iniciar e parar o serviço selecionado.
  
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
  
##  <a name="using-service-controller-class"></a><a name="ServiceController"></a> Usar a classe do controlador de serviço

Você pode usar a classe ServiceController para controlar o serviço do SQL Server ou qualquer outro serviço Windows. Para obter um exemplo de como fazer isso, confira [Classe ServiceController](/dotnet/api/system.serviceprocess.servicecontroller?view=netframework-4.8).

## <a name="manage-the-sql-server-service-on-linux"></a>Gerenciar o serviço SQL Server no Linux

### <a name="to-start-stop-or-restart-an-instance-of-the-sql-server-database-engine"></a>Para iniciar, parar ou reiniciar uma instância do Mecanismo de Banco de Dados do SQL Server

As seções a seguir mostram como iniciar, parar, reiniciar e verificar o status do [serviço SQL Server em Linux](../../linux/sql-server-linux-troubleshooting-guide.md#manage-the-sql-server-service).

Verifique o status do serviço SQL Server usando este comando:

   ```bash
   sudo systemctl status mssql-server
   ```

Você pode parar, iniciar ou reiniciar o serviço SQL Server, conforme necessário, usando os seguintes comandos:

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl start mssql-server
   sudo systemctl restart mssql-server
   ```

## <a name="next-steps"></a>Próximas etapas

- [Visão geral da documentação de instalação do SQL Server](../install-windows/install-sql-server.md)
- [Exibir e ler arquivos de log da Instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)
- [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md)
- [Iniciar o SQL Server com configuração mínima](../../database-engine/configure-windows/start-sql-server-with-minimal-configuration.md)
- [Recursos com suporte das edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)