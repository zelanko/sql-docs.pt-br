---
title: Gerenciar os serviços do Mecanismo de Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Configuration Manager, accessing
- Database Engine [SQL Server], services
- managing services [SQL Server], about service management
- services [SQL Server]
- SQL Server Agent service, managing
- SQL Server services, about SQL Server service
- MSSQLServer
- server configuration [SQL Server]
- managing services [SQL Server]
- SQL Server Agent service
- services [SQL Server], managing
- administering SQL Server, services
- SQL Server services
ms.assetid: aa732e43-53ba-4eea-bb9b-089da0766fc1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8b12a6d599a9d740dc78f8b1545fb0dbf029cbde
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935229"
---
# <a name="manage-the-database-engine-services"></a>Gerenciar os serviços do Mecanismo de Banco de Dados
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado nos sistemas operacionais como um serviço. Um serviço é um tipo de aplicativo executado em segundo plano no sistema. Os serviços normalmente fornecem recursos essenciais de sistema operacional, como fornecimento de Web, registro de eventos ou fornecimento de arquivos. Serviços podem ser executados sem exibir uma interface de usuário na área de trabalho do computador. O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e diversos outros componentes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são executados como serviços. Estes serviços normalmente são iniciados quando o sistema operacional inicia. Isto depende do que é especificado durante a instalação; alguns serviços não são iniciados por padrão. Esta seção descreve o gerenciamento de diversos serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Antes de você fazer o logon em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você precisa saber iniciar, interromper, pausar, retomar e reinicializar uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Depois que você fizer logon, você pode executar tarefas como administrar o servidor ou fazer consultas em um banco de dados.  
  
## <a name="using-the-sql-server-service"></a>Usando o SQL Server Service  
 Quando você inicia uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], você estará iniciando o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Depois que o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for inicializado, os usuários poderão estabelecer novas conexões com o servidor. O serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser iniciado e interrompido como um serviço, seja local ou remotamente. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço é conhecido como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER) se for a instância padrão ou MSSQL $ *\<instancename>* se for uma instância nomeada.  
  
## <a name="using-sql-server-configuration-manager"></a>Usando o SQL Server Configuration Manager  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Configuration Manager permite que você interrompa, inicie ou pause diversos serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager não pode gerenciar serviços do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
 Você também pode usar o Gerenciador de Configurações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para exibir as propriedades do serviço selecionado. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Configuration Manager é um snap-in do MMC ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console). Para obter mais informações sobre o MMC e como funciona um snap-in, veja a Ajuda do Windows.  
  
 **Para acessar o SQL Server Configuration Manager**  
  
-   No menu **Iniciar** , aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
 **Para acessar o SQL Server Configuration Manager usando o Windows 8**  
  
 Como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager é um snap-in do programa [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console (MMC) e não um programa autônomo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager não aparece como um aplicativo ao executar o Windows 8. Para abrir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, no botão **Pesquisar** , em **Aplicativos**, digite **SQLServerManager12.msc** (para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]), **SQLServerManager11.msc** (para [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) ou **SQLServerManager10.msc** para ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) e pressione **Enter**.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|||  
|-|-|  
|[Requisitos de segurança para gerenciar serviços](security-requirements-for-managing-services.md)|[Impedir a inicialização automática de uma instância do SQL Server &#40;SQL Server Configuration Manager&#41;](scm-services-prevent-automatic-startup-of-an-instance.md)|  
|[Configurar contas de serviço e permissões do Windows](configure-windows-service-accounts-and-permissions.md)|[Alterar a conta de inicialização do serviço SQL Server &#40;SQL Server Configuration Manager&#41;](scm-services-change-the-service-startup-account.md)|  
|[Executar o SQL Server com ou sem uma rede](run-sql-server-with-or-without-a-network.md)|[Configurar opções de inicialização do servidor &#40;SQL Server Configuration Manager&#41;](scm-services-configure-server-startup-options.md)|  
|[Serviço SQL Server Browser &#40;Mecanismo de Banco de Dados e SSAS&#41;](sql-server-browser-service-database-engine-and-ssas.md)|[Alterar a senha das contas usadas pelo SQL Server &#40;SQL Server Configuration Manager&#41;](scm-services-change-the-password-of-the-accounts-used.md)|  
|[Opções de inicialização do serviço Mecanismo de Banco de Dados](database-engine-service-startup-options.md)|[Configurar logs de erros do SQL Server](scm-services-configure-sql-server-error-logs.md)|  
|[Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](start-stop-pause-resume-restart-sql-server-services.md)|[Alterar modo de autenticação do servidor](change-server-authentication-mode.md)|  
|[Iniciar o SQL Server no modo de usuário único](start-sql-server-in-single-user-mode.md)|[Serviço Gravador do SQL](sql-writer-service.md)|  
|[Iniciar o SQL Server com configuração mínima](start-sql-server-with-minimal-configuration.md)|[Difundir uma mensagem de desligamento &#40;prompt de comando&#41;](broadcast-a-shutdown-message-command-prompt.md)|  
|[Conectar-se a um outro computador &#40;SQL Server Configuration Manager&#41;](scm-services-connect-to-another-computer.md)|[Fazer logon em uma instância do SQL Server &#40;Prompt de Comando&#41;](log-in-to-an-instance-of-sql-server-command-prompt.md)|  
|[Definir uma instância do SQL Server para iniciar automaticamente &#40;SQL Server Configuration Manager&#41;](scm-services-set-an-instance-to-start-automatically.md)|[Configurar permissões do sistema de arquivos para acesso ao Mecanismo de Banco de Dados](configure-file-system-permissions-for-database-engine-access.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Configurar o SQL Server Agent](../../ssms/agent/sql-server-agent.md)  
  
 [Fazendo o logon no SQL Server](logging-in-to-sql-server.md)  
  
  
