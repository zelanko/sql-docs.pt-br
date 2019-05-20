---
title: Solução de problemas de conexão de banco de dados e de servidor com o Reporting Services | Microsoft Docs
ms.date: 02/28/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: 8bbb88df-72fd-4c27-91b7-b255afedd345
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1e44d8dde3f93a946a25cc8fe269a26f70a7432a
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65574112"
---
# <a name="troubleshoot-server-and-database-connection-problems-with-reporting-services"></a>Solucionar problemas de conexão de banco de dados e servidor com o Reporting Services
Use este tópico para solucionar problemas de conexão com um servidor de relatório. Este tópico também fornece informações sobre mensagens de "erro inesperado". Para saber mais sobre configuração de fonte de dados e como configurar a conexão do servidor de relatório, confira [Especificar informações de credenciais e de conexão para fontes de dados de relatório](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md) e [Configurar uma conexão de banco de dados do servidor de relatório (Gerenciador de configurações do SSRS)](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
## <a name="cannot-create-a-connection-to-data-source-datasourcename-rserroropeningconnection"></a>Não é possível criar uma conexão com uma fonte de dados 'datasourcename'. (rsErrorOpeningConnection)  
Este é um erro genérico que ocorre quando o servidor de relatório não pode abrir uma conexão com uma fonte de dados externa que fornece dados a um relatório. Este erro aparece com uma segunda mensagem de erro que indica a causa subjacente. Os erros adicionais a seguir podem aparecer com **rsErrorOpeningConnection**.  
  
### <a name="login-failed-for-user-username"></a>Falha no logon do usuário 'UserName'  
O usuário não tem permissão para acessar a fonte de dados. Se você estiver usando um banco de dados do SQL Server, verifique se o usuário tem um logon de usuário de banco de dados válido. Para saber mais sobre como criar um usuário de banco de dados ou um logon do SQL Server, confira [Criar um usuário de banco de dados](../../relational-databases/security/authentication-access/create-a-database-user.md) e [Criar um logon do SQL Server](../../relational-databases/security/authentication-access/create-a-login.md).  
  
### <a name="login-failed-for-user-nt-authorityanonymous-logon"></a>Falha no logon do usuário 'NT AUTHORITY\ANONYMOUS LOGON'  
Este erro ocorre quando as credenciais são transmitidas em várias conexões de computador. Se você estiver usando a Autenticação do Windows e o protocolo Kerberos versão 5 não estiver habilitado, este erro ocorrerá quando as credenciais forem transmitidas em mais de uma conexão de computador. Para resolver este erro, use credenciais armazenadas ou credenciais solicitadas. Para saber mais sobre como contornar esse problema, confira [Especificar informações de credenciais e de conexão para fontes de dados de relatório](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).  
  
### <a name="an-error-has-occurred-while-establishing-a-connection-to-the-server"></a>Ocorreu um erro ao estabelecer uma conexão com o servidor.  
Ao conectar-se ao SQL Server, essa falha pode ser provocada porque, sob as configurações padrão, o SQL Server não permite conexões remotas. (provedor: Provedor de Pipes Nomeados, erro: 40 - não foi possível abrir uma conexão com o SQL Server). Esse erro é retornado pela instância do Mecanismo de Banco de Dados que hospeda o banco de dados do servidor de relatório. Na maioria das vezes, esse erro ocorre porque o serviço SQL Server é interrompido. Ou, se você estiver usando o SQL Server Express com Advanced Services ou uma instância nomeada, esse erro ocorrerá caso a URL do servidor de relatório ou a cadeia de conexão do banco de dados de tal servidor não esteja correta. Para resolver esses problemas, siga este procedimento:  
  
* Verifique se o serviço SQL Server (**MSSQLSERVER**) foi iniciado. No computador que hospeda a instância do Mecanismo de Banco de Dados, clique em Iniciar, em Ferramentas Administrativas, em Serviços e role até o SQL Server (**MSSQLSERVER**). Se ele ainda não tiver sido iniciado, clique com o botão direito do mouse no serviço, selecione Propriedades, em Tipo de Inicialização, escolha Automático e clique consecutivamente em Aplicar, Iniciar e OK.   
* Verifique se a URL do servidor de relatório e a cadeia de conexão do banco de dados de tal servidor estão corretas. Se o Reporting Services ou o Mecanismo de Banco de Dados tiver sido instalado como uma instância nomeada, a cadeia de conexão padrão criada durante a Instalação incluirá o nome da instância. Por exemplo, se você instalou uma instância padrão do SQL Server Express com Advanced Services em um servidor denominado DEVSRV01, a URL do Gerenciador de Relatórios será DEVSRV01\Reports$SQLEXPRESS. Além disso, o nome de servidor de banco de dados na cadeia de conexão será semelhante a DEVSRV01\SQLEXPRESS. Para saber mais sobre URLs e cadeias de conexão de fonte de dados para SQL Server Express, confira [Reporting Services no SQL Server Express com Advanced Services](https://technet.microsoft.com/library/ms365166(v=sql.105).aspx). Para verificar a cadeia de conexão do banco de dados do servidor de relatório, inicie a ferramenta Configuração do Reporting Services e exiba a página Configuração do Banco de Dados.  
  
### <a name="a-connection-cannot-be-made-ensure-that-the-server-is-running"></a>Uma conexão não pode ser feita. Verifique se o servidor está em execução.  
Este erro é retornado pelo provedor ADOMD.NET. Há várias razões para a ocorrência desse erro. Se você tiver especificado o servidor como “localhost”, tente especificar o nome do servidor. Esse erro também poderá ocorrer se não for possível alocar a memória na nova conexão. Para saber mais, confira [o artigo 912017 da Base de Dados de Conhecimento — Mensagem de erro quando você se conectar a uma instância do SQL Server 2005 Analysis Services:](https://support.microsoft.com/kb/912017).  
  
Se o erro também incluir "Nenhum host desse tipo é conhecido", isso indica que o servidor do Analysis Services não está disponível ou está recusando a conexão. Se o servidor do Analysis Services estiver instalado como uma instância nomeada em um computador remoto, talvez seja necessário executar o serviço SQL Server Browser para obter o número da porta usada pela instância em questão.  
  
### <a name="report-services-soap-proxy-source"></a>(Origem do Proxy SOAP do Report Services)  
Se esse erro ocorrer durante a geração do modelo de relatório e a seção de informações adicionais incluir "O SQL Server não existe ou acesso foi negado", as seguintes condições podem existir:  
* A cadeia de conexão da fonte de dados inclui "localhost".  
* O TCP/IP está desabilitado para o serviço SQL Server.  
  
Para resolver este erro, modifique a cadeia de conexão para usar o nome do servidor ou habilite o TCP/IP para o serviço. Siga estas etapas para habilitar o TCP/IP:  
  
1. Inicie o SQL Server Configuration Manager  
2. Expanda **Configuração de Rede do SQL Server**.  
3. Selecione **Protocolos do MSSQLSERVER**.  
4. Clique com o botão direito do mouse em **TCP/IP**e escolha **Habilitar**.  
5. Escolha **Serviços do SQL Server**.  
6. Clique com o botão direito do mouse em **SQL Server (MSSQLSERVER)** e escolha **Reiniciar**.  
  
## <a name="wmi-error-when-connecting-to-a-report-server-in-management-studio"></a>Erro de WMI ao conectar-se a um servidor de relatório no Management Studio  
Por padrão, o Management Studio usa o provedor de WMI (Instrumentação de Gerenciamento do Windows) do Reporting Services para estabelecer uma conexão com o servidor de relatório. Se o provedor WMI não estiver instalado corretamente, o seguinte erro ocorrerá quando você tentar se conectar ao servidor de relatório:  
  
Não é possível se conectar ao \<your server name>. O provedor WMI do Reporting Services não está instalado ou está instalado incorretamente (Microsoft.SqlServer.Management.UI.RSClient).  
  
Para resolver esse erro, reinstale o software. Em todos os outros casos, como solução temporária, você pode se conectar ao servidor de relatório pelo ponto de extremidade SOAP:  
  
* Na caixa de diálogo **Conectar ao Servidor** no Management Studio, em **Nome do Servidor**, digite a URL do servidor de relatório. Por padrão, ela é `https://<your server name>/reportserver`. Ou se estiver usando o SQL Server 2008 Express com Advanced Services, ela será `https://<your server name>/reportserver$sqlexpress`.  
  
Para resolver o erro e conseguir se conectar usando o provedor de WMI, execute o programa de instalação para reparar o Reporting Services ou reinstale o Reporting Services.  
  
## <a name="connection-error-where-login-failed-due-to-unknown-user-name-or-bad-password"></a>Erro de conexão; o logon falhou devido a um nome de usuário desconhecido ou uma senha inválida  
Um erro **rsReportServerDatabaseLogonFailed** poderá ocorrer se você estiver usando uma conta de domínio para a conexão do servidor de relatório com o banco de dados do servidor de relatório e se a senha da conta de domínio tiver sido alterada.   
  
O texto completo do erro é: “O servidor de relatório não pode abrir uma conexão com seu banco de dados. Falha de logon (**rsReportServerDatabaseLogonFailed**). Falha de logon: nome de usuário desconhecido ou senha inválida”.  
  
Se a senha for redefinida, atualize a conexão. Para saber mais, confira [Configurar uma conexão de banco de dados do servidor de relatório (Configuration Manager do SSRS)](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
## <a name="the-report-server-cannot-open-a-connection-to-the-report-server-database-rsreportserverdatabaseunavailable"></a>O servidor de relatório não pode abrir uma conexão com o banco de dados do servidor de relatório. (rsReportServerDatabaseUnavailable).  
Mensagem completa: O servidor de relatório não pode abrir uma conexão com o banco de dados do servidor de relatório. Uma conexão com o banco de dados é necessária para todas as solicitações e processamentos. (rsReportServerDatabaseUnavailable)  
Esse erro ocorre quando o servidor de relatório não consegue se conectar ao banco de dados relacional do SQL Server que fornece o armazenamento interno ao servidor. A conexão com o banco de dados do servidor de relatório é gerenciada pela ferramenta Configuração do Reporting Services. Você pode executar a ferramenta, ir à página Configuração do Banco de Dados e corrigir as informações de conexão. É recomendável usar a ferramenta para atualizar as informações de conexão; a ferramenta assegura que as configurações dependentes sejam atualizadas e que os serviços sejam reiniciados. Para saber mais, confira [Configurar uma conexão de banco de dados do servidor de relatório](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md) e [Configurar uma conta de serviço do servidor de relatório](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
Esse erro também poderá ocorrer se a instância do Mecanismo de Banco de Dados que hospeda o banco de dados do servidor de relatório não estiver configurada para conexões remotas. A conexão remota é habilitada, por padrão, em algumas edições do SQL Server. Para verificar se ela está habilitada na instância do Mecanismo de Banco de Dados do SQL Server que você está usando, execute a ferramenta SQL Server Configuration Manager. Você deve habilitar TCP/IP e pipes nomeados. Um servidor de relatório usa os dois protocolos. Para obter instruções sobre como habilitar conexões remotas, confira a seção "Como configurar conexões remotas com o banco de dados do servidor de relatório" em [Configurar um servidor de relatório para administração remota](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md).  
  
Se o erro incluir o texto adicional a seguir, a senha expirou na conta usada para executar a instância do Mecanismo de Banco de Dados: "Erro ao estabelecer uma conexão com o servidor. Ao conectar-se ao SQL Server, essa falha pode ser provocada porque, sob as configurações padrão, o SQL Server não permite conexões remotas. (**provedor: Interfaces de Rede do SQL Server, erro: 26 — erro ao localizar servidor/instância especificada)**". Para resolver esse erro, redefina a senha.   
  
## <a name="rpc-server-is-not-listening"></a>“O servidor RPC não está escutando”  
O serviço Servidor de Relatório usa o servidor RPC (Chamada de Procedimento Remoto) para algumas operações. Se o erro “O servidor RPC não está escutando” for exibido, verifique se o serviço Servidor de Relatório está em execução.  
  
## <a name="unexpected-error-general-network-error"></a>Erro inesperado (erro de rede geral)  
Esse erro indica um erro de conexão de fonte de dados. Verifique a cadeia de conexão e verifique se você tem permissão para acessar a fonte de dados. Se estiver usando a Autenticação do Windows para acessar uma fonte de dados, você deve ter permissão para acessar o computador que hospeda a fonte de dados.  
  
## <a name="unable-to-grant-database-access-in-sharepoint-central-administration"></a>Não é possível conceder acesso a banco de dados na Administração Central do SharePoint  
Ao configurar o Reporting Services para integração a um produto SharePoint, ou uma tecnologia no Windows Vista ou Windows Server 2008, você poderá receber a mensagem de erro a seguir ao tentar conceder acesso na página **Conceder Acesso ao Banco de Dados** na Administração Central do SharePoint: "Não é possível estabelecer uma conexão com o computador".  
  
Isso acontece porque o UAC (Controle de Conta de Usuário) no Windows Vista e no Windows Server 2008 requer aceitação explícita de um administrador para elevar e usar o token de administrador na execução de tarefas que exigem permissões de administrador. No entanto, nesse caso, o serviço Administração do Windows SharePoint Services não pode ser elevado para conceder às contas de serviço do Reporting Services acesso aos bancos de dados de conteúdo e configuração do SharePoint.  
  
No SQL Server 2008 Reporting Services, apenas a conta de serviço do Servidor de Relatório requer acesso ao banco de dados; já no SQL Server 2005 Reporting Services SP2, as contas de serviço do Servidor de Relatório, Windows e Web, exigem acesso ao banco de dados. Para saber mais sobre a conta de serviço do Servidor de Relatório no SQL Server 2008, confira Conta de Serviço (Configuração do Reporting Services).  
  
Há duas soluções alternativas para esse problema.   
1.  Em uma delas, você pode desativar temporariamente o UAC e usar a Administração Central do SharePoint para conceder acesso.  
> [!IMPORTANT]  
> Tome cuidado ao desativar o UAC para usar a solução alternativa, e ative-o imediatamente depois de conceder acesso ao banco de dados na Administração Central do SharePoint. Se não desejar desativar o UAC, use a segunda solução alternativa apresentada nesta seção. Para obter mais informações sobre o UAC, consulte a documentação do produto Windows.  
2. Na segunda solução alternativa, você pode conceder manualmente acesso ao banco de dados às contas de serviço do Reporting Services. Use o procedimento a seguir para conceder acesso adicionando as contas de serviço do Reporting Services às funções de banco de dados e ao grupo do Windows corretos. Esse procedimento se aplica à conta de serviço do Servidor de Relatório no SQL Server 2008 Reporting Services; se você estiver executando o SQL Server 2005 Reporting Services, execute o procedimento para ambas as contas de serviço do Servidor de Relatório, Windows e Web.   
  
### <a name="to-manually-grant-database-access"></a>Para conceder manualmente acesso ao banco de dados  
  
1. Adicione a conta de serviço do Servidor de Relatório ao grupo WSSP_WPG do Windows no computador do Reporting Services.  
2. Conecte-se à instância do banco de dados que mantém a configuração e os bancos de dados de conteúdo do SharePoint, e crie um logon de banco de dados SQL para a conta de serviço do Servidor de Relatório.  
3. Adicione o logon de banco de dados SQL às seguintes funções de banco de dados:  
  
* db_owner role no banco de dados WSS Content  
* WSS_Content_Application_Pools role no banco de dados SharePoint_Config  
  
## <a name="unable-to-connect-to-the-reports-and-reportserver-directories-when-the-report-server-databases-are-created-on-a-virtual-sql-server-that-runs-in-a-microsoft-cluster-services-mscs-cluster"></a>Não é possível se conectar aos diretórios /reports e /reportserver quando os bancos de dados do servidor de relatório são criados em um SQL Server executando em um cluster MSCS (Serviços de Cluster da Microsoft)  
Quando você cria os bancos de dados do servidor de relatório, **ReportServer** e **ReportServerTempDB**, em um SQL Server virtual executado em um cluster MSCS, o nome remoto no formato `<domain>\<computer_name>$` não pode ser registrado como logon no SQL Server. Se tiver configurado a conta de serviço do Servidor de Relatório de modo a exigir esse nome remoto para as conexões, os usuários não poderão se conectar aos diretórios /reports e /reportserver no Reporting Services. Por exemplo, a conta NetworkService interna do Windows requer tal nome remoto. Para evitar esse problema, use uma conta de domínio explícita ou um logon do SQL Server para se conectar aos bancos de dados do servidor de relatório.  
    
  ## <a name="see-also"></a>Consulte Também  
[Suporte ao navegador para Reporting Services e Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)  
[Erros e eventos (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
[Solucionar problemas de recuperação de dados com relatórios do Reporting Services](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[Solucionar problemas de assinaturas e entrega do Reporting Services](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

