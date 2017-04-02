---
title: "Instalar o SQL Server 2016 no Server Core | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1dd294cc-5b69-4d0c-9005-3e307b75678b
caps.latest.revision: 43
ms.author: "mikeray"
manager: "jhubbard"
---
# Instalar o SQL Server 2016 no Server Core
  Você pode instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma instalação do Server Core do [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 ou do [!INCLUDE[win8srv](../../includes/win8srv-md.md)]. Este tópico apresenta detalhes de configuração específicos sobre a instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no Server Core.  
  
 A opção de instalação do Server Core para o sistema operacional [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] ou [!INCLUDE[win8srv](../../includes/win8srv-md.md)] oferece um ambiente mínimo para a execução de funções de servidor específicas. Isso ajuda a reduzir os requisitos de manutenção e gerenciamento e a superfície de ataque para essas funções de servidor. Para obter mais informações sobre a implementação do Server Core no [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)], consulte [Server Core for Windows Server 2008 R2](http://go.microsoft.com/fwlink/?LinkId=202439) (Server Core para Windows Server 2008 R2) (http://go.microsoft.com/fwlink/?LinkId=202439). Para obter mais informações sobre a implementação do Server Core no [!INCLUDE[win8srv](../../includes/win8srv-md.md)], consulte [Server Core for Windows Server 2012](http://msdn.microsoft.com/library/hh846323\(VS.85\).aspx) (Server Core para Windows Server 2012) (http://msdn.microsoft.com/library/hh846323(VS.85).aspx).  
  
## <a name="prerequisites"></a>Pré-requisitos  
  
|Requisito|Como instalar o|  
|-----------------|--------------------|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]2.0 SP2|Incluído na instalação do Server Core do [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 e do [!INCLUDE[win8srv](../../includes/win8srv-md.md)]. Se essa opção não estiver habilitada, ela será habilitada por padrão pela Instalação.<br /><br /> Não é possível executar as versões 2.0, 3.0 e 3.5 lado a lado em um computador. Ao instalar o .NET Framework 3.5 SP1, você obtém as camadas de 2.0 e 3.0 automaticamente.|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 3.5 SP1 Full Profile|Incluído na instalação do Server Core do [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1. Se essa opção não estiver habilitada, ela será habilitada por padrão pela Instalação.<br /><br /> Em um computador com o sistema operacional Windows, você deverá baixar e instalar o .NET Framework 3.5 SP1 antes de executar a Instalação, para instalar os componentes dependentes do .NET 3.5 SP1.<br /><br /> Para obter mais informações sobre recomendações e a orientação sobre como adquirir e habilitar o .NET Framework 3.5 no [!INCLUDE[win8srv](../../includes/win8srv-md.md)], consulte [Microsoft .NET Framework 3.5 Deployment Considerations](http://msdn.microsoft.com/library/windows/hardware/hh975396) (Considerações sobre a implantação do Microsoft .NET Framework 3.5) (http://msdn.microsoft.com/library/windows/hardware/hh975396).|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4 Server Core Profile|Para todas as edições do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], exceto [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], a Instalação instala o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4 Server Core Profile como pré-requisito.|  
|Windows Installer 4.5|Enviado com a instalação do Server Core do [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 e do [!INCLUDE[win8srv](../../includes/win8srv-md.md)].|  
|Windows PowerShell|Enviado com a instalação do Server Core do [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 e do [!INCLUDE[win8srv](../../includes/win8srv-md.md)].|  
  
##  <a name="a-namebksupportedfeaturesa-supported-features"></a> Recursos com suporte  
 Use a tabela a seguir para descobrir quais recursos têm suporte no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em uma instalação do Server Core do [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 e do [!INCLUDE[win8srv](../../includes/win8srv-md.md)].  
  
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
|Servidor do Integration Services|Sim|Para obter mais informações sobre o novo Servidor do Integration Services e seus recursos no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], consulte [Servidor do SSIS (Integration Services)](https://msdn.microsoft.com/library/bb522534.aspx).|  
|Compatibilidade das ferramentas de cliente com versões anteriores|Não||  
|SDK de Ferramentas de cliente|Não||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online|Não||  
|Ferramentas de Gerenciamento - Básicas|Apenas remoto|Não há suporte para a instalação desses recursos no Server Core. Esses componentes podem ser instalados em um servidor diferente, que não seja o [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 ou o [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core, e conectados aos serviços de [!INCLUDE[ssDE](../../includes/ssde-md.md)] instalados no Server Core.|  
|Ferramentas de Gerenciamento – Completas|Apenas remoto|Não há suporte para a instalação desses recursos no Server Core. Esses componentes podem ser instalados em um servidor diferente, que não seja o [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 ou o [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core, e conectados aos serviços de [!INCLUDE[ssDE](../../includes/ssde-md.md)] instalados no Server Core.|  
|Distributed Replay Controller|Não||  
| Distributed Replay Client|Apenas remoto|Não há suporte para a instalação desses recursos no Server Core. Esses componentes podem ser instalados em um servidor diferente, que não seja o [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 ou o [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core, e conectados aos serviços de [!INCLUDE[ssDE](../../includes/ssde-md.md)] instalados no Server Core.|  
|SDK de Conectividade de Cliente do SQL|Sim||  
|Microsoft Sync Framework|Sim|O Microsoft Sync Framework não está incluído no pacote de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Você pode baixar a versão apropriada do Sync Framework desta página do [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkId=221788) (http://go.microsoft.com/fwlink/?LinkId=221788) e instalá-lo em um computador que esteja executando a instalação do Server Core do [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 ou [!INCLUDE[win8srv](../../includes/win8srv-md.md)].|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|Não||  
|[!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]|Não||  
  
## <a name="supported-scenario-matrix"></a>Matriz de cenários com suporte  
 A tabela a seguir mostra a matriz de cenários com suporte para a instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em uma instalação do Server Core do [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 e do [!INCLUDE[win8srv](../../includes/win8srv-md.md)].  
  
|||  
|-|-|  
|Edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Todas as edições de 64 bits do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]*|  
|Idioma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Todos os idiomas|  
|Idioma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na combinação de idioma/localidade do sistema operacional|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em japonês<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em alemão<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em chinês<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em árabe<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em tailandês<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em turco<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em português (Portugal)<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em inglês no Windows em inglês|  
|Windows Edition|[!INCLUDE[win8srv](../../includes/win8srv-md.md)] 64 bits x64 Datacenter<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 64 bits x64 Standard<br /><br /> Server Core do [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 bits x64 Data Center<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core do SP1 64 bits x64 Enterprise<br /><br /> Server Core do [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 bits x64 Standard<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core do SP1 64 bits x64 Web|  
  
 *Não há suporte para a instalação da versão de 32 bits das edições do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no Server Core.  
  
## <a name="upgrading"></a>Atualizando  
 Em instalações do Server Core, atualizar de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tem suporte.  
  
## <a name="installation"></a>Instalação  
 O [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] não tem suporte para a instalação por meio do assistente de instalação no sistema operacional Server Core. Quando você faz a instalação no Server Core, a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte ao modo silencioso completo usando o parâmetro /Q ou o modo Silencioso Simples usando o parâmetro /QS. Para obter mais informações, consulte [Instalar o SQL Server 2016 do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
> [!IMPORTANT]  
> Não é possível instalar o  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] lado a lado com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um computador executando o [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 ou [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core.  
  
 Independentemente do método de instalação, é necessário confirmar a aceitação dos termos da licença de software como indivíduo ou em nome de uma entidade, a menos que o uso do software seja governado por um contrato separado, como um contrato de licenciamento por volume da [!INCLUDE[msCoName](../../includes/msconame-md.md)] ou um contrato de terceiros com um ISV ou OEM.  
  
 Os termos da licença são exibidos para exame e aceitação na interface do usuário da Instalação. As instalações autônomas (usando o parâmetro /Q ou /QS) devem incluir o parâmetro /IACCEPTSQLSERVERLICENSETERMS. Você pode analisar as condições de licença separadamente em [Microsoft Software License Terms](http://go.microsoft.com/fwlink/?LinkId=148209)(em inglês).  
  
> [!NOTE]  
>  Dependendo de como você recebeu o software (por exemplo, por meio de licenciamento por volume da [!INCLUDE[msCoName](../../includes/msconame-md.md)]), o uso do software pode estar sujeito a termos e condições adicionais.  
  
 Para instalar recursos específicos, use o parâmetro /FEATURES e especifique o recurso pai ou os valores de recursos. Para obter mais informações sobre os parâmetros de recursos e seu uso, consulte as seções a seguir.  
  
### <a name="feature-parameters"></a>Parâmetros de recursos  
  
|Parâmetro de recurso|Descrição|  
|-----------------------|-----------------|  
|SQLENGINE|Instala apenas o [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|REPLICATION|Instala o componente Replicação juntamente com o [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
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
|/FEATURES=SQLEngine,AS,IS,Conn|Instala o [!INCLUDE[ssDE](../../includes/ssde-md.md)], o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e os componentes de conectividade.|  
|/FEATURES=SQLENGINE,ADVANCEDANALYTICS /IACCEPTROPENLICENSETERMS |Instala o [!INCLUDE[ssDE](../../includes/ssde-md.md)] e o [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)].|  

  
### <a name="installation-options"></a>Opções de instalação  
 A Instalação dá suporte às opções de instalação a seguir enquanto instala o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em um sistema operacional do Server Core:  
  
1.  **Instalação da linha de comando**  
  
     Para instalar recursos específicos usando a opção de instalação do prompt de comando, use o parâmetro /FEATURES e especifique o recurso pai ou os valores de recursos listados. Um exemplo de como usar os parâmetros a partir da linha de comando é apresentado a seguir:  
  
    ```  
    Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,Replication /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /TCPENABLED=1 /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
2.  **Instalação usando o arquivo de configuração**  
  
     A Instalação dá suporte ao uso do arquivo de configuração apenas através do prompt de comando. O arquivo de configuração é um arquivo de texto com a estrutura básica de um parâmetro (par de nome/valor) e um comentário descritivo. O arquivo de configuração especificado no prompt de comando deve ter uma extensão de nome de arquivo .INI. Veja a seguir exemplos de ConfigurationFile.INI:  
  
    -   Instalação do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. O exemplo a seguir mostra como instalar uma nova instância autônoma que inclui o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]:  
  
        ```  
        ; ssNoVersion Configuration File  
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
  
        SQLSYSADMINACCOUNTS="<DomainName\UserName>"  
  
        ; Accept the License agreement to continue with Installation  
  
        IAcceptSQLServerLicenseTerms="True"  
  
        ```  
  
    -   Instalação dos componentes de conectividade. O exemplo a seguir mostra como instalar os componentes de conectividade:  
  
        ```  
        ; ssNoVersion Configuration File  
        [OPTIONS]  
  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=Conn  
  
        ; Specifies acceptance of License Terms  
  
        IAcceptSQLServerLicenseTerms="True  
  
        ```  
  
    -   Instalando todos os recursos com suporte  
  
         . O exemplo a seguir mostra como instalar todos os recursos com suporte do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no Server Core:  
  
        ```  
        ; ssNoVersion Configuration File  
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
  
        SQLSYSADMINACCOUNTS="<DomainName\UserName>"  
  
        ; The name of the account that the Analysis Services service runs under.   
  
        ASSVCACCOUNT= "NT Service\MSSQLServerOLAPService"  
  
        ; Specifies the list of administrator accounts that need to be provisioned.   
  
        ASSYSADMINACCOUNTS="<DomainName\UserName>"  
  
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
  
         Se o arquivo DefaultSetup.ini estiver nas pastas \x86 e \x64 no nível raiz da mídia de origem do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], abra o arquivo DefaultSetup.ini e adicione o parâmetro *Features* a ele.  
  
         Se o arquivo DefaultSetup.ini não existir, você poderá criá-lo e copiá-lo nas pastas \x86 e \x64 no nível raiz da mídia de origem do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="configuring-remote-access-of-includessnoversiontokenssnoversionmdmd-running-on-server-core"></a>Configurando o acesso remoto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução no Server Core  
 Execute as ações descritas abaixo para configurar o acesso remoto de uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em execução em uma instalação do Server Core do [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 ou [!INCLUDE[win8srv](../../includes/win8srv-md.md)].  
  
### <a name="enable-remote-connections-on-the-instance-of-includessnoversiontokenssnoversionmdmd"></a>Habilitar conexões remotas na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Para habilitar conexões remotas, use o SQLCMD.exe localmente e execute as instruções a seguir na instância do Server Core:  
  
-   `EXEC sys.sp_configure N'remote access', N'1'`  
  
     `GO`  
  
-   `RECONFIGURE WITH OVERRIDE`  
  
     `GO`  
  
### <a name="enable-and-start-the-includessnoversiontokenssnoversionmdmd-browser-service"></a>Habilitar e iniciar o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser  
 Por padrão, o serviço Navegador está desabilitado.  Se ele estiver desabilitado em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução no Server Core, execute o seguinte comando no prompt de comando para habilitá-lo:  
  
 `sc config SQLBROWSER start= auto`  
  
 Depois de habilitá-lo, execute o seguinte comando a partir do prompt de comando para iniciar o serviço:  
  
 `net start SQLBROWSER`  
  
### <a name="create-exceptions-in-windows-firewall"></a>Criar exceções no Firewall do Windows  
 Para criar exceções para o acesso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Firewall do Windows, siga as etapas especificadas em [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
### <a name="enable-tcpip-on-the-instance-of-includessnoversiontokenssnoversionmdmd"></a>Habilitar TCP/IP na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 O protocolo TCP/IP pode ser habilitado por meio do Windows PowerShell para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Server Core. Siga estas etapas:  
  
1.  No computador executando o [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 ou [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core, inicie o Gerenciador de Tarefas.  
  
2.  Na guia **Aplicativos** , clique em **Nova Tarefa**.  
  
3.  Na caixa de diálogo **Criar Nova Tarefa** , digite **sqlps.exe** no campo **Abrir** e clique em **OK**. Isso abrirá a janela **[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell**.  
  
4.  Na janela **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell**, execute o script a seguir para habilitar o protocolo TCP/IP:  
  
```  
$smo = 'Microsoft.SqlServer.Management.Smo.'  
$wmi = new-object ($smo + 'Wmi.ManagedComputer')  
# Enable the TCP protocol on the default instance.  If the instance is named, replace MSSQLSERVER with the instance name in the following line.  
$uri = "ManagedComputer[@Name='" + (get-item env:\computername).Value + "']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
$Tcp = $wmi.GetSmoObject($uri)  
$Tcp.IsEnabled = $true  
$Tcp.Alter()  
$Tcp  
```  
  
## <a name="uninstallation"></a>Desinstalação  
 Depois que fizer logon em um computador executando o [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 ou [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core, você terá um ambiente de desktop limitado com um prompt de comando de Administrador. Você pode usar esse prompt de comando para iniciar a desinstalação de uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para desinstalar uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], inicie a desinstalação do prompt de comando no modo silencioso completo usando o parâmetro /Q ou no modo silencioso simples usando o parâmetro /QS. O parâmetro /QS mostra o progresso por meio da interface de usuário, mas não aceita nenhuma entrada. /Q é executado no modo silencioso sem nenhuma interface de usuário.  
  
 Para desinstalar uma instância existente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
Setup.exe /Q /Action=Uninstall /FEATURES=SQLEngine,AS,IS /INSTANCENAME=MSSQLSERVER  
```  
  
 Para remover uma instância nomeada, especifique o nome da instância, em vez de "MSSQLSERVER" no exemplo anterior.  
  
> [!WARNING]  
>  Se você fechar acidentalmente o prompt de comando, siga estas etapas para iniciar um novo prompt de comando:  
>   
>  1.  Pressione Ctrl+Shift+Esc para exibir o Gerenciador de Tarefas.  
> 2.  Na guia **Aplicativos** , clique em **Nova Tarefa**.  
> 3.  Na caixa de diálogo **Criar Nova Tarefa** , digite **cmd** no campo **Abrir** e [!INCLUDE[clickOK](../../includes/clickok-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Instalar o SQL Server 2016 usando um arquivo de configuração](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)   
 [Instalar o SQL Server 2016 do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [Recursos com suporte nas edições do SQL Server 2016](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)   
 [Guia de introdução da opção de instalação do Server Core](http://go.microsoft.com/fwlink/?LinkId=221422)   
 [Configuração da instalação do Server Core: visão geral](http://go.microsoft.com/fwlink/?LinkId=221423)   
 [Cmdlets de cluster de failover no Windows PowerShell listados por foco de tarefa](http://go.microsoft.com/fwlink/?LinkId=221419)   
 [Mapeamento de comandos do Cluster.exe para cmdlets do Windows PowerShell para clusters de failover](http://go.microsoft.com/fwlink/?LinkId=221421)  
  
  