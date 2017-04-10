---
title: "Gerenciar os servi&#231;os do Mecanismo de Banco de Dados | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL Server Configuration Manager, acessando"
  - "Mecanismo de Banco de Dados [SQL Server], serviços"
  - "gerenciamento de serviços [SQL Server], sobre o gerenciamento de serviço"
  - "serviços [SQL Server]"
  - "SQL Server Agent, gerenciando"
  - "Serviços do SQL Server, sobre o serviço do SQL Server"
  - "MSSQLServer"
  - "configuração do servidor [SQL Server]"
  - "serviços de gerenciamento [SQL Server]"
  - "serviço do SQL Server Agent"
  - "serviços [SQL Server], gerenciando"
  - "administrando o SQL Server, serviços"
  - "serviços do SQL Server"
ms.assetid: aa732e43-53ba-4eea-bb9b-089da0766fc1
caps.latest.revision: 43
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 43
---
# Gerenciar os servi&#231;os do Mecanismo de Banco de Dados
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado nos sistemas operacionais como um serviço. Um serviço é um tipo de aplicativo executado em segundo plano no sistema. Os serviços normalmente fornecem recursos essenciais de sistema operacional, como fornecimento de Web, registro de eventos ou fornecimento de arquivos. Serviços podem ser executados sem exibir uma interface de usuário na área de trabalho do computador. O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e diversos outros componentes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são executados como serviços. Estes serviços normalmente são iniciados quando o sistema operacional inicia. Isto depende do que é especificado durante a instalação; alguns serviços não são iniciados por padrão. Esta seção descreve o gerenciamento de diversos serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Antes de você fazer o logon em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você precisa saber iniciar, interromper, pausar, retomar e reinicializar uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Depois que você fizer logon, você pode executar tarefas como administrar o servidor ou fazer consultas em um banco de dados.  
  
## Usando o SQL Server Service  
 Quando você inicia uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], você estará iniciando o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Depois que o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for inicializado, os usuários poderão estabelecer novas conexões com o servidor. O serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser iniciado e interrompido como um serviço, seja local ou remotamente. O serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será chamado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER) se for a instância padrão ou de MSSQL$*\<instancename>* se for uma instância nomeada.  
  
## Usando o SQL Server Configuration Manager  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Configuration Manager permite que você interrompa, inicie ou pause diversos serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Configuration Manager não pode gerenciar serviços do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
 Você também pode usar o Gerenciador de Configurações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para exibir as propriedades do serviço selecionado. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Configuration Manager é um snap-in do MMC ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console). Para obter mais informações sobre o MMC e como funciona um snap-in, veja a Ajuda do Windows.  
  
 **Para acessar o SQL Server Configuration Manager**  
  
-   No menu **Iniciar** , aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
 **Para acessar o SQL Server Configuration Manager usando o Windows 8**  
  
 Como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager é um snap-in do programa [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console (MMC) e não um programa autônomo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager não aparece como um aplicativo ao executar o Windows 8. Para abrir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, no botão **Pesquisar**, em **Aplicativos**, digite **SQLServerManager12.msc** (para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]), **SQLServerManager11.msc** (para [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) ou **SQLServerManager10.msc** para ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) e pressione **Enter**.  
  
## Nesta seção  
  
|||  
|-|-|  
|[Requisitos de segurança para gerenciar serviços](../../database-engine/configure-windows/security-requirements-for-managing-services.md)|[Impedir a inicialização automática de uma instância do SQL Server &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/scm services - prevent automatic startup of an instance.md)|  
|[Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)|[Alterar a conta de inicialização do serviço SQL Server &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/scm-services-change-the-service-startup-account.md)|  
|[Executar o SQL Server com ou sem uma rede](../../database-engine/configure-windows/run-sql-server-with-or-without-a-network.md)|[Configurar opções de inicialização do servidor &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/configure-server-startup-options-sql-server-configuration-manager.md)|  
|[Serviço SQL Server Browser &#40;Mecanismo de Banco de Dados e SSAS&#41;](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)|[Alterar a senha das contas usadas pelo SQL Server &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/scm services - change the password of the accounts used.md)|  
|[Opções de inicialização do serviço Mecanismo de Banco de Dados](../../database-engine/configure-windows/database-engine-service-startup-options.md)|[Configurar logs de erros do SQL Server](../../database-engine/configure-windows/configure-sql-server-error-logs.md)|  
|[Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](../../database-engine/configure-windows/start, stop, pause, resume, restart sql server services.md)|[Alterar modo de autenticação do servidor](../../database-engine/configure-windows/change-server-authentication-mode.md)|  
|[Iniciar o SQL Server no modo de usuário único](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)|[Serviço do gravador do SQL](../../database-engine/configure-windows/sql-writer-service.md)|  
|[Iniciar o SQL Server com configuração mínima](../../database-engine/configure-windows/start-sql-server-with-minimal-configuration.md)|[Difundir uma mensagem de desligamento &#40;prompt de comando&#41;](../../database-engine/configure-windows/broadcast-a-shutdown-message-command-prompt.md)|  
|[Conectar-se a um outro computador &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/connect-to-another-computer-sql-server-configuration-manager.md)|[Fazer logon em uma instância do SQL Server &#40;Prompt de Comando&#41;](../../database-engine/configure-windows/log-in-to-an-instance-of-sql-server-command-prompt.md)|  
|[Definir uma instância do SQL Server para iniciar automaticamente &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/scm services - set an instance to start automatically.md)|[Configurar permissões do sistema de arquivos para acesso ao mecanismo de banco de dados](../../database-engine/configure-windows/configure-file-system-permissions-for-database-engine-access.md)|  
  
## Conteúdo relacionado  
 [Configurar o SQL Server Agent](../../ssms/agent/configure-sql-server-agent.md)  
  
 [Fazendo o logon no SQL Server](../../database-engine/configure-windows/logging-in-to-sql-server.md)  
  
  