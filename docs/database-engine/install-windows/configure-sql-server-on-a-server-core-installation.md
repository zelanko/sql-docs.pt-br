---
title: Configurar o SQL Server em uma instalação do Server Core | Microsoft Docs
ms.custom: ''
ms.date: 09/05/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- IsHadrEnabled server property
- Server Core Installation [SQL Server]
ms.assetid: ed6e5e94-4b8d-422a-a17e-61b05a4df903
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: jroth
ms.openlocfilehash: 9aa75a4d0ca9b66c37cb57ee603d513c6912b751
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66794966"
---
# <a name="configure-sql-server-on-a-server-core-installation"></a>Configurar o SQL Server em uma instalação do Server Core

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo abrange detalhes sobre a configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma instalação do Server Core.  

##  <a name="BKMK_ConfigureWindows"></a> Configurar e gerenciar o Server Core no Windows Server  
A seção fornece referências a artigos que ajudam a configurar e gerenciar uma instalação do Server Core.  
  
Nem todos os recursos do [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] têm suporte no modo SQL Core.  Alguns desses componentes podem ser instalados em um computador cliente, ou em um servidor diferente que não esteja executando o Server Core, e podem ser conectados aos serviços de Mecanismo de Banco de Dados instalados no Server Core.  
  
Para obter mais informações sobre como configurar e gerenciar remotamente uma instalação do Server Core, consulte os seguintes artigos:  
  
