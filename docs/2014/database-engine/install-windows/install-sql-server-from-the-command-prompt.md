---
title: Instalar o SQL Server 2014 do Prompt de comando | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- installing SQL Server, command prompt
- installation scripts [SQL Server]
- maintenance scripts [SQL Server]
- REMOVENODE property
- components [SQL Server], removing
- command prompt [SQL Server], SQL Server installations
- ASACCOUNT parameter
- failover clustering [SQL Server], installing
- master database [SQL Server], rebuilding
- SQLCOLLATION parameter
- clusters [SQL Server], installing
- unattended installations [SQL Server]
- modifying collations
- AGTPASSWORD parameter
- USESYSDB parameter
- RSPASSWORD parameter
- AUTOSTART parameter
- ASPASSWORD parameter
- stand-alone installations [SQL Server]
- SAMPLEDATABASESERVER parameter
- adding components
- SAPWD parameter
- scripts [SQL Server], uninstallations
- remote installations [SQL Server]
- components [SQL Server], installing
- TARGETCOMPUTER parameter
- REMOVENODE parameter
- REINSTALLMODE parameter
- scripts [SQL Server], maintenance
- rebuilding registry
- SQLPASSWORD parameter
- rebuilding databases
- IP property
- PIDKEY parameter
- RSCONFIGURATION parameter
- ADDLOCAL parameter
- Setup [SQL Server], command prompt
- REBUILDDATABASE parameter
- SECURITYMODE parameter
- REMOVE property
- DISABLENETWORKPROTOCOLS parameter
- INSTALLDATADIR parameter
- REMOVE parameter
- removing components
- SQLACCOUNT parameter
- parameters [SQL Server], SQL Server installations
- UPGRADE parameter
- shortcuts [SQL Server]
- updating components
- removing SQL Server
- clustered instance of SQL Server
- INSTALLSQLDATADIR parameter
- RSACCOUNT parameter
- ADMINPASSWORD parameter
- GROUP property
- ERRORREPORTING property
- uninstallation scripts [SQL Server]
- AGTACCOUNT parameter
- SAVESYSDB parameter
- INSTALLVS parameter
- INSTANCENAME parameter
- scripts [SQL Server], installations
- rebuilding database, master
- uninstalling SQL Server
- ASCOLLATION parameter
- .ini files
- ADDNODE parameter
- command line installations [SQL Server]
- VS parameter
- INSTALLASDATADIR parameter
- INSTALLSQLDIR parameter
- nodes [Faillover Clustering], command prompt
- INSTALLSQLSHAREDDIR parameter
ms.assetid: df40c888-691c-4962-a420-78a57852364d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0f533591be751375ce5686b7c2998af6410fb311
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53366278"
---
# <a name="install-sql-server-2014-from-the-command-prompt"></a>Install SQL Server 2014 from the Command Prompt
  Antes de executar a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [Planning a SQL Server Installation](../../sql-server/install/planning-a-sql-server-installation.md).  
  
 A instalação de uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no prompt de comando permite especificar os recursos a serem instalados e como eles devem ser configurados. Você também pode especificar interação silenciosa, básica ou completa com a interface do usuário de Instalação.  
  
