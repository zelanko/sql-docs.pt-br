---
title: Configurar o SQL Server em uma instalação do Server Core | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- IsHadrEnabled server property
- Server Core Installation [SQL Server]
ms.assetid: ed6e5e94-4b8d-422a-a17e-61b05a4df903
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0c2a82aac84777c0601d234162135f9404184c39
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72797912"
---
# <a name="configure-sql-server-on-a-server-core-installation"></a>Configurar o SQL Server em uma instalação do Server Core
  Este tópico abrange detalhes sobre a configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma instalação do Server Core do [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1. 
  
##  <a name="configure-and-manage-server-core-on-windows-server"></a>Configurar e gerenciar o Server Core no Windows Server  
 A seção fornece referências a tópicos que ajudam a configurar e gerenciar uma instalação do Server Core.  
  
 Nem todos os recursos do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] têm suporte no modo SQL Core.  Alguns desses componentes podem ser instalados em um computador cliente, ou em um servidor diferente que não esteja executando o Server Core, e podem ser conectados aos serviços de Mecanismo de Banco de Dados instalados no Server Core.  
  
 Para obter mais informações sobre como configurar e gerenciar remotamente uma instalação do Server Core, consulte os seguintes tópicos:  
  
-   [Windows Server 2008 R2: práticas recomendadas para implantações do Server Core](https://go.microsoft.com/fwlink/?LinkID=245957) (https://go.microsoft.com/fwlink/?LinkID=245957)  
  
-   [Configurando uma instalação do Server Core: visão geral](https://go.microsoft.com/fwlink/?LinkId=245958) (https://go.microsoft.com/fwlink/?LinkId=245958)  
  
-   [Configurando uma instalação do Server Core do Windows server 2008 R2 com sconfig. cmd](https://go.microsoft.com/fwlink/?LinkId=245959) (https://go.microsoft.com/fwlink/?LinkId=245959)  
  
-   [Instalando uma função de servidor em um servidor que executa uma instalação Server Core do Windows server 2008 R2: visão geral](https://go.microsoft.com/fwlink/?LinkId=245960) (https://go.microsoft.com/fwlink/?LinkId=245960)  
  
-   [Instalando recursos do Windows em um servidor que executa uma instalação do Server Core do Windows server 2008 R2: visão geral](https://go.microsoft.com/fwlink/?LinkId=245961) (https://go.microsoft.com/fwlink/?LinkId=245961)  
  
-   [Gerenciando uma instalação do Server Core: visão geral](https://go.microsoft.com/fwlink/?LinkId=245962) (https://go.microsoft.com/fwlink/?LinkId=245962)  
  
-   [Administrando uma instalação do Server Core](https://go.microsoft.com/fwlink/?LinkId=245963) (https://go.microsoft.com/fwlink/?LinkId=245963)  
  
##  <a name="install-updates"></a>Instalar as atualizações  
 Esta seção fornece informações sobre como instalar atualizações do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em um computador com o Windows Server Core. Nós recomendamos que os clientes avaliem e instalem as atualizações mais recentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o mais rápido possível para ter certeza de que os sistemas estejam atualizados com as atualizações de segurança mais recentes. Para obter mais informações sobre [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] como instalar o em um computador Windows Server Core, consulte [instalar SQL Server 2014 no Server Core](install-sql-server-on-server-core.md).  
  
 Estes são os dois cenários para instalar atualizações de produto:  
  
-   [Instalando atualizações para o SQL Server 2014 durante uma nova instalação](#installing-updates-during-a-new-installation) 
  
-   [Instalando atualizações para o SQL Server 2014 após a instalação](#installing-updates-after-installation) 
  
### <a name="installing-updates-during-a-new-installation"></a>Instalando atualizações durante uma nova instalação  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte apenas a instalações de prompt de comando no sistema operacional Server Core. Para obter mais informações, consulte [Install SQL Server 2014 from the Command Prompt](install-sql-server-from-the-command-prompt.md) (Instalar o SQL Server 2014 do Prompt de Comando).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integra as últimas atualizações de produto com a instalação principal de produto, de forma que o produto principal e suas atualizações aplicáveis sejam instalados ao mesmo tempo.  
  
 Depois que a Instalação localizar as versões mais recentes das atualizações aplicáveis, ela baixará e integrará essas atualizações com o processo de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atual. A Atualização de Produto pode efetuar pull de uma atualização cumulativa, service pack ou service pack mais atualização cumulativa.  
  
 Especifique os parâmetros UpdateEnabled e UpdateSource para incluir as últimas atualizações de produto com a instalação principal do produto. Consulte o seguinte exemplo para habilitar atualizações de produto durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
```cmd 
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,Replication /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /UpdateEnabled=True /UpdateSource="<SourcePath>" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
### <a name="installing-updates-after-installation"></a>Instalando atualizações após a instalação 
 Em uma instância instalada do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], nós recomendamos que você aplique as atualizações de segurança mais recentes e críticas inclusive Versões de Distribuição Geral (GDRs) e Service Packs (SPs). As atualizações individuais cumulativas e as atualizações de segurança devem ser adotadas caso a caso, "conforme o necessário". Avalie a atualização; se ela for necessária, aplique-a.  
  
 Aplique uma atualização em um prompt de comando substituindo <nome_do_pacote> pelo nome do seu pacote de atualização:  
  
-   Atualize uma única instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e todos os componentes compartilhados. Você pode especificar a instância usando o parâmetro InstanceName ou o parâmetro InstanceID.  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceName=MyInstance  
    ```  
  
-   Atualize apenas componentes compartilhados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch  
    ```  
  
-   Atualize todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador e todos os componentes compartilhados:  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /AllInstances  
    ```  
  
##  <a name="startstop-sql-server-service"></a>Iniciar/parar serviço de SQL Server  
 O aplicativo [sqlservr](../../tools/sqlservr-application.md) inicia, encerra, pausa e continua uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio de um prompt de comando.  
  
 Você também pode usar serviços Net para iniciar e interromper serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="enable-alwayson-availability-groups"></a>Habilitar Grupos de Disponibilidade AlwaysOn  
 Habilitar os Grupos de Disponibilidade AlwaysOn é pré-requisito para uma instância do servidor usar grupos de disponibilidade como uma solução de recuperação de desastres de alta disponibilidade. Para obter mais informações sobre como gerenciar os grupos de disponibilidade do AlwaysOn, veja [Habilitar e desabilitar grupos de disponibilidade do AlwaysOn &#40;SQL Server&#41;](../availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).  
  
### <a name="using-sql-server-configuration-manager-remotely"></a>Usando SQL Server Configuration Manager remotamente  
 Estas etapas devem ser realizadas em um computador que esteja executando a edição de cliente do [!INCLUDE[win7](../../includes/win7-md.md)] ou posterior ou em outro servidor com o Shell Gráfico de Servidor instalado (isto é, uma instalação completa do [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] ou uma instalação do Windows Server 8 com o recurso Shell Gráfico de Servidor habilitado).  
  
1.  Abra o gerenciamento de computador. Para abrir o Gerenciamento do Computador, siga um destes procedimentos:  
  
    1.  No [!INCLUDE[win7](../../includes/win7-md.md)], Windows Server 2008 ou [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]:  
  
        1.  Clique em Iniciar, em Todos os Programas, em Ferramentas Administrativas e em Gerenciamento do Computador.  
  
        2.  Clique em Iniciar, em Executar, digite COMPMGMT.MSC e clique em OK.  
  
    2.  No Windows 8 com o Shell Gráfico de Servidor habilitado:  
  
        1.  Mova o mouse até o canto inferior esquerdo da tela e clique com o botão direito do mouse quando visualizar a sobreposição Iniciar.  
  
        2.  Selecione Gerenciamento do Computador no menu de contexto.  
  
2.  Na árvore de console, clique com o botão direito do mouse em Gerenciamento do Computador e, depois, clique em Conectar a outro computador.  
  
3.  Na caixa de diálogo Selecionar Computador, digite o nome do computador Server Core a ser gerenciado, ou clique em Procurar para localizá-lo e, depois, clique em OK.  
  
4.  Na árvore de console, em Gerenciamento do Computador do computador Server Core, clique em Serviços e Aplicativos.  
  
5.  Clique duas vezes no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
6.  Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, clique [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em serviços, clique com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o\<botão direito do mouse em ( \<nome da instância>), em que nome da instância> é o nome de uma instância de servidor local para a qual você deseja habilitar grupos de disponibilidade AlwaysOn e clique em Propriedades.  
  
7.  Selecione a guia Alta Disponibilidade AlwaysOn.  
  
8.  Verifique se o campo Nome do cluster de failover do Windows contém o nome do nó de cluster de failover local. Se esse campo estiver em branco, significa que essa instância de servidor no momento não dá suporte a Grupos de Disponibilidade AlwaysOn. Talvez o computador local não seja um nó de cluster, o cluster WSFC tenha sido desligado ou essa edição do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] não dê suporte a Grupos de Disponibilidade AlwaysOn.  
  
9. Marque a caixa de seleção Habilitar Grupos de Disponibilidade AlwaysOn e clique em OK.  
  
10. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager salva suas alterações. Em seguida, você deve reiniciar manualmente o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Isso permite escolher a hora de reinicialização mais adequada de acordo com as necessidades da sua empresa. Quando o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for reiniciado, AlwaysOn será habilitado e a propriedade de servidor IsHadrEnabled será definida como 1.  
  
> [!NOTE]
>  -   Você deve ter direitos de usuário apropriados ou deve ter a devida autoridade delegada no computador de destino para se conectar a esse computador.  
> -   O nome do computador gerenciado aparece entre parênteses ao lado de Gerenciamento do Computador na árvore de console.  
  
### <a name="using-powershell-cmdlets-to-enable-alwayson-availability-groups"></a>Usando cmdlets do PowerShell para habilitar Grupos de Disponibilidade AlwaysOn

 O cmdlet do PowerShell, Enable-SqlAlwaysOn, é usado para habilitar o Grupo de Disponibilidade AlwaysOn em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se Grupos de Disponibilidade AlwaysOn estiver habilitado enquanto o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver sendo executado, o serviço do Mecanismo de Banco de Dados deverá ser reiniciado para que as alterações sejam concluídas. A menos que você especifique o parâmetro -Force, o cmdlet solicitará que você responda se deseja reiniciar o serviço; se for cancelado, nenhuma operação ocorrerá.  
  
 Você deve ter permissões de administrador para executar este cmdlet.  
  
 Você pode usar uma das seguintes sintaxes para habilitar Grupos de Disponibilidade AlwaysOn para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
Enable-SqlAlwaysOn [-Path <string>] [-Credential <PSCredential>] [-Force] [-NoServiceRestart] [-Confirm] [-WhatIf] [<Commom Parameters>]  
```  
  
```  
Enable-SqlAlwaysOn -InputObject <Server> [-Credential <PSCredential>] [-Force] [-NoServiceRestart] [-Confirm] [-WhatIf] [<Commom Parameters>]  
```  
  
```  
Enable-SqlAlwaysOn [-ServerInstance <string>] [-Credential <PSCredential>] [-Force] [-NoServiceRestart] [-Confirm] [-WhatIf] [<Commom Parameters>]  
```  
  
 O seguinte comando PowerShell habilita Grupos de Disponibilidade AlwaysOn em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Computador/Instância):  
  
```powershell
Enable-SqlAlwaysOn -Path SQLSERVER:\SQL\Machine\Instance  
```  
  
## <a name="configuring-remote-access-of-sql-server-running-on-server-core"></a>Configurando o acesso remoto de SQL Server em execução no Server Core  
 Execute as ações descritas abaixo para configurar o acesso remoto de uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em execução no [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1.  
  
### <a name="enable-remote-connections-on-an-instance-of-sql-server"></a>Habilitar conexões remotas em uma instância do SQL Server 
 Para habilitar conexões remotas, use o SQLCMD.exe localmente e execute as instruções a seguir na instância do Server Core:  
  
-   `EXEC sys.sp_configure N'remote access', N'1'`  
  
     `GO`  
  
-   `RECONFIGURE WITH OVERRIDE`  
  
     `GO`  
  
### <a name="enable-and-start-the-sql-server-browser-service"></a>Habilitar e iniciar o serviço SQL Server Browser  
 Por padrão, o serviço Navegador está desabilitado.  Se ele estiver desabilitado em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução no Server Core, execute o seguinte comando no prompt de comando para habilitá-lo:  
  
 `sc config SQLBROWSER start= auto`  
  
 Depois de habilitá-lo, execute o seguinte comando a partir do prompt de comando para iniciar o serviço:  
  
 `net start SQLBROWSER`  
  
### <a name="create-exceptions-in-windows-firewall"></a>Criar exceções no Firewall do Windows  
 Para criar exceções para o acesso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Firewall do Windows, siga as etapas especificadas em [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
### <a name="enable-tcpip-on-an-instance-of-sql-server"></a>Habilitar TCP/IP em uma instância do SQL Server
 O protocolo TCP/IP pode ser habilitado por meio do Windows PowerShell para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Server Core. Siga estas etapas:  
  
1.  No computador executando o Windows Server 2008 R2 Server Core SP1, inicie o Gerenciador de Tarefas.  
  
2.  Na guia **Aplicativos** , clique em **Nova Tarefa**.  
  
3.  Na caixa de diálogo **Criar Nova Tarefa** , digite **sqlps.exe** no campo **Abrir** e clique em **OK**. Isso abrirá a janela **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell**.  
  
4.  Na janela **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell**, execute o script a seguir para habilitar o protocolo TCP/IP:  
  
```powershell
$smo = 'Microsoft.SqlServer.Management.Smo.'  
$wmi = new-object ($smo + 'Wmi.ManagedComputer')  
# Enable the TCP protocol on the default instance.  If the instance is named, replace MSSQLSERVER with the instance name in the following line.  
$uri = "ManagedComputer[@Name='" + (get-item env:\computername).Value + "']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
$Tcp = $wmi.GetSmoObject($uri)  
$Tcp.IsEnabled = $true  
$Tcp.Alter()  
$Tcp  
```  
  
##  <a name="sql-server-profiler"></a>SQL Server Profiler  
 Em um computador remoto, inicie o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] e selecione Novo Rastreamento no menu Arquivo. O aplicativo exibe uma caixa de diálogo Conectar ao Servidor, onde é possível especificar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que reside no computador Server Core, ao qual você deseja se conectar. Para obter mais informações, consulte [Start SQL Server Profiler](../../tools/sql-server-profiler/start-sql-server-profiler.md).  
  
 Para obter mais informações sobre as permissões necessárias para executar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], veja [Permissões necessárias para executar o SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md).  
  
 Para obter mais detalhes sobre o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], veja [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md).  
  
##  <a name="sql-server-auditing"></a>Auditoria do SQL Server  
 É possível usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)] remotamente para definir uma auditoria. Após a criação e habilitação da auditoria, o destino receberá entradas. Para obter mais informações sobre como criar e gerenciar auditorias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
##  <a name="sql-servevr-command-prompt-utilities"></a>Utilitários de prompt de comando do SQL Servevr  
 Você pode usar os utilitários de prompt de comando a seguir, que o habilitam a gerar scripts de operações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um computador Server Core. A seguinte tabela contém uma lista de utilitários de prompt de comando que são enviados com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para Server Core:  
  
|**Utilitário**|**Descrição**|**Instalado no**|  
|-----------------|---------------------|----------------------|  
|[Utilitário bcp](../../tools/bcp-utility.md)|Usado para copiar dados entre uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e um arquivo de dados em formato especificado pelo usuário.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilitário dtexec](../../integration-services/packages/dtexec-utility.md)|Usado para configurar e executar um pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[Utilitário dtutil](../../integration-services/dtutil-utility.md)|Usado para gerenciar pacotes SSIS.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[Utilitário osql](../../tools/osql-utility.md)|Permite a inserção de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] , procedimentos do sistema e arquivos de script no prompt de comando.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Aplicativo sqlagent90](../../tools/sqlagent90-application.md)|Usado para iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a partir de um prompt de comando.|\<drive>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<*instance_name*>\MSSQL\Binn|  
|[Utilitário sqlcmd](../../tools/sqlcmd-utility.md)|Permite a inserção de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] , procedimentos do sistema e arquivos de script no prompt de comando.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilitário SQLdiag](../../tools/sqldiag-utility.md)|Usado para coletar informações de diagnóstico para o Suporte e Atendimento ao Cliente [!INCLUDE[msCoName](../../includes/msconame-md.md)] .|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilitário sqlmaint](../../tools/sqlmaint-utility.md)|Usado para executar planos de manutenção de banco de dados criados em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|\<unidade>: \Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12. MSSQLSERVER\MSSQL\Binn|  
|[Utilitário sqlps](../../tools/sqlps-utility.md)|Usado para executar comandos e scripts PowerShell. Carrega e registra o provedor e os cmdlets do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Aplicativo sqlservr](../../tools/sqlservr-application.md)|Usado para iniciar e parar uma instância de [!INCLUDE[ssDE](../../includes/ssde-md.md)] no prompt de comando para solução de problemas.|\<unidade>: \Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12. MSSQLSERVER\MSSQL\Binn|  
  
##  <a name="use-troubleshooting-tools"></a>Usar ferramentas de solução de problemas  
 É possível usar o [Utilitário SQLdiag](../../tools/sqldiag-utility.md) para coletar logs e arquivos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e de outros tipos de servidores, e usá-lo para monitorar os servidores ao longo do tempo ou para solucionar problemas específicos com seus servidores. O SQLdiag foi criado para agilizar e simplificar a coleta de informações de diagnóstico para os Serviços de Suporte Técnico da Microsoft.  
  
 Você pode iniciar o utilitário no prompt de comando do administrador no Server Core, usando a sintaxe especificada no tópico: [SQLdiag Utility](../../tools/sqldiag-utility.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar o SQL Server 2014 no Server Core](install-sql-server-on-server-core.md)   
 [Tópicos de instruções sobre a instalação](../../sql-server/install/installation-how-to-topics.md)  