- [Instalar o Server Core](https://technet.microsoft.com/windows-server-docs/get-started/getting-started-with-server-core)  
  
- [Configurar uma instalação do Server Core do Windows Server 2016 com Sconfig.cmd](https://docs.microsoft.com/windows-server/get-started/sconfig-on-ws2016)  
  
- [Instalar funções de servidor e recursos em um servidor Windows Server 2012 R2 do Server Core](https://technet.microsoft.com/library/jj574158(v=ws.11).aspx)
  
- [Gerenciando uma instalação Server Core: Visão geral](https://go.microsoft.com/fwlink/?LinkId=245962)  
  
- [Administrando uma instalação do Server Core](https://go.microsoft.com/fwlink/?LinkId=245963)
  
##  <a name="BKMK_InstallSQLUpdates"></a> Instalar atualizações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
Esta seção fornece informações sobre como instalar atualizações do [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] em um computador com o Windows Server Core. Nós recomendamos que os clientes avaliem e instalem as atualizações mais recentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o mais rápido possível para ter certeza de que os sistemas estejam atualizados com as atualizações de segurança mais recentes. Para obter mais informações sobre como instalar o [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] em um computador Windows Server Core, consulte [Instalar o SQL Server no Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md).  
  
Estes são os dois cenários para instalar atualizações de produto:  
  
- [Instalando atualizações para o SQL Server durante uma nova instalação](../../database-engine/install-windows/configure-sql-server-on-a-server-core-installation.md#bkmk_NewInstall)  
  
- [Instalando atualizações para o SQL Server após a instalação](../../database-engine/install-windows/configure-sql-server-on-a-server-core-installation.md#bkmk_alreadyInstall)  
  
###  <a name="bkmk_NewInstall"></a> Instalando atualizações para o [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] durante uma nova instalação  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte apenas a instalações de prompt de comando no sistema operacional Server Core. Para obter mais informações, consulte [Instalar o SQL Server por meio do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integra as últimas atualizações de produto com a instalação principal de produto, de forma que o produto principal e suas atualizações aplicáveis sejam instalados ao mesmo tempo.  
  
Depois que a Instalação localizar as versões mais recentes das atualizações aplicáveis, ela baixará e integrará essas atualizações com o processo de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atual. A Atualização de Produto pode efetuar pull de uma atualização cumulativa, service pack ou service pack mais atualização cumulativa.  
  
Especifique os parâmetros UpdateEnabled e UpdateSource para incluir as últimas atualizações de produto com a instalação principal do produto. Consulte o seguinte exemplo para habilitar atualizações de produto durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /UpdateEnabled=True /UpdateSource="<SourcePath>" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
###  <a name="bkmk_alreadyInstall"></a> Instalando atualizações para o [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] depois que tiver sido instalado.  
Em uma instância instalada do [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)], nós recomendamos que você aplique as atualizações de segurança mais recentes e críticas inclusive Versões de Distribuição Geral (GDRs) e Service Packs (SPs). As atualizações individuais cumulativas e as atualizações de segurança devem ser adotadas caso a caso, "conforme o necessário". Avalie a atualização; se ela for necessária, aplique-a.  
  
Aplique uma atualização em um prompt de comando substituindo <nome_do_pacote> pelo nome do seu pacote de atualização:  
  
- Atualize uma única instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e todos os componentes compartilhados. Você pode especificar a instância usando o parâmetro InstanceName ou o parâmetro InstanceID.  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceName=MyInstance  
    ```  
  
- Atualize apenas componentes compartilhados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch  
    ```  
  
- Atualize todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador e todos os componentes compartilhados:  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /AllInstances  
    ```  
  
## <a name="BKMK_StartStopServices"></a> Iniciar/parar o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
O aplicativo [sqlservr](../../tools/sqlservr-application.md) inicia, encerra, pausa e continua uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio de um prompt de comando.  
  
Você também pode usar serviços Net para iniciar e interromper serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="BKMK_EnableAlwaysON"></a> Habilitar Grupos de Disponibilidade AlwaysOn  
Habilitar os Grupos de Disponibilidade AlwaysOn é pré-requisito para uma instância do servidor usar grupos de disponibilidade como uma solução de recuperação de desastres de alta disponibilidade. Para obter mais informações sobre como gerenciar os Grupos de Disponibilidade AlwaysOn, consulte [Habilitar e desabilitar Grupos de Disponibilidade AlwaysOn (SQL Server)](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).  
  
### <a name="using-includessnoversionincludesssnoversion-mdmd-configuration-manager-remotely"></a>Usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager remotamente  
Estas etapas devem ser realizadas em um computador que executa a edição de cliente do Windows ou o Windows Server que tem o Shell Gráfico de Servidor instalado.  
  
1. Abra **Gerenciamento de Computador**. Para abrir o **Gerenciamento de Computador**, clique em **Iniciar**, digite `compmgmt.msc` e, em seguida, clique em **OK**.    
  
2. Na árvore de console, clique com o botão direito do mouse em **Gerenciamento de Computador** e, depois, clique em **Conectar a outro computador...** .  
  
3. Na caixa de diálogo **Selecionar Computador**, digite o nome do computador Server Core a ser gerenciado ou clique em **Procurar** para localizá-lo e, depois, clique em **OK**.  
  
4. Na árvore de console, em **Gerenciamento de Computador** do computador Server Core, clique em **Serviços e Aplicativos**.  
  
5. Clique duas vezes em **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager**.  
  
6. No **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager**, clique em **Serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** , clique com o botão direito do mouse em **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** (\<instance name>), em que \<instance name> é o nome de uma instância de servidor local na qual você deseja habilitar os Grupos de Disponibilidade AlwaysOn e clique em Propriedades.  
  
7. Selecione a guia **Alta Disponibilidade AlwaysOn** .  
  
8. Verifique se o campo Nome do cluster de failover do Windows contém o nome do nó de cluster de failover local. Se esse campo estiver em branco, significa que essa instância de servidor no momento não dá suporte a Grupos de Disponibilidade AlwaysOn. Talvez o computador local não seja um nó de cluster, o cluster WSFC tenha sido desligado ou essa edição do [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] não seja compatível com os Grupos de Disponibilidade AlwaysOn.  
  
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
  
```  
Enable-SqlAlwaysOn -Path SQLSERVER:\SQL\Machine\Instance  
```  
  
##  <a name="BKMK_ConfigureRemoteAccess"></a> Configurando o acesso remoto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução no Server Core  
 Execute as ações descritas abaixo para configurar o acesso remoto de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] em execução no Windows Server Core.  
  
### <a name="enable-remote-connections-on-the-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Habilitar conexões remotas na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Para habilitar conexões remotas, use o SQLCMD.exe localmente e execute as instruções a seguir na instância do Server Core:  
  
-   `EXEC sys.sp_configure N'remote access', N'1'`  
  
     `GO`  
  
-   `RECONFIGURE WITH OVERRIDE`  
  
     `GO`  
  
### <a name="enable-and-start-the-includessnoversionincludesssnoversion-mdmd-browser-service"></a>Habilitar e iniciar o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser  
 Por padrão, o serviço Navegador está desabilitado.  Se ele estiver desabilitado em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução no Server Core, execute o seguinte comando no prompt de comando para habilitá-lo:  
  
 `sc config SQLBROWSER start= auto`  
  
 Depois de habilitá-lo, execute o seguinte comando a partir do prompt de comando para iniciar o serviço:  
  
 `net start SQLBROWSER`  
  
### <a name="create-exceptions-in-windows-firewall"></a>Criar exceções no Firewall do Windows  
 Para criar exceções para o acesso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Firewall do Windows, siga as etapas especificadas em [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
### <a name="enable-tcpip-on-the-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Habilitar TCP/IP na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 O protocolo TCP/IP pode ser habilitado por meio do Windows PowerShell para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Server Core. Siga estas etapas:  
  
1.  No computador que executa o Windows Server Core, inicie o **Gerenciador de Tarefas**.  
  
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
  
##  <a name="BKMK_Profiler"></a> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler  
 Em um computador remoto, inicie o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] e selecione Novo Rastreamento no menu Arquivo. O aplicativo exibe uma caixa de diálogo Conectar ao Servidor, onde é possível especificar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que reside no computador Server Core, ao qual você deseja se conectar. Para obter mais informações, consulte [Start SQL Server Profiler](../../tools/sql-server-profiler/start-sql-server-profiler.md).  
  
 Para obter mais informações sobre as permissões necessárias para executar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], veja [Permissões necessárias para executar o SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md).  
  
 Para obter mais detalhes sobre o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], veja [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md).  
  
##  <a name="BKMK_Auditing"></a> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Auditoria  
 É possível usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)] remotamente para definir uma auditoria. Após a criação e habilitação da auditoria, o destino receberá entradas. Para obter mais informações sobre como criar e gerenciar auditorias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
##  <a name="BKMK_CMD"></a> Utilitários do prompt de comando  
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
|[Utilitário sqlmaint](../../tools/sqlmaint-utility.md)|Usado para executar planos de manutenção de banco de dados criados em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|\<drive>:\Arquivos de Programas\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL14.MSSQLSERVER\MSSQL\Binn|  
|[Utilitário sqlps](../../tools/sqlps-utility.md)|Usado para executar comandos e scripts PowerShell. Carrega e registra o provedor e os cmdlets do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlservr](../../tools/sqlservr-application.md)|Usado para iniciar e parar uma instância de [!INCLUDE[ssDE](../../includes/ssde-md.md)] no prompt de comando para solução de problemas.|\<drive>:\Arquivos de Programas\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL14.MSSQLSERVER\MSSQL\Binn|  
  
##  <a name="BKMK_troubleshoot"></a> Usar ferramentas de solução de problemas  
 É possível usar o [Utilitário SQLdiag](../../tools/sqldiag-utility.md) para coletar logs e arquivos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e de outros tipos de servidores, e usá-lo para monitorar os servidores ao longo do tempo ou para solucionar problemas específicos com seus servidores. O SQLdiag foi criado para agilizar e simplificar a coleta de informações de diagnóstico para os Serviços de Suporte Técnico da Microsoft.  
  
 Inicie o utilitário no prompt de comando do administrador no Server Core, usando a sintaxe especificada no artigo: [Utilitário SQLdiag](../../tools/sqldiag-utility.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar o SQL Server no Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md)   
 [Artigos de instruções sobre a instalação](https://msdn.microsoft.com/library/59de41e7-557f-462a-8914-53ec35496baa)  
  
  
