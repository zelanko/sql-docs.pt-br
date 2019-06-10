---
title: Instalar o SQL Server 2016 no Server Core | Microsoft Docs
ms.custom: ''
ms.date: 09/05/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 1dd294cc-5b69-4d0c-9005-3e307b75678b
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: jroth
ms.openlocfilehash: 3eb1ff10fbf0af49cd698537af915378cc1ddb87
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794925"
---
# <a name="install-sql-server-on-server-core"></a>Instalar o SQL Server no Server Core

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Instale o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma instalação do Server Core.   
  
A opção de instalação do Server Core oferece um ambiente mínimo para a execução de funções de servidor específicas. Isso ajuda a reduzir os requisitos de manutenção e gerenciamento e a superfície de ataque para essas funções de servidor. Para obter mais informações sobre o Server Core, consulte [Instalar o Server Core](https://docs.microsoft.com/windows-server/get-started/getting-started-with-server-core). Para obter mais informações sobre o Server Core implementado no [!INCLUDE[win8srv](../../includes/win8srv-md.md)], consulte [Server Core para Windows Server 2012](https://msdn.microsoft.com/library/hh846323\(VS.85\).aspx) (https://msdn.microsoft.com/library/hh846323(VS.85).aspx)).  
  
 Para obter informações sobre os sistemas operacionais com suporte no momento, consulte [Requisitos de hardware e software para a instalação do SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).

## <a name="prerequisites"></a>Prerequisites  
  
|Requisito|Como instalar o|  
|-----------------|--------------------|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6.1 |Para todas as edições do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] exceto [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], a Instalação exige o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6.1 Server Core Profile. A Instalação do SQL Server instalará isso automaticamente caso ainda não esteja instalado. A Instalação exige uma reinicialização. Instale o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] antes de executar a instalação para evitar uma reinicialização.|  
|Windows Installer 4.5|Fornecido com a instalação do Server Core.|  
|Windows PowerShell|Fornecido com a instalação do Server Core.|  
|Tempo de execução Java |Para usar o PolyBase, você precisa instalar o Tempo de Execução Java apropriado. Para obter mais informações, consulte [Instalação do PolyBase](../../relational-databases/polybase/polybase-installation.md).|
  
##  <a name="BK_SupportedFeatures"></a> Recursos com suporte  
 Use a tabela a seguir para descobrir quais recursos têm suporte no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em uma instalação do Server Core.  
  