> [!NOTE]  
>  Quando você instala pelo prompt de comando, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte ao modo silencioso completo usando o parâmetro /Q ou o modo Silencioso Simples usando o parâmetro /QS. A opção /QS mostra apenas o andamento, não aceita nenhuma entrada e não exibe nenhuma mensagem de erro, se encontrado. O parâmetro /QS só tem suporte quando /Action=install é especificado.  
  
 Independentemente do método de instalação, é necessário confirmar a aceitação dos termos da licença de software como indivíduo ou em nome de uma entidade, a menos que o uso do software seja governado por um contrato separado, como um contrato de licenciamento por volume da [!INCLUDE[msCoName](../../includes/msconame-md.md)] ou um contrato de terceiros com um ISV ou OEM.  
  
 Os termos da licença são exibidos para exame e aceitação na interface do usuário da Instalação. As instalações autônomas (usando o parâmetro /Q ou /QS) devem incluir o parâmetro /IACCEPTSQLSERVERLICENSETERMS. Você pode analisar as condições de licença separadamente em [Microsoft Software License Terms](https://go.microsoft.com/fwlink/?LinkId=148209)(em inglês).  
  
> [!NOTE]  
>  Dependendo de como você recebeu o software (por exemplo, por meio de licenciamento por volume da [!INCLUDE[msCoName](../../includes/msconame-md.md)] ), o uso do software pode estar sujeito a termos e condições adicionais.  
  
 Há suporte à instalação de prompt de comando nos seguintes cenários:  
  
-   Instalação, atualização ou remoção de uma instância e de componentes compartilhados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um computador local usando sintaxe e parâmetros especificados no prompt de comando.  
  
-   Instalando, atualizando ou removendo uma instância de cluster de failover.  
  
-   Atualizando de uma edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para outra edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Instalando uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um computador local usando sintaxe e parâmetros especificados em um arquivo de configuração. É possível usar esse método para copiar uma configuração de instalação em vários computadores ou para instalar vários nós de uma instalação de cluster de failover.  
  
 Ao instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no prompt de comando, especifique parâmetros de Instalação para sua instalação no prompt de comando como parte da sintaxe de instalação.  
  
> [!NOTE]  
>  Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto. Para instalações de cluster de failover, você deve ter privilégios de administrador local com permissões para fazer logon como um serviço e atuar como parte do sistema operacional em todos os nós do cluster de failover.  
  
##  <a name="ProperUse"></a> Uso apropriado dos parâmetros de instalação  
 Use as diretrizes a seguir para desenvolver comandos de instalação com a sintaxe correta:  
  
-   /PARAMETER  
  
-   /PARAMETER=true/false  
  
-   /PARAMETER=1/0 para tipos boolianos  
  
-   /PARAMETER="valor" para todos os parâmetros de valor único. O uso de aspas duplas é recomendado, mas é obrigatório se o valor contiver um espaço.  
  
-   /PARAMETER="value1" "value2" "value3" para todos os parâmetros de vários valores. O uso de aspas duplas é recomendado, mas é obrigatório se o valor contiver um espaço.  
  
 **Exceções:**  
  
-   /FEATURES, que é um parâmetro de vários valores, mas seu formato é /FEATURES=AS,RS,IS sem nenhum espaço e delimitado por vírgulas  
  
 **Exemplos:**  
  
-   /INSTANCEDIR=c:\Path tem suporte.  
  
-   /INSTANCEDIR = "c:\Path" é suportado  
  
> [!NOTE]
>  -   Os valores de servidores relacionais dão suporte aos formatos de barra invertida finais adicionais (caracteres de barra invertida ou duas barras invertidas) para o caminho.  
> -   /PID, o valor deste parâmetro deve ser incluído entre aspas duplas.  
  
## <a name="includessnoversionincludesssnoversion-mdmd-parameters"></a>Parâmetros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 As seções a seguir fornecem parâmetros para o desenvolvimento de scripts de instalação de linha de comando a fim de instalar, atualizar e reparar cenários.  
  
 Os parâmetros listados para um componente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são específicos àquele componente. Os parâmetros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e do Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são aplicáveis quando você instala o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
-   [Parâmetros de instalação](#Install)  
  
-   [Parâmetros do SysPrep](#SysPrep)  
  
-   [Parâmetros de atualização](#Upgrade)  
  
-   [Parâmetros de reparo](#Repair)  
  
-   [Parâmetros de recompilação do banco de dados do sistema](#Rebuild)  
  
-   [Parâmetros de desinstalação](#Uninstall)  
  
-   [Parâmetros de cluster de failover](#ClusterInstall)  
  
-   [Parâmetros de contas de serviço](#Accounts)  
  
-   [Parâmetros de funcionalidades](#Feature)  
  
-   [Parâmetros de função](install-sql-server-from-the-command-prompt.md#role)  
  
-   [Controlando o comportamento de failover com o parâmetro /FAILOVERCLUSTERROLLOWNERSHIP](install-sql-server-from-the-command-prompt.md#rollownership)  
  
-   [Configuração de ID da Instância ou InstanceID](install-sql-server-from-the-command-prompt.md#instanceid)  
  
##  <a name="Install"></a> Parâmetros de instalação  
 Use os parâmetros listados na tabela a seguir para desenvolver scripts de linha de comando para a instalação.  
  
|componente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Parâmetro|Descrição|  
|-----------------------------------------|---------------|-----------------|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ACTION<br /><br /> **Necessário**|Necessário para indicar o fluxo de trabalho da instalação. Valores com suporte:<br /><br /> Instalar|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Necessário somente quando o parâmetro /Q ou /QS é especificado para instalações autônomas.**|Necessário para confirmar a aceitação dos termos de licença.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ENU<br /><br /> **Opcional**|Use esse parâmetro para instalar a versão em inglês do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um sistema operacional localizado quando a mídia de instalação incluir pacotes do idioma inglês e do idioma correspondente ao sistema operacional.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/UpdateEnabled<br /><br /> **Opcional**|Especifique se a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve descobrir e incluir atualizações de produto. Os valores válidos são True e False ou 1 e 0. Por padrão, a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluirá as atualizações localizadas.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/UpdateSource<br /><br /> **Opcional**|Especifique o local em que a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] obterá as atualizações de produto. Os valores válidos são “MU” para pesquisar [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, um caminho de pasta válido, um caminho relativo, por exemplo .\MyUpdates ou um compartilhamento UNC. Por padrão, a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pesquisará o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update ou um serviço Windows Update por meio do Windows Server Update Services.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/CONFIGURATIONFILE<br /><br /> **Opcional**|Especifica o [ConfigurationFile](install-sql-server-using-a-configuration-file.md) a ser usado.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ERRORREPORTING<br /><br /> **Opcional**|Especifica o relatório de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Para obter mais informações, consulte a [Política de Privacidade do Serviço de Relatório de Erros da Microsoft](https://go.microsoft.com/fwlink/?LinkID=72173). Valores com suporte:<br /><br /> 1=habilitado<br /><br /> 0=desabilitado|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FEATURES<br /><br /> - Ou -<br /><br /> /ROLE<br /><br /> **Necessário**|Especifica os componentes a serem instalados.<br /><br /> Escolha **/FEATURES** para especificar componentes individuais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instalar. Para obter mais informações, consulte a [Parâmetros de recursos](#Feature) abaixo.<br /><br /> Escolha [Parâmetros de função](#Role) para especificar uma função de instalação. As funções de instalação instalam o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma configuração predeterminada.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/HELP, H, ?<br /><br /> **Opcional**|Exibe as opções de uso dos parâmetros de instalação.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INDICATEPROGRESS<br /><br /> **Opcional**|Especifica que o arquivo de log de Instalação detalhado será conectado ao console.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTALLSHAREDDIR<br /><br /> **Opcional**|Especifica um diretório de instalação não padrão para componentes compartilhados de 64 bits.<br /><br /> O padrão é % arquivos de programas %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> Não é possível definir como % arquivos de programas(x86%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTALLSHAREDWOWDIR<br /><br /> **Opcional**|Especifica um diretório de instalação não padrão para componentes compartilhados de 32 bits. Com suporte apenas em sistemas de 64 bits.<br /><br /> O padrão é % programas(x86%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> Não pode ser definido como % arquivos de programas %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTANCEDIR<br /><br /> **Opcional**|Especifica um diretório de instalação não padrão para componentes específicos à instância.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTANCEID<br /><br /> **Opcional**|Especifica um valor não padrão para uma [InstanceID](#InstanceID).|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTANCENAME<br /><br /> **Necessário**|Especifica um nome de instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Para obter mais informações, consulte [Instance Configuration](../../sql-server/install/instance-configuration.md).|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/PID<br /><br /> **Opcional**|Especifica a chave do produto (Product Key) da edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se esse parâmetro não for especificado, a versão Evaluation será usada.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/Q<br /><br /> **Opcional**|Especifica que a Instalação é executada em modo silencioso sem nenhuma interface do usuário. Isso é usado para instalações autônomas.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/QS<br /><br /> **Opcional**|Especifica que a Instalação é executada e mostra o andamento por meio da interface do usuário, mas não aceita nenhuma entrada nem mostra nenhuma mensagem de erro.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/UIMODE<br /><br /> **Opcional**|Especifica se deve apresentar somente o número mínimo de caixas de diálogo durante a instalação. <br />                **/UIMode** somente pode ser usado com os parâmetros **/ACTION=INSTALL** e **UPGRADE** . Valores com suporte:<br /><br /> **/UIMODE=Normal** é o padrão para edições diferentes de Express e apresenta todas as caixas de diálogo de instalação para os recursos selecionados.<br /><br /> **/UIMODE=AutoAdvance** é o padrão para edições Express e ignora caixas de diálogo dispensáveis.<br /><br /> <br /><br /> Quando combinado com outros parâmetros, **UIMODE** é substituído. Por exemplo, quando **/UIMODE=AutoAdvance** e **/ADDCURRENTUSERASSQLADMIN=FALSE** são ambos fornecidos, a caixa de diálogo de provisionamento não é automaticamente populada com o usuário atual.<br /><br /> A configuração **UIMode** não pode ser usada com os parâmetros **/Q** ou **/QS** .|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/SQMREPORTING<br /><br /> **Opcional**|Especifica o relatório de uso de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Para obter mais informações, consulte a [Política de Privacidade do Serviço de Relatório de Erros da Microsoft](https://go.microsoft.com/fwlink/?LinkID=72173). Valores com suporte:<br /><br /> 1=habilitado<br /><br /> 0=desabilitado|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/HIDECONSOLE<br /><br /> **Opcional**|Especifica se a janela do console é ocultada ou fechada.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent|/AGTSVCACCOUNT<br /><br /> **Necessário**|Especifica a conta do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent|/AGTSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha da conta do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent|/AGTSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica o modo de [inicialização](#Accounts) do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Valores com suporte:<br /><br /> Automatic<br /><br /> Desabilitado<br /><br /> Manual|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASBACKUPDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de backup do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores padrão:<br /><br /> Para o modo WOW em 64 bits: % programas(x86\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\olap\backup.<br /><br /> Para todas as outras instalações: % Program Files %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\olap\backup.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCOLLATION<br /><br /> **Opcional**|Especifica a configuração de ordenação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Valor padrão:<br /><br /> Latin1_General_CI_AS|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCONFIGDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de configuração do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores padrão:<br /><br /> Para o modo WOW em 64 bits: % programas(x86\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\olap\config.<br /><br /> Para todas as outras instalações: % Program Files %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\olap\config.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASDATADIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores padrão:<br /><br /> Para o modo WOW em 64 bits: % programas(x86\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\OLAP\Data.<br /><br /> Para todas as outras instalações: % Program Files %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\OLAP\Data.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASLOGDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de log do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores padrão:<br /><br /> Para o modo WOW em 64 bits: % programas(x86\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\olap\log.<br /><br /> Para todas as outras instalações: % Program Files %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\olap\log.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSERVERMODE<br /><br /> **Opcional**|Especifica o modo de servidor da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Os valores válidos são MULTIDIMENSIONAL, POWERPIVOT ou TABULAR. **ASSERVERMODE** diferencia maiúsculas de minúsculas. Todos os valores devem ser expressos em maiúsculas. Para obter mais informações sobre valores válidos, consulte [Install Analysis Services in Tabular Mode](../../analysis-services/instances/install-windows/install-analysis-services.md).|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCACCOUNT<br /><br /> **Necessário**|Especifica a conta de serviço do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha do serviço [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica o modo de [inicialização](#Accounts) do serviço [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores com suporte:<br /><br /> Automatic<br /><br /> Desabilitado<br /><br /> Manual|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSYSADMINACCOUNTS<br /><br /> **Necessário**|Especifica as credenciais de administrador do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASTEMPDIR<br /><br /> **Opcional**|Especifica o diretório de arquivos temporários do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores padrão:<br /><br /> Para o modo WOW em 64 bits: % programas(x86\\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \\< INSTANCEDIR\>\\< ASInstanceID\>\olap\temp.<br /><br /> Para todas as outras instalações: % Program Files %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\olap\temp.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASPROVIDERMSOLAP<br /><br /> **Opcional**|Especifica se o provedor MSOLAP pode ser executado no processo. Valor padrão:<br /><br /> 1=habilitado|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/FARMACCOUNT<br /><br /> **Necessário para SPI_AS_NewFarm**|Especifica uma conta de usuário de domínio para executar serviços de Administração Central do SharePoint e outros serviços essenciais em um farm.<br /><br /> Esse parâmetro é usado apenas para instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instaladas por meio de [Parâmetros de função](#Role)= SPI_AS_NEWFARM.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/FARMPASSWORD<br /><br /> **Necessário para SPI_AS_NewFarm**|Especifica uma senha para a conta do farm.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/PASSPHRASE<br /><br /> **Necessário para SPI_AS_NewFarm**|Especifica uma frase secreta que será usada para adicionar outros servidores de aplicativos ou servidores Web front-end a um farm do SharePoint.<br /><br /> Esse parâmetro é usado apenas para instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instaladas por meio de [Parâmetros de função](#Role) = SPI_AS_NEWFARM.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/FARMADMINIPORT<br /><br /> **Necessário para SPI_AS_NewFarm**|Especifica uma porta usada para conexão com o aplicativo Web Administração Central do SharePoint.<br /><br /> Esse parâmetro é usado apenas para instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instaladas por meio de [Parâmetros de função](#Role) = SPI_AS_NEWFARM.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Navegador|/BROWSERSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica o modo de [inicialização](#Accounts) do serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Valores com suporte:<br /><br /> Automatic<br /><br /> Desabilitado<br /><br /> Manual|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/ENABLERANU<br /><br /> **Opcional**|Habilita credenciais de executar como para instalações do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] .|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/INSTALLSQLDATADIR<br /><br /> **Opcional**|Especifica o diretório de dados dos arquivos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Valores padrão:<br /><br /> Para o modo WOW em 64-bits: % programas(x86%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<br /><br /> Para todas as outras instalações: % arquivos de programas %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **Necessário quando /SECURITYMODE=SQL**|Especifica a senha da conta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sa.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SECURITYMODE<br /><br /> **Opcional**|Especifica o modo de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se esse parâmetro não for fornecido, apenas o modo de autenticação do Windows terá suporte. Valor com suporte:<br /><br /> SQL|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLBACKUPDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de backup. Valor padrão:<br /><br /> \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Backup|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **Opcional**|Especifica as configurações de ordenação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> O valor padrão baseia-se na localidade do sistema operacional Windows. Para obter mais informações, veja [Configurações de ordenação na Instalação](https://msdn.microsoft.com/library/ms143508%28v=sql.105%29.aspx).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/ADDCURRENTUSERASSQLADMIN<br /><br /> **Opcional**|Adiciona o usuário atual para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `sysadmin` função de servidor fixa. O parâmetro /ADDCURRENTUSERASSQLADMIN pode ser usado ao instalar edições Express ou quando /Role=ALLFeatures_WithDefaults estiver sendo usado. Para obter mais informações, veja [/ROLE](#Role) abaixo. O uso de /ADDCURRENTUSERASSQLADMIN é opcional, mas /ADDCURRENTUSERASSQLADMIN ou /SQLSYSADMINACCOUNTS é obrigatório. Valores padrão:<br /><br /> True para edições do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> False para todas as outras edições|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **Necessário**|Especifica a conta de inicialização do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha de SQLSVCACCOUNT.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica o modo de [inicialização](#Accounts) do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Valores com suporte:<br /><br /> Automatic<br /><br /> Desabilitado<br /><br /> Manual|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **Necessário**|Use este parâmetro para provisionar logons para serem membros da função sysadmin.<br /><br /> Para as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diferentes da [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], /SQLSYSADMINACCOUNTS é obrigatório. Para as edições do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], o uso de /SQLSYSADMINACCOUNTS é opcional, mas /SQLSYSADMINACCOUNTS ou /ADDCURRENTUSERASSQLADMIN é obrigatório.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de dados do tempdb. Valor padrão:<br /><br /> \<InstallSQLDataDir > \ \<SQLInstanceID > \Mssql\Data.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de log do tempdb. Valor padrão:<br /><br /> \<InstallSQLDataDir > \ \<SQLInstanceID > \Mssql\Data.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de dados de bancos de dados do usuário. Valor padrão:<br /><br /> \<InstallSQLDataDir > \ \<SQLInstanceID > \Mssql\Data.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBLOGDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de log de bancos de dados do usuário. Valor padrão:<br /><br /> \<InstallSQLDataDir > \ \<SQLInstanceID > \Mssql\Data.|  
|FILESTREAM|/FILESTREAMLEVEL<br /><br /> **Opcional**|Especifica o nível de acesso para o recurso FILESTREAM. Valores com suporte:<br /><br /> 0 =Desabilitar o suporte ao FILESTREAM desta instância. (Valor padrão)<br /><br /> 1=Habilitar FILESTREAM para o acesso de [!INCLUDE[tsql](../../includes/tsql-md.md)] .<br /><br /> 2=Habilitar FILESTREAM para o acesso de [!INCLUDE[tsql](../../includes/tsql-md.md)] e o acesso de fluxo de E/S de arquivo. (Inválido para cenários de cluster)<br /><br /> 3=Permitir que clientes remotos tenham acesso de streaming a dados FILESTREAM.|  
|FILESTREAM|/FILESTREAMSHARENAME<br /><br /> **Opcional**<br /><br /> **Necessário quando FILESTREAMLEVEL for maior do que 1.**|Especifica o nome do compartilhamento do Windows no qual os dados FILESTREAM serão armazenados.|  
|Texto completo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FTSVCACCOUNT<br /><br /> **Opcional**|Especifica a conta do serviço iniciador de filtro de texto completo.<br /><br /> Esse parâmetro é ignorado no [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]. ServiceSID é usado para ajudar a proteger a comunicação entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o Daemon de Filtro de Texto Completo. Se os valores não forem fornecidos, o Serviço Iniciador de Filtro de Texto Completo será desabilitado. Você deve usar o Gerenciador de Controle do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para alterar a conta de serviço e habilitar a funcionalidade de texto completo. Valor padrão:<br /><br /> Conta Serviço Local|  
|Texto completo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FTSVCPASSWORD<br /><br /> **Opcional**|Especifica a senha do serviço iniciador de filtro de texto completo.<br /><br /> Esse parâmetro é ignorado no [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)].|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **Necessário**|Especifica a conta do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Valor padrão:<br /><br /> NT AUTHORITY\NETWORK SERVICE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **Opcional**|Especifica o modo de [inicialização](#Accounts) do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuração de rede|/NPENABLED<br /><br /> **Opcional**|Especifica o estado do protocolo de Pipes Nomeados para o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Valores com suporte:<br /><br /> 0=desabilitar o protocolo de Pipes Nomeados<br /><br /> 1=habilitar o protocolo de Pipes Nomeados|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuração de rede|/TCPENABLED<br /><br /> **Opcional**|Especifica o estado do protocolo TCP para o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Valores com suporte:<br /><br /> 0=desabilitar o protocolo TCP<br /><br /> 1=habilitar o protocolo TCP|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Opcional**|Especifica o modo de Instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Valores com suporte:<br /><br /> SharePointFilesOnlyMode<br /><br /> DefaultNativeMode<br /><br /> FilesOnlyMode<br /><br /> Observação: Se a instalação incluir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)], o RSINSTALLMODE padrão será DefaultNativeMode.<br /><br /> Se a instalação não incluir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do [!INCLUDE[ssDE](../../includes/ssde-md.md)], o RSINSTALLMODE padrão será FilesOnlyMode.<br /><br /> Se você escolher DefaultNativeMode, mas a instalação não incluir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do [!INCLUDE[ssDE](../../includes/ssde-md.md)], a instalação alterará automaticamente o RSINSTALLMODE para FilesOnlyMode.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT<br /><br /> **Necessário**|Especifica a conta de inicialização do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha da conta de inicialização do serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCStartupType<br /><br /> **Opcional**|Especifica o modo de [inicialização](#Accounts) do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
###### <a name="sample-syntax"></a>Sintaxe de exemplo:  
 Para instalar uma nova instância autônoma com os componentes de Replicação e Pesquisa de Texto Completo do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
```  
  
Setup.exe /q /ACTION=Install /FEATURES=SQL /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /IACCEPTSQLSERVERLICENSETERMS  
  
```  
  
##  <a name="SysPrep"></a> Parâmetros do SysPrep  
 Para obter mais informações sobre o SysPrep do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte  
  
 [Instalar o SQL Server 2014 usando SysPrep](install-sql-server-using-sysprep.md).  
  
#### <a name="prepare-image-parameters"></a>Parâmetros de preparação de imagem  
 Use os parâmetros da tabela a seguir para desenvolver scripts de linha de comando para preparar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sem configurá-la.  
  
|componente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Parâmetro|Descrição|  
|-----------------------------------------|---------------|-----------------|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ACTION<br /><br /> **Necessário**|Necessário para indicar o fluxo de trabalho de instalação. Valores com suporte:<br /><br /> PrepareImage|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Necessário somente quando o parâmetro /Q ou /QS é especificado para instalações autônomas.**|Necessário para confirmar a aceitação dos termos de licença.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ENU<br /><br /> **Opcional**|Use esse parâmetro para instalar a versão em inglês do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um sistema operacional localizado quando a mídia de instalação incluir pacotes do idioma inglês e do idioma correspondente ao sistema operacional.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/UpdateEnabled<br /><br /> **Opcional**|Especifique se a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve descobrir e incluir atualizações de produto. Os valores válidos são True e False ou 1 e 0. Por padrão, a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluirá as atualizações localizadas.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/UpdateSource<br /><br /> **Opcional**|Especifique o local em que a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] obterá as atualizações de produto. Os valores válidos são “MU” para pesquisar [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, um caminho de pasta válido, um caminho relativo, por exemplo .\MyUpdates ou um compartilhamento UNC. Por padrão, a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pesquisará o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update ou um serviço Windows Update por meio do Windows Server Update Services.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/CONFIGURATIONFILE<br /><br /> **Opcional**|Especifica o [ConfigurationFile](install-sql-server-using-a-configuration-file.md) a ser usado.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FEATURES<br /><br /> **Necessário**|Especifica os [componentes](#Feature) a serem instalados.<br /><br /> Os valores com suporte são: SQLEngine, Replication, FullText, DQ, AS, AS_SPI, RS, RS_SHP, RS_SHPWFE, DQC, SSDTBI, Conn, IS, BC, SDK, BOL, SSMS, Adv_SSMS, DREPLAY_CTLR, DREPLAY_CLT, SNAC_SDK, SQLODBC, SQLODBC_SDK, LocalDB, MDS|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/HELP, H, ?<br /><br /> **Opcional**|Exibe as opções de uso dos parâmetros de instalação.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/HIDECONSOLE<br /><br /> **Opcional**|Especifica se a janela do console é ocultada ou fechada.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INDICATEPROGRESS<br /><br /> **Opcional**|Especifica que o arquivo de log de Instalação detalhado será conectado ao console.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTALLSHAREDDIR<br /><br /> **Opcional**|Especifica um diretório de instalação não padrão para componentes compartilhados de 64 bits.<br /><br /> O padrão é % arquivos de programas %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> Não é possível definir como % arquivos de programas(x86%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTANCEDIR<br /><br /> **Opcional**|Especifica um diretório de instalação não padrão para componentes específicos à instância.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTANCEID<br /><br /> Antes do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 Atualização Cumulativa 2 (janeiro de 2013) **Obrigatório**<br /><br /> A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 Atualização Cumulativa 2 **Necessário** para recursos de instância.|Especifica um InstanceID para a instância que está sendo preparada.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/Q<br /><br /> **Opcional**|Especifica que a Instalação é executada em modo silencioso sem nenhuma interface do usuário. Isso é usado para instalações autônomas.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/QS<br /><br /> **Opcional**|Especifica que a Instalação é executada e mostra o andamento por meio da interface do usuário, mas não aceita nenhuma entrada nem mostra nenhuma mensagem de erro.|  
  
###### <a name="sample-syntax"></a>Sintaxe de exemplo:  
 Para preparar uma nova instância autônoma com os componentes de Replicação e Pesquisa de Texto Completo do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
```  
Setup.exe /q /ACTION=PrepareImage /FEATURES=SQL,RS /InstanceID =<MYINST> /IACCEPTSQLSERVERLICENSETERMS  
```  
  
#### <a name="complete-image-parameters"></a>Parâmetros de conclusão de imagem  
 Use os parâmetros da tabela a seguir para desenvolver scripts de linha de comando para concluir e configurar uma instância preparada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|componente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Parâmetro|Descrição|  
|-----------------------------------------|---------------|-----------------|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ACTION<br /><br /> **Necessário**|Necessário para indicar o fluxo de trabalho da instalação. Valores com suporte:<br /><br /> CompleteImage|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Necessário somente quando o parâmetro /Q ou /QS é especificado para instalações autônomas.**|Necessário para confirmar a aceitação dos termos de licença.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ENU<br /><br /> **Opcional**|Use esse parâmetro para instalar a versão em inglês do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um sistema operacional localizado quando a mídia de instalação incluir pacotes do idioma inglês e do idioma correspondente ao sistema operacional.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/CONFIGURATIONFILE<br /><br /> **Opcional**|Especifica o [ConfigurationFile](install-sql-server-using-a-configuration-file.md) a ser usado.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ERRORREPORTING<br /><br /> **Opcional**|Especifica o relatório de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Para obter mais informações, consulte a [Política de Privacidade do Serviço de Relatório de Erros da Microsoft](https://go.microsoft.com/fwlink/?LinkID=72173). Valores com suporte:<br /><br /> 1=habilitado<br /><br /> 0=desabilitado|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/HELP, H, ?<br /><br /> **Opcional**|Exibe as opções de uso dos parâmetros de instalação.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INDICATEPROGRESS<br /><br /> **Opcional**|Especifica que o arquivo de log de Instalação detalhado será conectado ao console.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTANCEID<br /><br /> Antes do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 Atualização Cumulativa 2 (janeiro de 2013) **Obrigatório**<br /><br /> A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 Atualização Cumulativa 2 **Opcional**|Use a ID de Instância especificada durante a etapa de preparação da imagem. Valores com suporte:<br /><br /> InstanceID de uma instância preparada.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTANCENAME<br /><br /> Antes do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 Atualização Cumulativa 2 (janeiro de 2013) **Obrigatório**<br /><br /> A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 Atualização Cumulativa 2 **Opcional**|Especifica um nome de instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a instância que está sendo concluída.<br /><br /> Para obter mais informações, consulte [Instance Configuration](../../sql-server/install/instance-configuration.md).|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/PID<br /><br /> **Opcional**|Especifica a chave do produto (Product Key) da edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se esse parâmetro não for especificado, a versão Evaluation será usada.<br /><br /> Observação: Se você estiver instalando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express with Tools ou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express com Advanced Services, o PID será predefinido.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/Q<br /><br /> **Opcional**|Especifica que a Instalação é executada em modo silencioso sem nenhuma interface do usuário. Isso é usado para instalações autônomas.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/QS<br /><br /> **Opcional**|Especifica que a Instalação é executada e mostra o andamento por meio da interface do usuário, mas não aceita nenhuma entrada nem mostra nenhuma mensagem de erro.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/SQMREPORTING<br /><br /> **Opcional**|Especifica o relatório de uso de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Para obter mais informações, consulte a [Política de Privacidade do Serviço de Relatório de Erros da Microsoft](https://go.microsoft.com/fwlink/?LinkID=72173). Valores com suporte:<br /><br /> 1=habilitado<br /><br /> 0=desabilitado|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/HIDECONSOLE<br /><br /> **Opcional**|Especifica se a janela do console é ocultada ou fechada.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent|/AGTSVCACCOUNT<br /><br /> **Necessário**|Especifica a conta do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent|/AGTSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha da conta do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent|/AGTSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica o modo de [inicialização](#Accounts) do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Valores com suporte:<br /><br /> Automatic<br /><br /> Desabilitado<br /><br /> Manual|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Navegador|/BROWSERSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica o [inicialização](#Accounts) modo para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço localizador. Valores com suporte:<br /><br /> Automatic<br /><br /> Desabilitado<br /><br /> Manual|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/ENABLERANU<br /><br /> **Opcional**|Habilita credenciais de executar como para instalações do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] .|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/INSTALLSQLDATADIR<br /><br /> **Opcional**|Especifica o diretório de dados dos arquivos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Valores padrão:<br /><br /> Para o modo WOW em 64-bits: % programas(x86%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<br /><br /> Para todas as outras instalações: % arquivos de programas %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **Necessário quando /SECURITYMODE=SQL**|Especifica a senha da conta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sa.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SECURITYMODE<br /><br /> **Opcional**|Especifica o modo de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se esse parâmetro não for fornecido, apenas o modo de autenticação do Windows terá suporte. Valor com suporte:<br /><br /> SQL|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLBACKUPDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de backup.<br /><br /> Valor padrão:<br /><br /> \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Backup|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **Opcional**|Especifica as configurações de ordenação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> O valor padrão baseia-se na localidade do sistema operacional Windows. Para obter mais informações, veja [Configurações de ordenação na Instalação](https://msdn.microsoft.com/library/ms143508%28v=sql.105%29.aspx).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **Necessário**|Especifica a conta de inicialização do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha de SQLSVCACCOUNT.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica o modo de [inicialização](#Accounts) do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Valores com suporte:<br /><br /> Automatic<br /><br /> Desabilitado<br /><br /> Manual|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **Necessário**|Use este parâmetro para provisionar logons para serem membros da função sysadmin.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de dados do tempdb.<br /><br /> Valor padrão:<br /><br /> \<InstallSQLDataDir > \ \<SQLInstanceID > \Mssql\Data.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de log do tempdb.<br /><br /> Valor padrão:<br /><br /> \<InstallSQLDataDir > \ \<SQLInstanceID > \Mssql\Data.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de dados de bancos de dados do usuário.<br /><br /> Valor padrão:<br /><br /> \<InstallSQLDataDir > \ \<SQLInstanceID > \Mssql\Data.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBLOGDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de log de bancos de dados do usuário.<br /><br /> Valor padrão:<br /><br /> \<InstallSQLDataDir > \ \<SQLInstanceID > \Mssql\Data.|  
|FILESTREAM|/FILESTREAMLEVEL<br /><br /> **Opcional**|Especifica o nível de acesso para o recurso FILESTREAM. Valores com suporte:<br /><br /> 0 =Desabilitar o suporte ao FILESTREAM desta instância. (Valor padrão)<br /><br /> 1=Habilitar FILESTREAM para o acesso de [!INCLUDE[tsql](../../includes/tsql-md.md)] .<br /><br /> 2=Habilitar FILESTREAM para o acesso de [!INCLUDE[tsql](../../includes/tsql-md.md)] e o acesso de fluxo de E/S de arquivo. (Inválido para cenários de cluster)<br /><br /> 3=Permitir que clientes remotos tenham acesso de streaming a dados FILESTREAM.|  
|FILESTREAM|/FILESTREAMSHARENAME<br /><br /> **Opcional**<br /><br /> **Necessário quando FILESTREAMLEVEL for maior do que 1.**|Especifica o nome do compartilhamento do Windows no qual os dados FILESTREAM serão armazenados.|  
|Texto completo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FTSVCACCOUNT<br /><br /> **Opcional**|Especifica a conta do serviço iniciador de filtro de texto completo.<br /><br /> Esse parâmetro é ignorado no [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]. ServiceSID é usado para ajudar a proteger a comunicação entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o Daemon de Filtro de Texto Completo. Se os valores não forem fornecidos, o Serviço Iniciador de Filtro de Texto Completo será desabilitado. Você deve usar o Gerenciador de Controle do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para alterar a conta de serviço e habilitar a funcionalidade de texto completo. Valor padrão:<br /><br /> Conta Serviço Local|  
|Texto completo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FTSVCPASSWORD<br /><br /> **Opcional**|Especifica a senha do serviço iniciador de filtro de texto completo.<br /><br /> Esse parâmetro é ignorado no [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)].|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuração de rede|/NPENABLED<br /><br /> **Opcional**|Especifica o estado do protocolo de Pipes Nomeados para o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Valores com suporte:<br /><br /> 0=desabilitar o protocolo de Pipes Nomeados<br /><br /> 1=habilitar o protocolo de Pipes Nomeados|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuração de rede|/TCPENABLED<br /><br /> **Opcional**|Especifica o estado do protocolo TCP para o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Valores com suporte:<br /><br /> 0=desabilitar o protocolo TCP<br /><br /> 1=habilitar o protocolo TCP|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Opcional**|Especifica o modo de Instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT<br /><br /> **Necessário**|Especifica a conta de inicialização do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha da conta de inicialização do serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCStartupType<br /><br /> **Opcional**|Especifica o modo de [inicialização](#Accounts) do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
###### <a name="sample-syntax"></a>Sintaxe de exemplo:  
 Para concluir uma instância autônoma preparada que inclui os componentes de Replicação e de Pesquisa de Texto Completo do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
```  
  
setup.exe /q /ACTION=CompleteImage /INSTANCENAME=MYNEWINST /INSTANCEID=<MYINST> /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /IACCEPTSQLSERVERLICENSETERMS  
  
```  
  
##  <a name="Upgrade"></a> Parâmetros de atualização  
 Use os parâmetros listados na tabela a seguir para desenvolver scripts de linha de comando para atualização.  
  
|componente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Parâmetro|Descrição|  
|-----------------------------------------|---------------|-----------------|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ACTION<br /><br /> **Necessário**|Necessário para indicar o fluxo de trabalho da instalação. Valores com suporte:<br /><br /> UPGRADE<br /><br /> EditionUpgrade<br /><br /> O valor EditionUpgrade é usado para atualizar uma edição existente do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para outra edição. Para obter mais informações sobre a versão e as atualizações de edição com suporte, consulte [Supported Version and Edition Upgrades](supported-version-and-edition-upgrades.md).|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Necessário somente quando o parâmetro /Q ou /QS é especificado para instalações autônomas.**|Necessário para confirmar a aceitação dos termos de licença.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ENU<br /><br /> **Opcional**|Use esse parâmetro para instalar a versão em inglês do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um sistema operacional localizado quando a mídia de instalação incluir pacotes do idioma inglês e do idioma correspondente ao sistema operacional.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/*UpdateEnabled*<br /><br /> **Opcional**|Especifique se a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve descobrir e incluir atualizações de produto. Os valores válidos são True e False ou 1 e 0. Por padrão, a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluirá as atualizações localizadas.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/*UpdateSource*<br /><br /> **Opcional**|Especifique o local em que a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] obterá as atualizações de produto. Os valores válidos são “MU” para pesquisar [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, um caminho de pasta válido, um caminho relativo, por exemplo .\MyUpdates ou um compartilhamento UNC. Por padrão, a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pesquisará o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update ou um serviço Windows Update por meio do Windows Server Update Services.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/CONFIGURATIONFILE<br /><br /> **Opcional**|Especifica o [ConfigurationFile](install-sql-server-using-a-configuration-file.md) a ser usado.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ERRORREPORTING<br /><br /> **Opcional**|Especifica o relatório de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Para obter mais informações, consulte a [Política de Privacidade do Serviço de Relatório de Erros da Microsoft](https://go.microsoft.com/fwlink/?LinkID=72173). Valores com suporte:<br /><br /> 1=habilitado<br /><br /> 0=desabilitado|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/HELP, H, ?<br /><br /> **Opcional**|Exibe as opções de uso dos parâmetros.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INDICATEPROGRESS<br /><br /> **Opcional**|Especifica que o arquivo de log de Instalação detalhado será conectado ao console.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ INSTANCEDIR<br /><br /> **Opcional**|Especifica um diretório de instalação não padrão para componentes compartilhados.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTANCEID<br /><br /> **Necessário ao atualizar do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]** ou posterior.<br /><br /> **Opcional ao atualizar do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]**|Especifica um valor não padrão para uma [InstanceID](#InstanceID).|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTANCENAME<br /><br /> **Necessário**|Especifica um nome de instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Para obter mais informações, consulte [Instance Configuration](../../sql-server/install/instance-configuration.md).|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/PID<br /><br /> **Opcional**|Especifica a chave do produto (Product Key) da edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se esse parâmetro não for especificado, a versão Evaluation será usada.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/Q<br /><br /> **Opcional**|Especifica que a Instalação é executada em modo silencioso sem nenhuma interface do usuário. Isso é usado para instalações autônomas.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/UIMODE<br /><br /> **Opcional**|Especifica se deve apresentar somente o número mínimo de caixas de diálogo durante a instalação. <br />                **/UIMode** somente pode ser usado com os parâmetros **/ACTION=INSTALL** e **UPGRADE** . Valores com suporte:<br /><br /> **/UIMODE=Normal** é o padrão para edições diferentes de Express e apresenta todas as caixas de diálogo de instalação para os recursos selecionados.<br /><br /> **/UIMODE=AutoAdvance** é o padrão para edições Express e ignora caixas de diálogo dispensáveis.<br /><br /> A configuração **UIMode** não pode ser usada com os parâmetros **/Q** ou **/QS** .|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/SQMREPORTING<br /><br /> **Opcional**|Especifica o relatório de uso de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Para obter mais informações, consulte a [Política de Privacidade do Serviço de Relatório de Erros da Microsoft](https://go.microsoft.com/fwlink/?LinkID=72173). Valores com suporte:<br /><br /> 1=habilitado<br /><br /> 0=desabilitado|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/HIDECONSOLE<br /><br /> **Opcional**|Especifica se a janela do console deve ser ocultada ou fechada.|  
|Serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/BROWSERSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica o modo de [inicialização](#Accounts) do serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Valores com suporte:<br /><br /> Automatic<br /><br /> Desabilitado<br /><br /> Manual|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Texto completo|/FTUPGRADEOPTION<br /><br /> **Opcional**|Especifica a opção de atualização do catálogo de Texto Completo. Valores com suporte:<br /><br /> REBUILD<br /><br /> RESET<br /><br /> IMPORT|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **Necessário**|Especifica a conta do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Valor padrão:<br /><br /> NT AUTHORITY\NETWORK SERVICE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **Opcional**|Especifica o modo de [inicialização](#Accounts) do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSUPGRADEDATABASEACCOUNT<br /><br /> **Opcional**|A propriedade só é usada ao atualizar um servidor de relatório no modo SharePoint que seja da versão 2008 R2 ou anterior. As demais operações de atualização são executadas para servidores de relatório que usam a arquitetura mais antiga do modo do SharePoint, que foi modificada no SQL Server 2012 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Se essa opção não estiver incluída com a instalação de linha de comando, o serviço de conta padrão para a instância do servidor de relatório antigo será usado. Se esta propriedade for usada, forneça a senha para a conta usando a propriedade **/RSUPGRADEPASSWORD** .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSUPGRADEPASSWORD<br /><br /> **Opcional**|Senha da conta de serviço do Servidor de Relatórios existente.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/ALLOWUPGRADEFORSSRSSHAREPOINTMODE|A troca é necessária ao atualizar uma instalação do modo SharePoint que se baseia na arquitetura de serviço compartilhado do SharePoint. A opção não é necessária para atualizar versões de serviço não compartilhadas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
###### <a name="sample-syntax"></a>Sintaxe de exemplo:  
 Para atualizar uma instância existente ou um nó de cluster de failover de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)],  
  
```  
Setup.exe /q /ACTION=upgrade /INSTANCEID = <INSTANCEID>/INSTANCENAME=MSSQLSERVER /RSUPGRADEDATABASEACCOUNT="<Provide a SQL Server logon account that can connect to the report server during upgrade>" /RSUPGRADEPASSWORD="<Provide a password for the report server upgrade account>" /ISSVCAccount="NT Authority\Network Service" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
##  <a name="Repair"></a> Parâmetros de reparo  
 Use os parâmetros listados na tabela a seguir para desenvolver scripts de linha de comando para reparação.  
  
|componente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Parâmetro|Descrição|  
|-----------------------------------------|---------------|-----------------|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ACTION<br /><br /> **Necessário**|Necessário para indicar o fluxo de trabalho de reparo. Valores com suporte:<br /><br /> Reparar|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ENU<br /><br /> **Opcional**|Use esse parâmetro para instalar a versão em inglês do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um sistema operacional localizado quando a mídia de instalação incluir pacotes do idioma inglês e do idioma correspondente ao sistema operacional.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FEATURES<br /><br /> **Necessário**|Especifica os [componentes](#Feature) a serem reparados.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTANCENAME<br /><br /> **Necessário**|Especifica um nome de instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Para obter mais informações, consulte [Instance Configuration](../../sql-server/install/instance-configuration.md).|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/Q<br /><br /> **Opcional**|Especifica que a Instalação é executada em modo silencioso sem nenhuma interface do usuário. Isso é usado para instalações autônomas.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/HIDECONSOLE<br /><br /> **Opcional**|Especifica se a janela do console é ocultada ou fechada.|  
  
###### <a name="sample-syntax"></a>Sintaxe de exemplo:  
 Reparar uma instância e os componentes compartilhados.  
  
```  
Setup.exe /q /ACTION=Repair /INSTANCENAME=<instancename>  
```  
  
##  <a name="Rebuild"></a> Parâmetros de recompilação do banco de dados do sistema  
 Use os parâmetros listados na tabela a seguir para desenvolver scripts de linha de comando para recompilar os bancos de dados do sistema mestre, modelo, msdb e tempdb. Para obter mais informações, consulte [Recriar bancos de dados do sistema](../../relational-databases/databases/system-databases.md).  
  
|componente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Parâmetro|Descrição|  
|-----------------------------------------|---------------|-----------------|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ACTION<br /><br /> **Necessário**|Necessário para indicar o fluxo de trabalho de reconstrução do banco de dados. Valores com suporte:<br /><br /> Rebuilddatabase|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTANCENAME<br /><br /> **Necessário**|Especifica um nome de instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Para obter mais informações, consulte [Instance Configuration](../../sql-server/install/instance-configuration.md).|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/Q<br /><br /> **Opcional**|Especifica que a Instalação é executada em modo silencioso sem nenhuma interface do usuário. Isso é usado para instalações autônomas.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **Opcional**|Especifica uma nova ordenação no nível do servidor.<br /><br /> O valor padrão baseia-se na localidade do sistema operacional Windows. Para obter mais informações, veja [Configurações de ordenação na Instalação](https://msdn.microsoft.com/library/ms143508%28v=sql.105%29.aspx).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **Necessário quando /SECURITYMODE=SQL tiver sido especificado durante a instalação da instância.**|Especifica a senha da conta SA do SQL.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **Necessário**|Use este parâmetro para provisionar logons para serem membros da função sysadmin.|  
  
##  <a name="Uninstall"></a> Parâmetros de desinstalação  
 Use os parâmetros listados na tabela a seguir para desenvolver scripts de linha de comando para desinstalação.  
  
|componente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Parâmetro|Descrição|  
|-----------------------------------------|---------------|-----------------|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ACTION<br /><br /> **Necessário**|Necessário para indicar o fluxo de trabalho da desinstalação. Valores com suporte:<br /><br /> Desinstalar|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/CONFIGURATIONFILE<br /><br /> **Opcional**|Especifica o [ConfigurationFile](install-sql-server-using-a-configuration-file.md) a ser usado.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FEATURES<br /><br /> **Necessário**|Especifica os [componentes](#Feature) a serem desinstalados.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/HELP, H, ?<br /><br /> **Opcional**|Exibe as opções de uso dos parâmetros.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INDICATEPROGRESS<br /><br /> **Opcional**|Especifica que o arquivo de log de Instalação detalhado será conectado ao console.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTANCENAME<br /><br /> **Necessário**|Especifica um nome de instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Para obter mais informações, consulte [Instance Configuration](../../sql-server/install/instance-configuration.md).|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/Q<br /><br /> **Opcional**|Especifica que a Instalação é executada em modo silencioso sem nenhuma interface do usuário. Isso é usado para instalações autônomas.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/HIDECONSOLE<br /><br /> **Opcional**|Especifica se a janela do console é ocultada ou fechada.|  
  
###### <a name="sample-syntax"></a>Sintaxe de exemplo:  
 Para desinstalar uma instância existente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
Setup.exe /Action=Uninstall /FEATURES=SQL,AS,RS,IS,Tools /INSTANCENAME=MSSQLSERVER  
```  
  
 Para remover uma instância nomeada, especifique o nome da instância em vez de "MSSQLSERVER" no exemplo que foi mencionado anteriormente neste tópico.  
  
##  <a name="ClusterInstall"></a> Parâmetros de cluster de failover  
 Antes de instalar uma instância de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , verifique os tópicos a seguir:  
  
-   [Requisitos de hardware e software para a instalação do SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [Considerações sobre segurança para uma instalação do SQL Server](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
-   [Antes de instalar o cluster de failover](../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)  
  
-   [Instâncias de Cluster de Failover do AlwaysOn (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)  
  
    > [!IMPORTANT]  
    >  Todos os comandos de instalação de cluster de failover requerem um cluster do Windows subjacente. Todos os nós que farão parte de um cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem fazer parte do mesmo cluster do Windows.  
  
 Teste e modifique os seguintes scripts de instalação de cluster de failover para que atendam às necessidades de sua organização.  
  
#### <a name="integrated-install-failover-cluster-parameters"></a>Parâmetros de cluster de failover para instalação integrada  
 Use os parâmetros listados na tabela a seguir para desenvolver scripts de linha de comando para a instalação de cluster de failover.  
  
 Para obter mais informações sobre a instalação integrada, consulte [instâncias de Cluster de Failover do AlwaysOn (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
> [!NOTE]  
>  Para adicionar outros nós após a instalação, use a ação [Adicionar Nó](#AddNode) .  
  
|componente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Parâmetro|Detalhes|  
|-----------------------------------------|---------------|-------------|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ACTION<br /><br /> **Necessário**|Necessário para indicar o fluxo de trabalho da instalação do cluster de failover. Valores com suporte:<br /><br /> InstallFailoverCluster|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Necessário somente quando o parâmetro /Q ou /QS é especificado para instalações autônomas.**|Necessário para confirmar a aceitação dos termos de licença.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ENU<br /><br /> **Opcional**|Use esse parâmetro para instalar a versão em inglês do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um sistema operacional localizado quando a mídia de instalação incluir pacotes do idioma inglês e do idioma correspondente ao sistema operacional.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FAILOVERCLUSTERGROUP<br /><br /> **Opcional**|Especifica o nome do grupo de recursos a ser usado para o cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Pode ser o nome de um grupo de clusters existente ou o nome de um novo grupo de recursos.<br /><br /> Valor padrão:<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (\<InstanceName>)|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/*UpdateEnabled*<br /><br /> **Opcional**|Especifique se a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve descobrir e incluir atualizações de produto. Os valores válidos são True e False ou 1 e 0. Por padrão, a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluirá as atualizações localizadas.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/*UpdateSource*<br /><br /> **Opcional**|Especifique o local em que a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] obterá as atualizações de produto. Os valores válidos são “MU” para pesquisar [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, um caminho de pasta válido, um caminho relativo, por exemplo .\MyUpdates ou um compartilhamento UNC. Por padrão, a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pesquisará o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update ou um serviço Windows Update por meio do Windows Server Update Services.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/CONFIGURATIONFILE<br /><br /> **Opcional**|Especifica o [ConfigurationFile](install-sql-server-using-a-configuration-file.md) a ser usado.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ERRORREPORTING<br /><br /> **Opcional**|Especifica o relatório de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte a [Política de Privacidade do Serviço de Relatório de Erros da Microsoft](https://go.microsoft.com/fwlink/?LinkID=72173). Valores com suporte:<br /><br /> 1=habilitado<br /><br /> 0=desabilitado|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FEATURES<br /><br /> **Necessário**|Especifica os [componentes](#Feature) a serem instalados.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/HELP, H, ?<br /><br /> **Opcional**|Exibe as opções de uso dos parâmetros.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INDICATEPROGRESS<br /><br /> **Opcional**|Especifica que o arquivo de log de Instalação detalhado será conectado ao console.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTALLSHAREDDIR<br /><br /> **Opcional**|Especifica um diretório de instalação não padrão para componentes compartilhados de 64 bits.<br /><br /> O padrão é % arquivos de programas %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> Não é possível definir como % arquivos de programas(x86%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTALLSHAREDWOWDIR<br /><br /> **Opcional**|Especifica um diretório de instalação não padrão para componentes compartilhados de 32 bits. Com suporte apenas em sistemas de 64 bits.<br /><br /> O padrão é % programas(x86%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> Não pode ser definido como % arquivos de programas %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTANCEDIR<br /><br /> **Opcional**|Especifica um diretório de instalação não padrão para componentes específicos à instância.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTANCEID<br /><br /> **Opcional**|Especifica um valor não padrão para uma [InstanceID](#InstanceID).|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTANCENAME<br /><br /> **Necessário**|Especifica um nome de instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Para obter mais informações, consulte [Instance Configuration](../../sql-server/install/instance-configuration.md).|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/PID<br /><br /> **Opcional**|Especifica a chave do produto (Product Key) da edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se esse parâmetro não for especificado, a versão Evaluation será usada.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/Q<br /><br /> **Opcional**|Especifica que a Instalação é executada em modo silencioso sem nenhuma interface do usuário. Isso é usado para instalações autônomas.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/QS<br /><br /> **Opcional**|Especifica que a Instalação é executada e mostra o andamento por meio da interface do usuário, mas não aceita nenhuma entrada nem mostra nenhuma mensagem de erro.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/SQMREPORTING<br /><br /> **Opcional**|Especifica o relatório de uso de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Para obter mais informações, consulte a [Política de Privacidade do Serviço de Relatório de Erros da Microsoft](https://go.microsoft.com/fwlink/?LinkID=72173). Valores com suporte:<br /><br /> 1=habilitado<br /><br /> 0=desabilitado|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/HIDECONSOLE<br /><br /> **Opcional**|Especifica se a janela do console deve ser ocultada ou fechada.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FAILOVERCLUSTERDISKS<br /><br /> **Opcional**|Especifica a lista de discos compartilhados a serem incluídos no grupo de recursos de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Valor padrão:<br /><br /> A primeira unidade é usada como a unidade padrão para todos os bancos de dados.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FAILOVERCLUSTERIPADDRESSES<br /><br /> **Necessário**|Especifica um endereço IP codificado. As codificações são separadas por ponto-e-vírgula (;) e seguem o formato \<IP Type>;\<address>;\<network name>;\<subnet mask>. Os tipos IP com suporte incluem DHCP, IPv4 e IPv6.<br />Você pode especificar vários endereços IP de cluster de failover com um espaço entre eles. Consulte os exemplos a seguir:<br /><br /> FAILOVERCLUSTERIPADDRESSES=DEFAULT<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;172.16.0.0;ClusterNetwork1;172.31.255.255<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;2001:db8:23:1002:20f:1fff:feff:b3a3;ClusterNetwork1|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FAILOVERCLUSTERNETWORKNAME<br /><br /> **Necessário**|Especifica o nome de rede do novo cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse nome é usado para identificar a nova instância de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na rede.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent|/AGTSVCACCOUNT<br /><br /> **Necessário**|Especifica a conta do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent|/AGTSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha da conta do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASBACKUPDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de backup do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores padrão:<br /><br /> Para o modo WOW em 64 bits: % programas(x86\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\olap\backup.<br /><br /> Para todas as outras instalações: % arquivos de programas %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\olap\backup.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCOLLATION<br /><br /> **Opcional**|Especifica a configuração de ordenação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].<br /><br /> Valor padrão:<br /><br /> -Latin1_General_CI_AS|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCONFIGDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de configuração do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores padrão:<br /><br /> Para o modo WOW em 64 bits: % programas(x86\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\olap\config.<br /><br /> Para todas as outras instalações: % Program Files %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\olap\config.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASDATADIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores padrão:<br /><br /> Para o modo WOW em 64 bits: % programas(x86\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\OLAP\Data.<br /><br /> Para todas as outras instalações: % Program Files %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\OLAP\Data.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASLOGDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de log do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores padrão:<br /><br /> Para o modo WOW em 64 bits: % programas(x86\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\olap\log.<br /><br /> Para todas as outras instalações: % Program Files %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\olap\log.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSYSADMINACCOUNTS<br /><br /> **Necessário**|Especifica as credenciais de administrador do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASTEMPDIR<br /><br /> **Opcional**|Especifica o diretório de arquivos temporários do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores padrão:<br /><br /> Para o modo WOW em 64 bits: % programas(x86\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\olap\temp.<br /><br /> Para todas as outras instalações: % Program Files %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\olap\temp.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASPROVIDERMSOLAP<br /><br /> **Opcional**|Especifica se o provedor MSOLAP pode ser executado no processo. Valor padrão:<br /><br /> 1=habilitado|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSERVERMODE<br /><br /> **Opcional**|Especifica o modo de servidor da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Os valores válidos em um cenário de cluster são MULTIDIMENSIONAL ou TABULAR. **ASSERVERMODE** diferencia maiúsculas de minúsculas. Todos os valores devem ser expressos em maiúsculas. Para obter mais informações sobre os valores válidos, consulte Instalar o Analysis Services em modo Tabular.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/INSTALLSQLDATADIR<br /><br /> **Necessário**|Especifica o diretório de dados dos arquivos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> O diretório de dados deve ser especificado em um disco de cluster compartilhado.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **Necessário quando /SECURITYMODE=SQL**|Especifica a senha da conta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sa.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SECURITYMODE<br /><br /> **Opcional**|Especifica o modo de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se esse parâmetro não for fornecido, apenas o modo de autenticação do Windows terá suporte. Valor com suporte:<br /><br /> SQL|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLBACKUPDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de backup. Valor padrão:<br /><br /> \<InstallSQLDataDir > \ \<SQLInstanceID > \MSSQL\Backup.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **Opcional**|Especifica as configurações de ordenação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> O valor padrão baseia-se na localidade do sistema operacional Windows. Para obter mais informações, veja [Configurações de ordenação na Instalação](https://msdn.microsoft.com/library/ms143508%28v=sql.105%29.aspx).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **Necessário**|Especifica a conta de inicialização do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha de SQLSVCACCOUNT.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **Necessário**|Use este parâmetro para provisionar logons para serem membros da função sysadmin.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de dados do tempdb. Valor padrão:<br /><br /> \<InstallSQLDataDir > \ \<SQLInstanceID > \Mssql\Data.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de log do tempdb. Valor padrão:<br /><br /> \<InstallSQLDataDir > \ \<SQLInstanceID > \Mssql\Data.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de dados de bancos de dados do usuário. Valor padrão:<br /><br /> \<InstallSQLDataDir > \ \<SQLInstanceID > \Mssql\Data.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBLOGDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de log de bancos de dados do usuário. Valor padrão:<br /><br /> \<InstallSQLDataDir > \ \<SQLInstanceID > \Mssql\Data.|  
|FILESTREAM|/FILESTREAMLEVEL<br /><br /> **Opcional**|Especifica o nível de acesso para o recurso FILESTREAM. Valores com suporte:<br /><br /> 0 =Desabilitar o suporte ao FILESTREAM desta instância. (Valor padrão)<br /><br /> 1=Habilitar FILESTREAM para o acesso de [!INCLUDE[tsql](../../includes/tsql-md.md)] .<br /><br /> 2=Habilitar FILESTREAM para o acesso de [!INCLUDE[tsql](../../includes/tsql-md.md)] e o acesso de fluxo de E/S de arquivo. (Inválido para cenários de cluster)<br /><br /> 3=Permitir que clientes remotos tenham acesso de streaming a dados FILESTREAM.|  
|FILESTREAM|/FILESTREAMSHARENAME<br /><br /> **Opcional**<br /><br /> **Necessário quando FILESTREAMLEVEL for maior do que 1.**|Especifica o nome do compartilhamento do Windows no qual os dados FILESTREAM serão armazenados.|  
|Texto completo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FTSVCACCOUNT<br /><br /> **Opcional**|Especifica a conta do serviço iniciador de filtro de texto completo.<br /><br /> Esse parâmetro é ignorado no [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]. ServiceSID será usado para ajudar a proteger a comunicação entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o Daemon de Filtro de Texto Completo.<br /><br /> Se os valores não forem fornecidos, o Serviço Iniciador de Filtro de Texto Completo será desabilitado. Você deve usar o Gerenciador de Controle do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para alterar a conta de serviço e habilitar a funcionalidade de texto completo. Valor padrão:<br /><br /> Conta Serviço Local|  
|Texto completo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FTSVCPASSWORD<br /><br /> **Opcional**|Especifica a senha do serviço iniciador de filtro de texto completo.<br /><br /> Esse parâmetro é ignorado no [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)].|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **Necessário**|Especifica a conta do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Valor padrão:<br /><br /> NT AUTHORITY\NETWORK SERVICE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **Opcional**|Especifica o modo de [inicialização](#Accounts) do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Opcional**|Especifica o modo de Instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT<br /><br /> **Necessário**|Especifica a conta de inicialização do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha da conta de inicialização do serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCStartupType<br /><br /> **Opcional**|Especifica o modo de [inicialização](#Accounts) do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
 <sup>1</sup> é recomendável que você use o SID de serviço em vez de grupos de domínio.  
  
##### <a name="additional-notes"></a>Observações adicionais:  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] são os únicos componentes com suporte a cluster. Os outros recursos não oferecem suporte a cluster e não têm alta disponibilidade por meio de failover.  
  
###### <a name="sample-syntax"></a>Sintaxe de exemplo:  
 Para instalar uma instância de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de nó único com o [!INCLUDE[ssDE](../../includes/ssde-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], a instância padrão.  
  
```  
setup.exe /q /ACTION=InstallFailoverCluster /InstanceName=MSSQLSERVER /INDICATEPROGRESS /ASSYSADMINACCOUNTS="<DomainName\UserName>" /ASDATADIR=<Drive>:\OLAP\Data /ASLOGDIR=<Drive>:\OLAP\Log /ASBACKUPDIR=<Drive>:\OLAP\Backup /ASCONFIGDIR=<Drive>:\OLAP\Config /ASTEMPDIR=<Drive>:\OLAP\Temp /FAILOVERCLUSTERDISKS="<Cluster Disk Resource Name - for example, 'Disk S:'" /FAILOVERCLUSTERNETWORKNAME="<Insert Network Name>" /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;Cluster Network;xxx.xxx.xxx.x" /FAILOVERCLUSTERGROUP="MSSQLSERVER" /Features=AS,SQL /ASSVCACCOUNT="<DomainName\UserName>" /ASSVCPASSWORD="xxxxxxxxxxx" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="xxxxxxxxxxx" /INSTALLSQLDATADIR="<Drive>:\<Path>\MSSQLSERVER" /SQLCOLLATION="SQL_Latin1_General_CP1_CS_AS" /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx" /SQLSYSADMINACCOUNTS="<DomainName\UserName> /IACCEPTSQLSERVERLICENSETERMS  
```  
  
#### <a name="prepare-failover-cluster-parameters"></a>Parâmetros de preparação de cluster de failover  
 Use os parâmetros listados na tabela a seguir para desenvolver scripts de linha de comando para a preparação do cluster de failover. Essa é a primeira etapa da instalação avançada de cluster, na qual você deve preparar as instâncias de cluster de failover em todos os nós do cluster de failover. Para obter mais informações, consulte [Instâncias do Cluster de Failover do AlwaysOn (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
|componente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Parâmetro|Descrição|  
|-----------------------------------------|---------------|-----------------|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ACTION<br /><br /> **Necessário**|Necessário para indicar o fluxo de trabalho da preparação do cluster de failover. Valores com suporte:<br /><br /> PrepareFailoverCluster|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Necessário somente quando o parâmetro /Q ou /QS é especificado para instalações autônomas.**|Necessário para confirmar a aceitação dos termos de licença.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ENU<br /><br /> **Opcional**|Use esse parâmetro para instalar a versão em inglês do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um sistema operacional localizado quando a mídia de instalação incluir pacotes do idioma inglês e do idioma correspondente ao sistema operacional.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/*UpdateEnabled*<br /><br /> **Opcional**|Especifique se a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve descobrir e incluir atualizações de produto. Os valores válidos são True e False ou 1 e 0. Por padrão, a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluirá as atualizações localizadas.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/*UpdateSource*<br /><br /> **Opcional**|Especifique o local em que a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] obterá as atualizações de produto. Os valores válidos são “MU” para pesquisar [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, um caminho de pasta válido, um caminho relativo, por exemplo .\MyUpdates ou um compartilhamento UNC. Por padrão, a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pesquisará o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update ou um serviço Windows Update por meio do Windows Server Update Services.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/CONFIGURATIONFILE<br /><br /> **Opcional**|Especifica o [ConfigurationFile](install-sql-server-using-a-configuration-file.md) a ser usado.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ERRORREPORTING<br /><br /> **Opcional**|Especifica o relatório de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Para obter mais informações, consulte a [Política de Privacidade do Serviço de Relatório de Erros da Microsoft](https://go.microsoft.com/fwlink/?LinkID=72173). Valores com suporte:<br /><br /> 1=habilitado<br /><br /> 0=desabilitado|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FEATURES<br /><br /> **Necessário**|Especifica os [componentes](#Feature) a serem instalados.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/HELP, H, ?<br /><br /> **Opcional**|Exibe as opções de uso dos parâmetros.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INDICATEPROGRESS<br /><br /> **Opcional**|Especifica que o arquivo de log de Instalação detalhado será conectado ao console.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTALLSHAREDDIR<br /><br /> **Opcional**|Especifica um diretório de instalação não padrão para componentes compartilhados de 64 bits.<br /><br /> O padrão é % arquivos de programas %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> Não é possível definir como % arquivos de programas(x86%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTALLSHAREDWOWDIR<br /><br /> **Opcional**|Especifica um diretório de instalação não padrão para componentes compartilhados de 32 bits. Com suporte apenas em sistemas de 64 bits.<br /><br /> O padrão é % programas(x86%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> Não pode ser definido como % arquivos de programas %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTANCEDIR<br /><br /> **Opcional**|Especifica um diretório de instalação não padrão para componentes específicos à instância.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTANCEID<br /><br /> **Opcional**|Especifica um valor não padrão para uma [InstanceID](#InstanceID).|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTANCENAME<br /><br /> **Necessário**|Especifica um nome de instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Para obter mais informações, consulte [Instance Configuration](../../sql-server/install/instance-configuration.md).|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/PID<br /><br /> **Opcional**|Especifica a chave do produto (Product Key) da edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se esse parâmetro não for especificado,<br /><br /> a versão Evaluation será usada.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/Q<br /><br /> **Opcional**|Especifica que a Instalação é executada em modo silencioso sem nenhuma interface do usuário. Isso é usado para instalações autônomas.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/QS<br /><br /> **Opcional**|Especifica que a Instalação é executada e mostra o andamento por meio da interface do usuário, mas não aceita nenhuma entrada nem mostra nenhuma mensagem de erro.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/SQMREPORTING<br /><br /> **Opcional**|Especifica o relatório de uso de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Para obter mais informações, consulte a [Política de Privacidade do Serviço de Relatório de Erros da Microsoft](https://go.microsoft.com/fwlink/?LinkID=72173). Valores com suporte:<br /><br /> 1=habilitado<br /><br /> 0=desabilitado|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/HIDECONSOLE<br /><br /> **Opcional**|Especifica se a janela do console é ocultada ou fechada.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent|/AGTSVCACCOUNT<br /><br /> **Necessário**|Especifica a conta do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent|/AGTSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha da conta do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCACCOUNT<br /><br /> **Necessário**|Especifica a conta de serviço do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha do serviço [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **Necessário**|Especifica a conta de inicialização do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha de SQLSVCACCOUNT.|  
|FILESTREAM|/FILESTREAMLEVEL<br /><br /> **Opcional**|Especifica o nível de acesso para o recurso FILESTREAM. Valores com suporte:<br /><br /> 0 =Desabilitar o suporte ao FILESTREAM desta instância. (Valor padrão)<br /><br /> 1=Habilitar FILESTREAM para o acesso de [!INCLUDE[tsql](../../includes/tsql-md.md)] .<br /><br /> 2=Habilitar FILESTREAM para o acesso de [!INCLUDE[tsql](../../includes/tsql-md.md)] e o acesso de fluxo de E/S de arquivo. (Inválido para cenários de cluster)<br /><br /> 3=Permitir que clientes remotos tenham acesso de streaming a dados FILESTREAM.|  
|FILESTREAM|/FILESTREAMSHARENAME<br /><br /> **Opcional**<br /><br /> **Obrigatório** quando FILESTREAMLEVEL é maior que 1.|Especifica o nome do compartilhamento do Windows no qual os dados FILESTREAM serão armazenados.|  
|Texto completo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FTSVCACCOUNT<br /><br /> **Opcional**|Especifica a conta do serviço iniciador de filtro de texto completo.<br /><br /> Esse parâmetro é ignorado no [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]. ServiceSID será usado para ajudar a proteger a comunicação entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o Daemon de Filtro de Texto Completo.<br /><br /> Se os valores não forem fornecidos, o Serviço Iniciador de Filtro de Texto Completo será desabilitado. Você deve usar o Gerenciador de Controle do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para alterar a conta de serviço e habilitar a funcionalidade de texto completo. Valor padrão:<br /><br /> Conta Serviço Local|  
|Texto completo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FTSVCPASSWORD<br /><br /> **Opcional**|Especifica a senha do serviço iniciador de filtro de texto completo.<br /><br /> Esse parâmetro é ignorado no [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)].|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **Necessário**|Especifica a conta do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Valor padrão:<br /><br /> NT AUTHORITY\NETWORK SERVICE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **Opcional**|Especifica o modo de [inicialização](#Accounts) do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Disponível apenas no modo Somente arquivos.**|Especifica o modo de Instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT<br /><br /> **Necessário**|Especifica a conta de inicialização do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha da conta de inicialização do serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCStartupType<br /><br /> **Opcional**|Especifica o modo de [inicialização](#Accounts) do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
 <sup>1</sup> é recomendável que você use o SID de serviço em vez de grupos de domínio.  
  
###### <a name="sample-syntax"></a>Sintaxe de exemplo:  
 Para executar a etapa de "Preparação" de um cenário de instalação avançada de cluster de failover para o [!INCLUDE[ssDE](../../includes/ssde-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 No prompt de comando, execute o seguinte comando para preparar uma instância padrão:  
  
```  
setup.exe /q /ACTION=PrepareFailoverCluster /InstanceName=MSSQLSERVER /Features=AS,SQL /INDICATEPROGRESS /ASSVCACCOUNT="<DomainName\UserName>" /ASSVCPASSWORD="xxxxxxxxxxx" /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="xxxxxxxxxxx" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
 No prompt de comando, execute o seguinte comando para preparar uma instância nomeada:  
  
```  
setup.exe /q /ACTION=PrepareFailoverCluster /InstanceName="<Insert Instance name>" /Features=AS,SQL /INDICATEPROGRESS /ASSVCACCOUNT="<DomainName\UserName>" /ASSVCPASSWORD="xxxxxxxxxxx" /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="xxxxxxxxxxx" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
#### <a name="complete-failover-cluster-parameters"></a>Parâmetros de conclusão de cluster de failover  
 Use os parâmetros listados na tabela a seguir para desenvolver scripts de linha de comando para a conclusão do cluster de failover. Esta é a segunda etapa na opção de instalação avançada de cluster de failover. Depois de executar a preparação em todos os nós de cluster de failover, execute esse comando no nó que possui os discos compartilhados. Para obter mais informações, consulte [Instâncias do Cluster de Failover do AlwaysOn (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
|componente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Parâmetro|Descrição|  
|-----------------------------------------|---------------|-----------------|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ACTION<br /><br /> **Necessário**|Necessário para indicar o fluxo de trabalho da conclusão do cluster de failover. Valores com suporte:<br /><br /> CompleteFailoverCluster|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ENU<br /><br /> **Opcional**|Use esse parâmetro para instalar a versão em inglês do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um sistema operacional localizado quando a mídia de instalação incluir pacotes do idioma inglês e do idioma correspondente ao sistema operacional.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FAILOVERCLUSTERGROUP<br /><br /> **Opcional**|Especifica o nome do grupo de recursos a ser usado para o cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Pode ser o nome de um grupo de clusters existente ou o nome de um novo grupo de recursos.<br /><br /> Valor padrão:<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (\<InstanceName>)|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/CONFIGURATIONFILE<br /><br /> **Opcional**|Especifica o [ConfigurationFile](install-sql-server-using-a-configuration-file.md) a ser usado.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ERRORREPORTING<br /><br /> **Opcional**|Especifica o relatório de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Para obter mais informações, consulte a [Política de Privacidade do Serviço de Relatório de Erros da Microsoft](https://go.microsoft.com/fwlink/?LinkID=72173). Valores com suporte:<br /><br /> 1=habilitado<br /><br /> 0=desabilitado|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/HELP, H, ?<br /><br /> **Opcional**|Exibe as opções de uso dos parâmetros.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INDICATEPROGRESS<br /><br /> **Opcional**|Especifica que o arquivo de log de Instalação detalhado será conectado ao console.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTANCENAME<br /><br /> **Necessário**|Especifica um nome de instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Para obter mais informações, consulte [Instance Configuration](../../sql-server/install/instance-configuration.md).|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/PID<br /><br /> **Opcional**|Especifica a chave do produto (Product Key) da edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se esse parâmetro não for especificado, a versão Evaluation será usada.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/Q<br /><br /> **Opcional**|Especifica que a Instalação é executada em modo silencioso sem nenhuma interface do usuário. Isso é usado para instalações autônomas.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/QS<br /><br /> **Opcional**|Especifica que a Instalação é executada e mostra o andamento por meio da interface do usuário, mas não aceita nenhuma entrada nem mostra nenhuma mensagem de erro.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/SQMREPORTING<br /><br /> **Opcional**|Especifica o relatório de uso de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Para obter mais informações, consulte a [Política de Privacidade do Serviço de Relatório de Erros da Microsoft](https://go.microsoft.com/fwlink/?LinkID=72173). Valores com suporte:<br /><br /> 1=habilitado<br /><br /> 0=desabilitado|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/HIDECONSOLE<br /><br /> **Opcional**|Especifica se a janela do console é ocultada ou fechada.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FAILOVERCLUSTERDISKS<br /><br /> **Opcional**|Especifica a lista de discos compartilhados a serem incluídos no grupo de recursos de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Valor padrão:<br /><br /> A primeira unidade é usada como a unidade padrão para todos os bancos de dados.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FAILOVERCLUSTERIPADDRESSES<br /><br /> **Necessário**|Especifica um endereço IP codificado. As codificações são separadas por ponto-e-vírgula (;) e seguem o formato \<IP Type>;\<address>;\<network name>;\<subnet mask>. Os tipos IP com suporte incluem DHCP, IPv4 e IPv6.<br />Você pode especificar vários endereços IP de cluster de failover com um espaço entre eles. Consulte os exemplos a seguir:<br /><br /> FAILOVERCLUSTERIPADDRESSES=DEFAULT<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;172.16.0.0;ClusterNetwork1;172.31.255.255<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;2001:db8:23:1002:20f:1fff:feff:b3a3;ClusterNetwork1|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FAILOVERCLUSTERNETWORKNAME<br /><br /> **Necessário**|Especifica o nome de rede do novo cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse nome é usado para identificar a nova instância de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na rede.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/CONFIRMIPDEPENDENCYCHANGE|Indica o consentimento para definir a dependência de recurso de endereço IP como OR para clusters de failover de várias sub-redes. Para obter mais informações, consulte [Criar um novo cluster de failover do SQL Server &#40;Instalação&#41;](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md). Valores com suporte:<br /><br /> 0 = False (padrão)<br /><br /> 1 = True|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASBACKUPDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de backup do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores padrão:<br /><br /> Para o modo WOW em 64 bits: % programas(x86\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\olap\backup.<br /><br /> Para todas as outras instalações: % arquivos de programas %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\olap\backup.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCOLLATION<br /><br /> **Opcional**|Especifica a configuração de ordenação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Valor padrão:<br /><br /> Latin1_General_CI_AS|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCONFIGDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de configuração do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores padrão:<br /><br /> Para o modo WOW em 64 bits: % programas(x86\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\olap\config.<br /><br /> Para todas as outras instalações: % Program Files %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\olap\config.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASDATADIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores padrão:<br /><br /> Para o modo WOW em 64 bits: % programas(x86\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\OLAP\Data.<br /><br /> Para todas as outras instalações: % Program Files %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< INSTANCEDIR\>\\< ASInstanceID\>\OLAP\Data.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASLOGDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de log do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores padrão:<br /><br /> Para o modo WOW em 64 bits: % programas(x86\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\ \<INSTANCEDIR >\\< ASInstanceID\>\olap\log.<br /><br /> Para todas as outras instalações: % Program Files %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\ \<INSTANCEDIR >\\< ASInstanceID\>\olap\log.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSERVERMODE<br /><br /> **Opcional**|Especifica o modo de servidor da instância do Analysis Services. Os valores válidos em um cenário de cluster são MULTIDIMENSIONAL ou TABULAR. **ASSERVERMODE** diferencia maiúsculas de minúsculas. Todos os valores devem ser expressos em maiúsculas. Para obter mais informações sobre os valores válidos, consulte Instalar o Analysis Services em modo Tabular.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSYSADMINACCOUNTS<br /><br /> **Necessário**|Especifica as credenciais de administrador do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASTEMPDIR<br /><br /> **Opcional**|Especifica o diretório de arquivos temporários do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores padrão:<br /><br /> Para o modo WOW em 64 bits: % programas(x86\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\ \<INSTANCEDIR >\\< ASInstanceID\>\olap\temp.<br /><br /> Para todas as outras instalações: % Program Files %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\ \<INSTANCEDIR >\\< ASInstanceID\>\olap\temp.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASPROVIDERMSOLAP<br /><br /> **Opcional**|Especifica se o provedor MSOLAP pode ser executado no processo. Valor padrão:<br /><br /> 1=habilitado|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/INSTALLSQLDATADIR<br /><br /> **Necessário**|Especifica o diretório de dados dos arquivos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> O diretório de dados deve ser especificado em um disco de cluster compartilhado.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **Necessário quando /SECURITYMODE=SQL**|Especifica a senha da conta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sa.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SECURITYMODE<br /><br /> **Opcional**|Especifica o modo de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Se esse parâmetro não for fornecido, apenas o modo de autenticação do Windows terá suporte. Valores com suporte:<br /><br /> SQL|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLBACKUPDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de backup. Valor padrão:<br /><br /> \<InstallSQLDataDir > \ \<SQLInstanceID > \MSSQL\Backup.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **Opcional**|Especifica as configurações de ordenação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> O valor padrão baseia-se na localidade do sistema operacional Windows. Para obter mais informações, veja [Configurações de ordenação na Instalação](https://msdn.microsoft.com/library/ms143508%28v=sql.105%29.aspx).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **Necessário**|Use este parâmetro para provisionar logons para serem membros da função sysadmin.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de dados do tempdb. Valor padrão:<br /><br /> \<InstallSQLDataDir > \ \<SQLInstanceID > \MSSQL\Data.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos l para tempdb. Valor padrão:<br /><br /> \<InstallSQLDataDir > \ \<SQLInstanceID > \Mssql\Data.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de dados de bancos de dados do usuário. Valor padrão:<br /><br /> \<InstallSQLDataDir > \ \<SQLInstanceID > \Mssql\Data.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBLOGDIR<br /><br /> **Opcional**|Especifica o diretório dos arquivos de log de bancos de dados do usuário. Valor padrão:<br /><br /> \<InstallSQLDataDir > \ \<SQLInstanceID > \Mssql\Data.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Disponível no modo Somente arquivos.**|Especifica o modo de Instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
###### <a name="sample-syntax"></a>Sintaxe de exemplo:  
 Para executar a etapa de "Conclusão" de um cenário de instalação avançada de cluster de failover para o [!INCLUDE[ssDE](../../includes/ssde-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Execute o comando a seguir no computador que será o nó ativo no cluster de failover para torná-lo utilizável. Você deve executar a ação "CompleteFailoverCluster" no nó que possui o disco compartilhado no cluster de failover do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 No prompt de comando, execute o comando a seguir para concluir a instalação do cluster de failover para uma instância padrão:  
  
```  
setup.exe /q /ACTION=CompleteFailoverCluster /InstanceName=MSSQLSERVER /INDICATEPROGRESS /ASSYSADMINACCOUNTS="<DomainName\Username>" /ASDATADIR=<Drive>:\OLAP\Data /ASLOGDIR=<Drive>:\OLAP\Log /ASBACKUPDIR=<Drive>:\OLAP\Backup /ASCONFIGDIR=<Drive>:\OLAP\Config /ASTEMPDIR=<Drive>:\OLAP\Temp /FAILOVERCLUSTERDISKS="<Cluster Disk Resource Name - for example, 'Disk S:'>:" /FAILOVERCLUSTERNETWORKNAME="<Insert FOI Network Name>" /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;Cluster Network;xxx.xxx.xxx.x" /FAILOVERCLUSTERGROUP="MSSQLSERVER" /INSTALLSQLDATADIR="<Drive>:\<Path>\MSSQLSERVER" /SQLCOLLATION="SQL_Latin1_General_CP1_CS_AS" /SQLSYSADMINACCOUNTS="<DomainName\UserName>"  
```  
  
 No prompt de comando, execute o comando a seguir para concluir a instalação do cluster de failover para uma instância nomeada:  
  
```  
setup.exe /q /ACTION=CompleteFailoverCluster /InstanceName="<Insert Instance Name>" /INDICATEPROGRESS /ASSYSADMINACCOUNTS="<DomainName\UserName>" /ASDATADIR=<Drive>:\KATMAI\Data /ASLOGDIR=<drive>:\KATMAI\Log /ASBACKUPDIR=<Drive>:\KATMAI\Backup /ASCONFIGDIR=<Drive>:\KATMAI\Config /ASTEMPDIR=<Drive>:\KATMAI\Temp /FAILOVERCLUSTERDISKS="<Cluster Disk Resource Name - for example, 'Disk S:'>" /FAILOVERCLUSTERNETWORKNAME="CompNamedFOI" /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;ClusterNetwork1;xxx.xxx.xxx.x" /FAILOVERCLUSTERGROUP="<Insert New Group Name>" /INSTALLSQLDATADIR="<Drive>:\<Path>\MSSQLSERVER_KATMAI" /SQLCOLLATION="SQL_Latin1_General_CP1_CS_AS" /SQLSYSADMINACCOUNTS="<DomainName\Username>"  
```  
  
#### <a name="upgrade-failover-cluster-parameters"></a>Parâmetros de atualização de cluster de failover  
 Use os parâmetros listados na tabela a seguir para desenvolver scripts de linha de comando para a atualização de cluster de failover. Para obter mais informações, consulte [atualizar uma instância de Cluster de Failover do SQL Server &#40;instalação&#41; ](../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md) e [instâncias de Cluster de Failover do AlwaysOn (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
|componente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Parâmetro|Descrição|  
|-----------------------------------------|---------------|-----------------|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ACTION<br /><br /> **Necessário**|Necessário para indicar o fluxo de trabalho da instalação. Valores com suporte:<br /><br /> UPGRADE|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Necessário somente quando o parâmetro /Q ou /QS é especificado para instalações autônomas.**|Necessário para confirmar a aceitação dos termos de licença.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ENU<br /><br /> **Opcional**|Use esse parâmetro para instalar a versão em inglês do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um sistema operacional localizado quando a mídia de instalação incluir pacotes do idioma inglês e do idioma correspondente ao sistema operacional.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/*UpdateEnabled*<br /><br /> **Opcional**|Especifique se a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve descobrir e incluir atualizações de produto. Os valores válidos são True e False ou 1 e 0. Por padrão, a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluirá as atualizações localizadas.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/*UpdateSource*<br /><br /> **Opcional**|Especifique o local em que a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] obterá as atualizações de produto. Os valores válidos são “MU” para pesquisar [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, um caminho de pasta válido, um caminho relativo, por exemplo .\MyUpdates ou um compartilhamento UNC. Por padrão, a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pesquisará o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update ou um serviço Windows Update por meio do Windows Server Update Services.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/CONFIGURATIONFILE<br /><br /> **Opcional**|Especifica o [ConfigurationFile](install-sql-server-using-a-configuration-file.md) a ser usado.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ERRORREPORTING<br /><br /> **Opcional**|Especifica o relatório de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Para obter mais informações, consulte a [Política de Privacidade do Serviço de Relatório de Erros da Microsoft](https://go.microsoft.com/fwlink/?LinkID=72173). Valores com suporte:<br /><br /> 1=habilitado<br /><br /> 0=desabilitado|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/HELP, H, ?<br /><br /> **Opcional**|Exibe as opções de uso dos parâmetros.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INDICATEPROGRESS<br /><br /> **Opcional**|Especifica que o arquivo de log de Instalação detalhado será conectado ao console.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ INSTANCEDIR<br /><br /> **Opcional**|Especifica um diretório de instalação não padrão para componentes compartilhados.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTANCEID<br /><br /> **Necessário ao atualizar do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou superior.**<br /><br /> **Opcional ao atualizar do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]**|Especifica um valor não padrão para uma [InstanceID](#InstanceID).|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTANCENAME<br /><br /> **Necessário**|Especifica um nome de instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Para obter mais informações, consulte [Instance Configuration](../../sql-server/install/instance-configuration.md).|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/PID<br /><br /> **Opcional**|Especifica a chave do produto (Product Key) da edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se esse parâmetro não for especificado, a versão Evaluation será usada.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/Q<br /><br /> **Opcional**|Especifica que a Instalação é executada em modo silencioso sem nenhuma interface do usuário. Isso é usado para instalações autônomas.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/SQMREPORTING<br /><br /> **Opcional**|Especifica o relatório de uso de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Para obter mais informações, consulte a [Política de Privacidade do Serviço de Relatório de Erros da Microsoft](https://go.microsoft.com/fwlink/?LinkID=72173). Valores com suporte:<br /><br /> 0=desabilitado<br /><br /> 1=habilitado|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/HIDECONSOLE<br /><br /> **Opcional**|Especifica se a janela do console é ocultada ou fechada.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FAILOVERCLUSTERROLLOWNERSHIP|Especifica o [comportamento de failover](#RollOwnership) durante a atualização.|  
|Serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/BROWSERSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica o modo de [inicialização](#Accounts) do serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Valores com suporte:<br /><br /> Automatic<br /><br /> Desabilitado<br /><br /> Manual|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Texto completo|/FTUPGRADEOPTION<br /><br /> **Opcional**|Especifica a opção de atualização do catálogo de Texto Completo. Valores com suporte:<br /><br /> REBUILD<br /><br /> RESET<br /><br /> IMPORT|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **Necessário**|Especifica a conta do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Valor padrão:<br /><br /> NT AUTHORITY\NETWORK SERVICE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **Opcional**|Especifica o modo de [inicialização](#Accounts) do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSUPGRADEDATABASEACCOUNT<br /><br /> **Opcional**|A propriedade só é usada ao atualizar um servidor de relatório no modo SharePoint que seja da versão 2008 R2 ou anterior. As demais operações de atualização são executadas para servidores de relatório que usam a arquitetura mais antiga do modo do SharePoint, que foi modificada no SQL Server 2012 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Se essa opção não estiver incluída com a instalação de linha de comando, o serviço de conta padrão para a instância do servidor de relatório antigo será usado. Se esta propriedade for usada, forneça a senha para a conta usando a propriedade **/RSUPGRADEPASSWORD** .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSUPGRADEPASSWORD<br /><br /> **Opcional**|Senha da conta de serviço do Servidor de Relatórios existente.|  
  
####  <a name="AddNode"></a> Parâmetros de adição de nó  
 Use os parâmetros listados na tabela a seguir para desenvolver scripts de linha de comando para AddNode.  
  
|componente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Parâmetro|Descrição|  
|-----------------------------------------|---------------|-----------------|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ACTION<br /><br /> **Necessário**|Necessário para indicar o fluxo de trabalho de AddNode. Valor com suporte:<br /><br /> AddNode|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Necessário somente quando o parâmetro /Q ou /QS é especificado para instalações autônomas.**|Necessário para confirmar a aceitação dos termos de licença.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ENU<br /><br /> **Opcional**|Use esse parâmetro para instalar a versão em inglês do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um sistema operacional localizado quando a mídia de instalação incluir pacotes do idioma inglês e do idioma correspondente ao sistema operacional.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/*UpdateEnabled*<br /><br /> **Opcional**|Especifique se a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve descobrir e incluir atualizações de produto. Os valores válidos são True e False ou 1 e 0. Por padrão, a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluirá as atualizações localizadas.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/*UpdateSource*<br /><br /> **Opcional**|Especifique o local em que a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] obterá as atualizações de produto. Os valores válidos são “MU” para pesquisar [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, um caminho de pasta válido, um caminho relativo, por exemplo .\MyUpdates ou um compartilhamento UNC. Por padrão, a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pesquisará o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update ou um serviço Windows Update por meio do Windows Server Update Services.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/CONFIGURATIONFILE<br /><br /> **Opcional**|Especifica o [ConfigurationFile](install-sql-server-using-a-configuration-file.md) a ser usado.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/HELP, H, ?<br /><br /> **Opcional**|Exibe as opções de uso dos parâmetros.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INDICATEPROGRESS<br /><br /> **Opcional**|Especifica que o arquivo de log de Instalação detalhado será conectado ao console.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTANCENAME<br /><br /> **Necessário**|Especifica um nome de instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Para obter mais informações, consulte [Instance Configuration](../../sql-server/install/instance-configuration.md).|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/PID<br /><br /> **Opcional**|Especifica a chave do produto (Product Key) da edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se esse parâmetro não for especificado, a versão Evaluation será usada.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/Q<br /><br /> **Opcional**|Especifica que a Instalação é executada em modo silencioso sem nenhuma interface do usuário. Isso é usado para instalações autônomas.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/QS<br /><br /> **Opcional**|Especifica que a Instalação é executada e mostra o andamento por meio da interface do usuário, mas não aceita nenhuma entrada nem mostra nenhuma mensagem de erro.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/HIDECONSOLE<br /><br /> **Opcional**|Especifica se a janela do console é ocultada ou fechada.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/FAILOVERCLUSTERIPADDRESSES<br /><br /> **Necessário**|Especifica um endereço IP codificado. As codificações são separadas por ponto-e-vírgula (;) e seguem o formato \<IP Type>;\<address>;\<network name>;\<subnet mask>. Os tipos IP com suporte incluem DHCP, IPv4 e IPv6.<br />Você pode especificar vários endereços IP de cluster de failover com um espaço entre eles. Consulte os exemplos a seguir:<br /><br /> FAILOVERCLUSTERIPADDRESSES=DEFAULT<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;172.16.0.0;ClusterNetwork1;172.31.255.255<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;2001:db8:23:1002:20f:1fff:feff:b3a3;ClusterNetwork1<br /><br /> <br /><br /> Para obter mais informações, consulte [Adicionar ou remover nós em um cluster de failover do SQL Server &#40;Instalação&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/CONFIRMIPDEPENDENCYCHANGE<br /><br /> **Necessário**|Indica o consentimento para definir a dependência de recurso de endereço IP como OR para clusters de failover de várias sub-redes. Para obter mais informações, consulte [Adicionar ou remover nós em um cluster de failover do SQL Server &#40;Instalação&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md). Valores com suporte:<br /><br /> 0 = False (padrão)<br /><br /> 1 = True|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent|/AGTSVCACCOUNT<br /><br /> **Necessário**|Especifica a conta do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent|/AGTSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha da conta do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCACCOUNT<br /><br /> **Necessário**|Especifica a conta de serviço do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha do serviço [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **Necessário**|Especifica a conta de inicialização do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha de SQLSVCACCOUNT.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Disponível no modo Somente arquivos**|Especifica o modo de Instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [Necessário](#Accounts)|Especifica a senha da conta de inicialização do serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
  
##### <a name="additional-notes"></a>Observações adicionais:  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] são os únicos componentes com suporte a cluster. Os outros recursos não oferecem suporte a cluster e não têm alta disponibilidade por meio de failover.  
  
###### <a name="sample-syntax"></a>Sintaxe de exemplo:  
 Para adicionar um nó a uma instância de cluster de failover existente com o [!INCLUDE[ssDE](../../includes/ssde-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
```  
setup.exe /q /ACTION=AddNode /INSTANCENAME="<Insert Instance Name>" /SQLSVCACCOUNT="<SQL account that is used on other nodes>" /SQLSVCPASSWORD="<password for SQL account>" /AGTSVCACCOUNT="<SQL Server Agent account that is used on other nodes>", /AGTSVCPASSWORD="<SQL Server Agent account password>" /ASSVCACCOUNT="<AS account that is used on other nodes>" /ASSVCPASSWORD="<password for AS account>" /INDICATEPROGRESS /IACCEPTSQLSERVERLICENSETERMS /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;ClusterNetwork1;xxx.xxx.xxx.x" /CONFIRMIPDEPENDENCYCHANGE=0  
```  
  
#### <a name="remove-node-parameters"></a>Parâmetros de remoção de nó  
 Use os parâmetros listados na tabela a seguir para desenvolver scripts de linha de comando para RemoveNode. Para desinstalar um cluster de failover, execute RemoveNode em cada nó de cluster de failover. Para obter mais informações, consulte [Instâncias do Cluster de Failover do AlwaysOn (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
|componente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Parâmetro|Descrição|  
|-----------------------------------------|---------------|-----------------|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/ACTION<br /><br /> **Necessário**|Necessário para indicar o fluxo de trabalho de RemoveNode. Valor com suporte:<br /><br /> RemoveNode|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/CONFIGURATIONFILE<br /><br /> **Opcional**|Especifica o [ConfigurationFile](install-sql-server-using-a-configuration-file.md) a ser usado.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/HELP, H, ?<br /><br /> **Opcional**|Exibe as opções de uso dos parâmetros.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INDICATEPROGRESS<br /><br /> **Opcional**|Especifica que o arquivo de log de Instalação detalhado será conectado ao console.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/INSTANCENAME<br /><br /> **Necessário**|Especifica um nome de instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Para obter mais informações, consulte [Instance Configuration](../../sql-server/install/instance-configuration.md).|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/Q<br /><br /> **Opcional**|Especifica que a Instalação é executada em modo silencioso sem nenhuma interface do usuário. Isso é usado para instalações autônomas.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/QS<br /><br /> **Opcional**|Especifica que a Instalação é executada e mostra o andamento por meio da interface do usuário, mas não aceita nenhuma entrada nem mostra nenhuma mensagem de erro.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/HIDECONSOLE<br /><br /> **Opcional**|Especifica se a janela do console é ocultada ou fechada.|  
|Controle de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|/CONFIRMIPDEPENDENCYCHANGE<br /><br /> **Necessário**|Indica o consentimento para alterar a definição da dependência de recurso de endereço IP de OR para AND para clusters de failover de várias sub-redes. Para obter mais informações, consulte [Adicionar ou remover nós em um cluster de failover do SQL Server &#40;Instalação&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md). Valores com suporte:<br /><br /> 0 = False (padrão)<br /><br /> 1 = True|  
  
###### <a name="sample-syntax"></a>Sintaxe de exemplo:  
 Para remover um nó de uma instância de cluster de failover existente com o [!INCLUDE[ssDE](../../includes/ssde-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
```  
setup.exe /q /ACTION=RemoveNode /INSTANCENAME="<Insert Instance Name>" [/INDICATEPROGRESS] /CONFIRMIPDEPENDENCYCHANGE=0  
```  
  
##  <a name="Accounts"></a> Parâmetros de conta de serviço  
 É possível configurar os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com uma conta interna, uma conta local ou uma conta de domínio.  
  
> [!NOTE]  
>  Ao usar uma conta de serviço gerenciada, conta virtual ou uma conta interna, você não deve especificar os parâmetros de senha correspondentes. Para obter mais informações sobre estas contas de serviço, consulte a seção **Novos tipos de conta disponíveis com o [!INCLUDE[win7](../../includes/win7-md.md)] e [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]** em [Configurar contas de serviço e permissões do Windows](../configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
 Para obter mais informações sobre configuração de contas de serviço, consulte [Configurar contas de serviço e permissões do Windows](../configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
|componente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Parâmetro de conta|Parâmetro de senha|Tipo de inicialização|  
|-----------------------------------------|-----------------------|------------------------|------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent|/AGTSVCACCOUNT|/AGTSVCPASSWORD|/AGTSVCSTARTUPTYPE|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCACCOUNT|/ASSVCPASSWORD|/ASSVCSTARTUPTYPE|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT|/SQLSVCPASSWORD|/SQLSVCSTARTUPTYPE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT|/ISSVCPASSWORD|/ISSVCStartupType|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT|/RSSVCPASSWORD|/RSSVCStartupType|  
  
##  <a name="Feature"></a> Parâmetros de funcionalidades  
 Para instalar recursos específicos, use o parâmetro /FEATURES e especifique o recurso pai ou os valores de recursos listados na tabela a seguir. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
||||  
|-|-|-|  
|Parâmetro de recurso pai|Parâmetro de recurso|Descrição|  
|SQL||Instala o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], a Replicação, o Texto Completo e o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)].|  
||SQLEngine|Instala apenas o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
||Replicação|Instala o componente Replicação juntamente com o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
||FullText|Instala o componente FullText com o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
||DQ|Copia os arquivos necessários para concluir a instalação do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] . Depois de concluir a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], execute o arquivo DQSInstaller.exe para concluir a instalação do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]. Para obter mais informações, consulte [Executar o DQSInstaller.exe para concluir a instalação do Data Quality Server](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md). O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]também é instalado.|  
|AS||Instala todos os componentes do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|RS||Instala todos os componentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|DQC||Instala o [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)].|  
|IS||Instala todos os componentes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|MDS||Instala o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].|  
|Ferramentas||Instala ferramentas cliente e componentes de Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
||BC|Instala componentes de compatibilidade com versões anteriores.|  
||BOL|Instala componentes de Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para exibir e gerenciar o conteúdo da ajuda.|  
||Conn|Instala os componentes de conectividade.|  
||SSMS|Instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] das ferramentas de gerenciamento - básicas. Isso inclui o seguinte:<br /><br /> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] suporte para o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], **sqlcmd** utilitário e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do PowerShell|  
||ADV_SSMS|Instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ferramentas de gerenciamento - completas. Isso inclui os seguintes componentes, além dos componentes da versão Básica:<br /><br /> Suporte do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]<br /><br /> [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]<br /><br /> [!INCLUDE[ssDE](../../includes/ssde-md.md)] Orientador de Otimização<br /><br /> Gerenciamento do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
||DREPLAY_CTLR|Instala o Distributed Replay Controller|  
||DREPLAY_CLT|Instala o Distributed Replay Client|  
||SNAC_SDK|Instala o SDK para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client|  
||SDK|Instala o Software Development Kit.|  
||LocalDB<sup>1</sup>|Instala o LocalDB, um modo de execução do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] destinado a desenvolvedores de programas.|  
  
 <sup>1</sup> o LocalDB é uma opção na instalação de qualquer SKU do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Express. Para obter mais informações, consulte [SQL Server 2014 Express LocalDB](../configure-windows/sql-server-2016-express-localdb.md).  
  
### <a name="feature-parameter-examples"></a>Exemplos de parâmetros de recursos:  
  
|Parâmetro e valores|Descrição|  
|--------------------------|-----------------|  
|/FEATURES=SQLEngine|Instala o [!INCLUDE[ssDE](../../includes/ssde-md.md)] sem os componentes de replicação e texto completo.|  
|/FEATURES=SQLEngine, FullText|Instala o [!INCLUDE[ssDE](../../includes/ssde-md.md)] e o texto completo.|  
|/FEATURES=SQL, Tools|Instala o [!INCLUDE[ssDE](../../includes/ssde-md.md)] completo e todas as ferramentas.|  
|/FEATURES=BOL|Instala componentes de Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para exibir e gerenciar o conteúdo da ajuda.|  
  
##  <a name="Role"></a> Parâmetros de função  
 A função de instalação ou o parâmetro /Role é usado para instalar uma seleção pré-configurada de recursos. As funções do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instalam uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em um farm existente do SharePoint ou em um novo farm não configurado. São fornecidas duas funções de instalação para dar suporte a cada cenário. Você pode escolher somente uma função de instalação para instalar de cada vez. Se você escolher uma função de instalação, serão instalados os recursos e os componentes que pertencem à função. Você não pode variar os recursos e os componentes que são designados para aquela função. Para obter mais informações sobre como usar o parâmetro de função de recurso, consulte [instalar o PowerPivot do Prompt de comando](../../../2014/sql-server/install/install-powerpivot-from-the-command-prompt.md).  
  
 A função AllFeatures_WithDefaults é o comportamento padrão de edições do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] e reduz o número de caixas de diálogo apresentadas ao usuário. Ela pode ser especificada na linha de comando ao instalar uma edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não seja o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].  
  
|Role|Descrição|Instala...|  
|----------|-----------------|---------------|  
|SPI_AS_ExistingFarm|Instala o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] como uma instância nomeada do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em um farm existente do [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] ou em um servidor autônomo.|Mecanismo de cálculo do[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pré-configurado para o armazenamento e o processamento de dados na memória.<br /><br /> Pacotes de solução do[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] <br /><br /> Programa instalador do [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)]<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online|  
|SPI_AS_NewFarm|Instala o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e o [!INCLUDE[ssDE](../../includes/ssde-md.md)] como uma instância nomeada do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em um novo farm não configurado do Office [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] ou em um servidor autônomo. A Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurará o farm durante a instalação da função de recurso.|Mecanismo de cálculo do[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pré-configurado para o armazenamento e o processamento de dados na memória.<br /><br /> Pacotes de solução do[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] <br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online<br /><br /> [!INCLUDE[ssDE](../../includes/ssde-md.md)]<br /><br /> Ferramentas de configuração<br /><br /> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
|AllFeatures_WithDefaults|Instala todos os recursos que estão disponíveis com a edição atual.<br /><br /> Adiciona o usuário atual para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `sysadmin` função de servidor fixa.<br /><br /> No [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] ou posterior e quando o sistema operacional não é controlador de domínios, o [!INCLUDE[ssDE](../../includes/ssde-md.md)], and [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] são padronizados para usar a conta NTAUTHORITY\NETWORK SERVICE e o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é padronizado para usar a conta NTAUTHORITY\NETWORK SERVICE.<br /><br /> Essa função é habilitada por padrão em edições do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Para todas as outras edições, essa função não é habilitada, mas pode ser especificada por meio da interface do usuário ou de parâmetros de linha de comando.|Em edições do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], instala somente os recursos disponíveis na edição. Nas outras edições, instala todos os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> O parâmetro **AllFeatures_WithDefaults** pode ser combinado com outros parâmetros que substituem as configurações de parâmetro **AllFeatures_WithDefaults** . Por exemplo, o uso do parâmetro **AllFeatures_WithDefaults** e do parâmetro **/Features=RS** substitui o comando para instalar todos os recursos e instala apenas o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], mas obriga o parâmetro **AllFeatures_WithDefaults** a usar a conta de serviço padrão do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].<br /><br /> Ao usar o parâmetro **AllFeatures_WithDefaults** junto com **/ADDCURRENTUSERASSQLADMIN=FALSE** , a caixa de diálogo de provisionamento não será preenchida automaticamente com o usuário atual. Adicione **/AGTSVCACCOUNT** e **/AGTSVCPASSWORD** para especificar uma conta de serviço e uma senha para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
  
##  <a name="RollOwnership"></a> Controlando o comportamento de failover com o parâmetro /FAILOVERCLUSTERROLLOWNERSHIP  
 Para atualizar um cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], você deve executar a Instalação em um nó de cluster de failover de cada vez, começando com os nós passivos. A Instalação determina quando executar o failover para o nó atualizado, dependendo do número total de nós na instância de cluster de failover e do número de nós que já foram atualizados. Quando metade ou mais da metade dos nós já tiver sido atualizada, por padrão, a Instalação provocará um failover em um nó atualizado.  
  
 Para controlar o comportamento de failover de nós de cluster durante o processo de atualização, execute a operação de atualização no prompt de comando e use o parâmetro /FAILOVERCLUSTERROLLOWNERSHIP para controlar o comportamento de failover antes de a operação de atualização colocar o nó offline. Este parâmetro é usado da seguinte maneira:  
  
-   /FAILOVERCLUSTERROLLOWNERSHIP=0 não estenderá a propriedade do cluster (mover grupo) para nós atualizados e não adicionará esse nó à lista de possíveis proprietários do cluster do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no final da atualização.  
  
-   /FAILOVERCLUSTERROLLOWNERSHIP=1 estenderá a propriedade (mover grupo) do cluster para nós atualizados e adicionará esse nó à lista de possíveis proprietários do cluster do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no final da atualização.  
  
-   /FAILOVERCLUSTERROLLOWNERSHIP=2 é a configuração padrão. Ele será usado se esse parâmetro não for especificado. Essa configuração indica que a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerenciará a propriedade (mover grupo) do cluster conforme necessário.  
  
##  <a name="InstanceID"></a> Configuração de ID da Instância ou InstanceID  
 O parâmetro ID da Instância ou /InstanceID é usado para especificar onde você pode instalar os componentes da instância e o caminho do Registro da instância. O valor de "INSTANCEID" é uma cadeia de caracteres e deve ser exclusivo.  
  
-   ID:MSSQL12 de instância do SQL. \<INSTANCEID >  
  
-   ID da instância ID:MSAS12. \<INSTANCEID >  
  
-   RS ID:MSRS12 de instância. \<INSTANCEID >  
  
 Os componentes com suporte à instância são instalados nos seguintes locais:  
  
 % Arquivos de programas %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< SQLInstanceID\>  
  
 % Arquivos de programas %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< ASInstanceID\>  
  
 % Arquivos de programas %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\< RSInstanceID\>  
  
> [!NOTE]  
>  Se INSTANCEID não for especificado na linha de comando, então, por padrão, a Instalação substituirá \<INSTANCEID> pelo \<INSTANCENAME>.  
  
## <a name="see-also"></a>Consulte também  
 [Instalar o SQL Server 2014 do Assistente de instalação &#40;programa de instalação&#41;](install-sql-server-from-the-installation-wizard-setup.md)   
 [Instalação do cluster de failover do SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)   
 [Instalar os recursos de BI do SQL Server 2014](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
  
  