|Recurso|Tem suporte|Informações adicionais|  
|-------------|---------------|----------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] Serviços|Sim||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replicação|Sim||  
|Pesquisa de Texto Completo|Sim||  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|Sim||  
|[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]|Sim||  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Não||  
|SSDT ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Tools)|Não||  
|Conectividade das ferramentas de cliente|Sim||  
|Servidor do Integration Services|Sim||  
|Compatibilidade das ferramentas de cliente com versões anteriores|Não||  
|SDK de Ferramentas de cliente|Não||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online|Não||  
|Ferramentas de Gerenciamento - Básicas|Apenas remoto|Não há suporte para a instalação desses recursos no Server Core. Esses componentes podem ser instalados em um servidor diferente que não seja o Server Core e conectados aos serviços do [!INCLUDE[ssDE](../../includes/ssde-md.md)] instalados no Server Core.|  
|Ferramentas de Gerenciamento – Completas|Apenas remoto|Não há suporte para a instalação desses recursos no Server Core. Esses componentes podem ser instalados em um servidor diferente que não seja o Server Core e conectados aos serviços do [!INCLUDE[ssDE](../../includes/ssde-md.md)] instalados no Server Core.|  
|Distributed Replay Controller|Não||  
|Distributed Replay Client|Apenas remoto|Não há suporte para a instalação desses recursos no Server Core. Esses componentes podem ser instalados em um servidor diferente que não seja o Server Core e conectados aos serviços do [!INCLUDE[ssDE](../../includes/ssde-md.md)] instalados no Server Core.|  
|SDK de Conectividade de Cliente do SQL|Sim||  
|Microsoft Sync Framework|Sim|O Microsoft Sync Framework não está incluído no pacote de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Baixe a versão apropriada do Sync Framework nesta página do [Centro de Download da Microsoft](https://go.microsoft.com/fwlink/?LinkId=221788) (https://go.microsoft.com/fwlink/?LinkId=221788)) e instale-a em um computador que executa o Server Core.|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|Não||  
|[!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]|Não||  
  
## <a name="supported-scenarios"></a>Cenários com suporte  
 A tabela a seguir mostra a matriz de cenários com suporte para a instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em um Server Core.  
  
|||  
|-|-|  
|Edições do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Todas as edições de 64 bits do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] |  
|Idioma do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Todos os idiomas|  
|Idioma do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na combinação de idioma/localidade do sistema operacional|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em japonês<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em alemão<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em chinês<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em árabe<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em tailandês<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em turco<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em português (Portugal)<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em inglês|  
|Windows Edition|[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation|  
  
## <a name="upgrade"></a>Atualizar 
 Em instalações do Server Core, atualizar de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tem suporte.  
  
## <a name="install"></a>Instalar  
 O[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] não tem suporte para a instalação por meio do assistente de instalação no sistema operacional Server Core. Quando você faz a instalação no Server Core, a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte ao modo silencioso completo usando o parâmetro /Q ou o modo Silencioso Simples usando o parâmetro /QS. Para obter mais informações, consulte [Instalar o SQL Server 2016 do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
 Independentemente do método de instalação, é necessário confirmar a aceitação dos termos da licença de software como indivíduo ou em nome de uma entidade, a menos que o uso do software seja governado por um contrato separado, como um contrato de licenciamento por volume da [!INCLUDE[msCoName](../../includes/msconame-md.md)] ou um contrato de terceiros com um ISV ou OEM.  
  
 Os termos da licença são exibidos para exame e aceitação na interface do usuário da Instalação. As instalações autônomas (usando o parâmetro /Q ou /QS) devem incluir o parâmetro /IACCEPTSQLSERVERLICENSETERMS. Você pode analisar as condições de licença separadamente em [Microsoft Software License Terms](https://go.microsoft.com/fwlink/?LinkId=148209)(em inglês).  
  
> [!NOTE]  
>  Dependendo de como você recebeu o software (por exemplo, por meio de licenciamento por volume da [!INCLUDE[msCoName](../../includes/msconame-md.md)] ), o uso do software pode estar sujeito a termos e condições adicionais.  
  
 Para instalar recursos específicos, use o parâmetro /FEATURES e especifique o recurso pai ou os valores de recursos. Para obter mais informações sobre os parâmetros de recursos e seu uso, consulte as seções a seguir.  
  
### <a name="feature-parameters"></a>Parâmetros de recursos  
  
|Parâmetro de recurso|Descrição|  
|-----------------------|-----------------|  
|SQLENGINE|Instala apenas o [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|Replicação|Instala o componente Replicação juntamente com o [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|FULLTEXT|Instala o componente FullText com o [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|AS|Instala todos os componentes do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|IS|Instala todos os componentes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|CONN|Instala os componentes de conectividade.| 
|ADVANCEDANALYTICS |Instala os serviços de R, e exige o mecanismo de banco de dados. Instalações autônomas exigem o parâmetro /IACCEPTROPENLICENSETERMS.  |


 Veja os exemplos a seguir do uso de parâmetros de recurso:  
  
|Parâmetro e valores|Descrição|  
|--------------------------|-----------------|  
|/FEATURES=SQLEngine|Instala apenas o [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|/FEATURES=SQLEngine,FullText|Instala o [!INCLUDE[ssDE](../../includes/ssde-md.md)] e o texto completo.|  
|/FEATURES=SQLEngine,Conn|Instala o [!INCLUDE[ssDE](../../includes/ssde-md.md)] e os componentes de conectividade.|  
|/FEATURES=SQLEngine,AS,IS,Conn|Instala o [!INCLUDE[ssDE](../../includes/ssde-md.md)], o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]e os componentes de conectividade.|  
|/FEATURES=SQLENGINE,ADVANCEDANALYTICS /IACCEPTROPENLICENSETERMS |Instala o  [!INCLUDE[ssDE](../../includes/ssde-md.md)] e o [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)].|  

  
### <a name="installation-options"></a>Opções de instalação  
 A Instalação dá suporte às opções de instalação a seguir enquanto instala o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em um sistema operacional do Server Core:  
  
1.  **Instalação da linha de comando**  
  
     Para instalar recursos específicos usando a opção de instalação do prompt de comando, use o parâmetro /FEATURES e especifique o recurso pai ou os valores de recursos listados. Um exemplo de como usar os parâmetros a partir da linha de comando é apresentado a seguir:  
  
    ```  
    Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,Replication /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /TCPENABLED=1 /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
2.  **Instalação usando o arquivo de configuração**  
  
     A Instalação dá suporte ao uso do arquivo de configuração apenas através do prompt de comando. O arquivo de configuração é um arquivo de texto com a estrutura básica de um parâmetro (par de nome/valor) e um comentário descritivo. O arquivo de configuração especificado no prompt de comando deve ter uma extensão de nome de arquivo .INI. Veja a seguir exemplos de ConfigurationFile.INI:  
  
    - Instalação do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. 
    
    O seguinte exemplo mostra como instalar uma nova instância autônoma que inclui o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]:  
  
        ```  
        ; SQL Server Configuration File  
        [OPTIONS]  
  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=SQLENGINE  
  
        ; Specify a default or named instance. MSSQLSERVER is the default instance for non-Express editions and SQLExpress for Express editions. This parameter is required when installing the ssNoVersion Database Engine, and Analysis Services (AS).  
  
        INSTANCENAME="MSSQLSERVER"  
  
        ; Specify the Instance ID for the ssNoVersion features you have specified. ssNoVersion directory structure, registry structure, and service names will incorporate the instance ID of the ssNoVersion instance.   
  
        INSTANCEID="MSSQLSERVER"  
  
        ; Account for ssNoVersion service: Domain\User or system account.   
  
        SQLSVCACCOUNT="NT Service\MSSQLSERVER"  
  
        ; Windows account(s) to provision as ssNoVersion system administrators.   
  
        SQLSYSADMINACCOUNTS="\<DomainName\UserName>"  
  
        ; Accept the License agreement to continue with Installation  
  
        IAcceptSQLServerLicenseTerms="True"  
  
        ```  
  
    -   Instalação dos componentes de conectividade. O exemplo a seguir mostra como instalar os componentes de conectividade:  
  
        ```  
        ; SQL Server Configuration File  
        [OPTIONS]  
  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=Conn  
  
        ; Specifies acceptance of License Terms  
  
        IAcceptSQLServerLicenseTerms="True  
  
        ```  
  
    -   Instalando todos os recursos com suporte  
  
        O exemplo a seguir mostra como instalar todos os recursos com suporte do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no Server Core:  
  
        ```  
        ; SQL Server Configuration File  
        [OPTIONS]  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=SQLENGINE,FullText,Replication,AS,IS,Conn  
  
        ; Specify a default or named instance. MSSQLSERVER is the default instance for non-Express editions and SQLExpress for Express editions. This parameter is required when installing the ssNoVersion Database Engine (SQL), or Analysis Services (AS).  
  
        INSTANCENAME="MSSQLSERVER"  
  
        ; Specify the Instance ID for the ssNoVersion features you have specified. ssNoVersion directory structure, registry structure, and service names will incorporate the instance ID of the ssNoVersion instance.   
  
        INSTANCEID="MSSQLSERVER"  
  
        ; Account for ssNoVersion service: Domain\User or system account.   
  
        SQLSVCACCOUNT="NT Service\MSSQLSERVER"  
  
        ; Windows account(s) to provision as ssNoVersion system administrators.   
  
        SQLSYSADMINACCOUNTS="\<DomainName\UserName>"  
  
        ; The name of the account that the Analysis Services service runs under.   
  
        ASSVCACCOUNT= "NT Service\MSSQLServerOLAPService"  
  
        ; Specifies the list of administrator accounts that need to be provisioned.   
  
        ASSYSADMINACCOUNTS="\<DomainName\UserName>"  
  
        ; Specifies the server mode of the Analysis Services instance. Valid values are MULTIDIMENSIONAL, POWERPIVOT or TABULAR. ASSERVERMODE is case-sensitive. All values must be expressed in upper case.   
  
        ASSERVERMODE="MULTIDIMENSIONAL"  
  
        ; Optional value, which specifies the state of the TCP protocol for the ssNoVersion service. Supported values are: 0 to disable the TCP protocol, and 1 to enable the TCP protocol.  
  
        TCPENABLED=1  
  
        ;Specifies acceptance of License Terms  
  
        IAcceptSQLServerLicenseTerms="True"  
        ```  
  
     Veja a seguir como você pode iniciar a Instalação usando um arquivo de configuração padrão ou personalizado.  
  
    -   Inicie a instalação usando um arquivo de configuração personalizado:  
  
         Para especificar o arquivo de configuração no prompt de comando:  
  
        ```  
        Setup.exe /QS /ConfigurationFile=MyConfigurationFile.INI  
        ```  
  
         Para especificar senhas no prompt de comando em vez de no arquivo de configuração:  
  
        ```  
        Setup.exe /QS /SQLSVCPASSWORD="************" /ASSVCPASSWORD="************"  /ConfigurationFile=MyConfigurationFile.INI  
        ```  
  
    -   Inicie a instalação usando DefaultSetup.ini:  
  
         Se o arquivo DefaultSetup.ini estiver nas pastas \x86 e \x64 no nível raiz da mídia de origem do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , abra o arquivo DefaultSetup.ini e adicione o parâmetro *Features* a ele.  
  
         Se o arquivo DefaultSetup.ini não existir, você poderá criá-lo e copiá-lo nas pastas \x86 e \x64 no nível raiz da mídia de origem do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="configure-remote-access-of-includessnoversionincludesssnoversion-mdmd-on-server-core"></a>Configurar o acesso remoto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Server Core  
 Execute as ações descritas abaixo para configurar o acesso remoto de uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em execução no Server Core.  
  
### <a name="enable-remote-connections-on-the-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Habilitar conexões remotas na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  

Para habilitar conexões remotas, use o SQLCMD.exe localmente e execute as instruções a seguir na instância do Server Core:  

   ```Transact-SQL
   EXEC sys.sp_configure N'remote access', N'1'  
   GO
   RECONFIGURE WITH OVERRIDE
   GO
   ```  
  
### <a name="enable-and-start-the-includessnoversionincludesssnoversion-mdmd-browser-service"></a>Habilitar e iniciar o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] browser service  
 Por padrão, o serviço Navegador está desabilitado.  Se ele estiver desabilitado em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução no Server Core, execute o seguinte comando no prompt de comando para habilitá-lo:  
  
 `sc config SQLBROWSER start= auto`  
  
 Depois de habilitá-lo, execute o seguinte comando a partir do prompt de comando para iniciar o serviço:  
  
 `net start SQLBROWSER`  
  
### <a name="create-exceptions-in-windows-firewall"></a>Criar exceções no Firewall do Windows  
 Para criar exceções para o acesso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Firewall do Windows, siga as etapas especificadas em [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
### <a name="enable-tcpip-on-the-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Habilitar TCP/IP na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 O protocolo TCP/IP pode ser habilitado por meio do Windows PowerShell para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Server Core. Siga estas etapas:  
  
1.  No servidor, inicie o Gerenciador de Tarefas.  
  
2.  Na guia **Aplicativos** , clique em **Nova Tarefa**.  
  
3.  Na caixa de diálogo **Criar Nova Tarefa** , digite **sqlps.exe** no campo **Abrir** e clique em **OK**. Isso abrirá a janela **[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell**.  
  
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
  
## <a name="uninstall"></a>Desinstalar

 Depois de fazer logon em um computador que executa o Server Core, você terá um ambiente de área de trabalho limitado com um prompt de comando de Administrador. Use esse prompt de comando para iniciar a desinstalação de um [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para desinstalar uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], inicie a desinstalação do prompt de comando no modo silencioso completo usando o parâmetro /Q ou no modo silencioso simples usando o parâmetro /QS. O parâmetro /QS mostra o progresso por meio da interface de usuário, mas não aceita nenhuma entrada. /Q é executado no modo silencioso sem nenhuma interface de usuário.  
  
 Para desinstalar uma instância existente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
Setup.exe /Q /Action=Uninstall /FEATURES=SQLEngine,AS,IS /INSTANCENAME=MSSQLSERVER  
```  
  
 Para remover uma instância nomeada, especifique o nome da instância, em vez de `MSSQLSERVER` no exemplo anterior.  
  
## <a name="start-a-new-command-prompt"></a>Iniciar um novo prompt de comando

Se você fechar acidentalmente o prompt de comando, siga estas etapas para iniciar um novo prompt de comando:  
 
1.  Pressione Ctrl+Shift+Esc para exibir o Gerenciador de Tarefas.  
2.  Na guia **Aplicativos** , clique em **Nova Tarefa**.  
3.  Na caixa de diálogo **Criar Nova Tarefa** , digite **cmd** no campo **Abrir** e [!INCLUDE[clickOK](../../includes/clickok-md.md)].  
  
## <a name="see-also"></a>Confira também  
 [Instalar o SQL Server usando um arquivo de configuração](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)   
 [Instalar o SQL Server do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [Edições e recursos com suporte do SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md)   
 [Instalar o Server Core](https://technet.microsoft.com/windows-server-docs/get-started/getting-started-with-server-core)   
 [Configurar uma instalação do Server Core do Windows Server 2016 com Sconfig.cmd](https://technet.microsoft.com/windows-server-docs/get-started/sconfig-on-ws2016)   
 [Cmdlets de cluster de failover no Windows PowerShell](/powershell/module/failoverclusters/)

  
  

