---
title: PowerShell do Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/11/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 60bb9610-7229-42eb-a95f-a377268a8720
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8effab0536063466efe25161949a0efeebd0038b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48162536"
---
# <a name="analysis-services-powershell"></a>Analysis Services PowerShell
  O [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] contém um provedor SQLAS (Analysis Services PowerShell) e cmdlets para que você possa usar o Windows PowerShell para navegar em, administrar e consultar objetos do Analysis Services.  
  
 O Analysis Services PowerShell consiste no seguinte:  
  
-   Provedor `SQLAS` usado para navegar na hierarquia do AMO (Objetos de Gerenciamento de Análise).  
  
-   Cmdlet `Invoke-ASCmd` usado para executar scripts MDX, DMX ou XMLA.  
  
-   Cmdlets específicos de tarefas para operações rotineiras, como processamento, gerenciamento de funções, gerenciamento de partições, backup e restauração.  
  
## <a name="in-this-article"></a>Neste artigo  
 [Pré-requisitos](#bkmk_prereq)  
  
 [Versões com suporte e modos do Analysis Services](#bkmk_vers)  
  
 [Requisitos de autenticação e considerações de segurança](#bkmk_auth)  
  
 [Tarefas do PowerShell do Analysis Services](#bkmk_tasks)  

Para obter mais informações sobre sintaxe e exemplos, consulte [Analysis Services PowerShell Reference](/sql/analysis-services/powershell/analysis-services-powershell-reference).

##  <a name="bkmk_prereq"></a> Pré-requisitos  
 O Windows PowerShell 2.0 deve estar instalado. Ele é instalado por padrão em versões mais recentes dos sistemas operacionais Windows. Para obter mais informações, consulte [instalar o Windows PowerShell 2.0](https://msdn.microsoft.com/library/ff637750.aspx)

<!-- ff637750.aspx above is linked to by:  (http://go.microsoft.com/fwlink/?LinkId=227613). -->
  
 Você deve instalar um recurso do SQL Server que inclui o módulo do SQL Server PowerShell (SQLPS) e bibliotecas de cliente. O modo mais fácil de fazer isto é instalar o SQL Server Management Studio, que inclui o recurso do PowerShell e bibliotecas de cliente automaticamente. Um módulo SQLPS (SQL Server PowerShell) contém os provedores PowerShell e cmdlets para todos os recursos do SQL Server, incluindo o módulo SQLASCmdlets e o provedor SQLAS usados para navegar na hierarquia de objetos do Analysis Services.  
  
 Você deve importar o **SQLPS** módulo antes de poder usar o `SQLAS` provedor e cmdlets. O provedor SQLAS é uma extensão do `SQLServer` provedor. Há várias maneiras de importar o módulo SQLPS. Para obter mais informações, consulte [Importar o módulo SQLPS](../../2014/database-engine/import-the-sqlps-module.md).  
  
 O acesso remoto a uma instância do Analysis Services exige a habilitação da administração remota e do compartilhamento de arquivos. Para obter mais informações, consulte [habilitar a administração remota](#bkmk_remote) neste tópico.  
  
##  <a name="bkmk_vers"></a> Versões e modos compatíveis do Analysis Services  
 Atualmente, há suporte para o Analysis Services PowerShell em qualquer edição do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Analysis Services executada no Windows Server 2008 R2, Windows Server 2008 SP1 ou Windows 7.  
  
 A tabela a seguir mostra a disponibilidade do Analysis Services PowerShell em diferentes contextos.  
  
|Contexto|Disponibilidade de recursos do PowerShell|  
|-------------|-------------------------------------|  
|Instâncias e bancos de dados multidimensionais|Com suporte para administração local e remota.<br /><br /> A partição de mesclagem exige uma conexão local.|  
|Instâncias e bancos de dados tabulares|Com suporte para administração local e remota.<br /><br /> Para obter mais informações, consulte um blog de agosto de 2011 [gerenciar Tabular Models Using PowerShell](http://go.microsoft.com/fwlink/?linkID=227685).|  
|Instâncias e bancos de dados PowerPivot para SharePoint|Suporte limitado. É possível usar conexões HTTP e o provedor SQLAS para visualizar informações da instância e do banco de dados.<br /><br /> Porém, não há suporte para usar os cmdlets. Você não deve usar o Analysis Services PowerShell para fazer backup e restauração de banco de dados PowerPivot na memória, nem deve adicionar ou remover funções, processar os dados ou executar script XMLA arbitrário.<br /><br /> Para fins de configuração, o PowerPivot para SharePoint tem suporte interno ao PowerShell que é fornecido separadamente. Para obter mais informações, consulte [referência do PowerShell para PowerPivot para SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint).|  
|Conexões nativas a cubos locais<br /><br /> “Data Source=c:\backup\test.cub”|Sem suporte.|  
|Conexões HTTP a arquivos de conexão do modelo semântico BI (.bism) no SharePoint<br /><br /> "Fonte de dados =http://server/shared_docs/name.bism"|Sem suporte.|  
|Conexões inseridas em bancos de dados PowerPivot<br /><br /> “Data Source=$Embedded$”|Sem suporte.|  
|Contexto de servidor local em procedimentos armazenados do Analysis Services<br /><br /> “Data Source=*”|Sem suporte.|  
  
##  <a name="bkmk_auth"></a> Requisitos de autenticação e considerações de segurança  
 Ao conectar-se ao Analysis Services, você deve fazer a conexão usando uma identidade de usuário do Windows. Na maioria das vezes, a conexão é feita usando uma segurança integrada do Windows, onde a identidade do usuário atual define o contexto de segurança sob o qual as operações de servidor são realizadas. No entanto, outros métodos de autenticação ficam disponíveis quando você configura o acesso de HTTP para o Analysis Services. Esta seção explica como o tipo de conexão determina quais opções de autenticação você pode usar.  
  
 As conexões para o Analysis Services são caracterizadas como conexões nativas ou conexões HTTP. Uma conexão nativa é uma conexão direta de um aplicativo cliente para o servidor. Em uma sessão do PowerShell, o cliente PowerShell usa o provedor OLE DB para o Analysis Services conectar-se diretamente a uma instância do Analysis Services. Uma conexão nativa é sempre feita usando uma segurança integrada do Windows, onde o Analysis Services PowerShell é executado como o usuário atual. O Analysis Services não dá suporte à representação. Se você desejar realizar uma operação como um usuário específico, deverá iniciar a sessão do PowerShell como esse usuário.  
  
 As conexões HTTP são feitas indiretamente por meio do IIS, permitindo opções adicionais de autenticação, como autenticação Básica, para conectar-se a uma instância do Analysis Services. Como o IIS dá suporte à representação, você pode fornecer uma cadeia de conexão que inclui credenciais que o IIS usará para representar ao fazer uma conexão. Para fornecer credenciais, você pode usar o parâmetro –Credential.  
  
 **Usando o parâmetro – Credential no PowerShell**  
  
 O parâmetro –Credential parameter usa o objeto PSCredential que especifica um nome de usuário e senha. No Analysis Services PowerShell, o parâmetro –Credential está disponível para cmdlets que fazem uma solicitação de conexão ao Analysis Services, em vez dos cmdlets que são executados dentro do contexto de uma conexão existente. Os cmdlets que fazem uma solicitação de conexão incluem Invoke-ASCmd, Backup-ASDatabase e Restore-ASDatabase. Para estes cmdlets, o parâmetro –Credential pode ser usado, supondo que os seguintes critérios sejam atendidos:  
  
1.  O servidor está configurado para acesso HTTP, o que significa que o IIS trata a conexão, lê o nome de usuário e a senha, e representa a identidade do usuário ao conectar-se ao Analysis Services. Para obter mais informações, consulte [Configurar o acesso HTTP ao Analysis Services nos Serviços de Informações da Internet &#40;IIS&#41; 8.0](instances/configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
2.  O diretório virtual IIS que foi criado para acesso HTTP do Analysis Services está configurado para autenticação Básica.  
  
3.  O nome de usuário e a senha fornecidos pelo objeto de credencial são resolvidos para uma identidade de usuário do Windows. O Analysis Services usa esta identidade como usuário atual. Se o usuário não for Windows ou não tiver permissões suficientes para realizar a operação solicitada, a solicitação falhará.  
  
 Para criar um objeto de credencial, você pode usar o cmdlet Get-Credential para coletar as credenciais do operador. Você poderá então usar o objeto de credencial em um comando que conecta-se ao Analysis Services. O exemplo a seguir ilustra a sintaxe uma abordagem. Neste exemplo, a conexão é para uma instância local configurada para acesso HTTP.  
  
```  
PS SQLSERVER:\SQLAS\HTTP_DS> $cred = Get-credential adventureworks\dbadmin  
PS SQLSERVER:\SQLAS\HTTP_DS> Invoke-ASCmd –Inputfile:”c:\discoverconnections.xmla” –Credential:$cred  
```  
  
 Ao usar autenticação Básica, você sempre deve usar HTTP com SSL, para que o nome de usuário e as senhas sejam enviados por meio de uma conexão criptografada. Para obter mais informações, consulte [configurar Secure Sockets Layer no IIS 7.0](http://go.microsoft.com/fwlink/?linkID=184299) e [configurar autenticação básica (IIS 7)](http://go.microsoft.com/fwlink/?LinkId=230776).  
  
 Lembre-se de que as credenciais, as consultas e os comandos que você fornecer no PowerShell são passados inalterados para a camada de transporte. Incluir conteúdo confidencial em seus scripts aumenta o risco de um ataque de injeção mal-intencionado.  
  
 **Fornecendo uma senha como um objeto Microsoft.Secure.String**  
  
 Algumas operações, como backup e restauração, dão suporte a opções de criptografia que são ativadas quando você fornece uma senha no comando. Fornecer a senha sinaliza ao Analysis Services para criptografar ou descriptografar o arquivo de backup. No Analysis Services, essa senha é instanciada como um objeto de cadeia de caracteres seguro. O exemplo a seguir fornece uma ilustração de como coletar uma senha do operador em tempo de execução.  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default> $pwd = read-host -AsSecureString -Prompt "Password"  
Password: ****  
PS SQLSERVER:\SQLAS\Localhost\default> $pwd -is [System.IDisposable]   
True  
```  
  
 Você agora pode fazer backup ou restaurar um arquivo de banco de dados criptografado, passando a variável $pwd para o parâmetro da senha. Para ver um exemplo completo que combina Esta ilustração com outros cmdlets, consulte [cmdlet Backup-ASDatabase](/sql/analysis-services/powershell/backup-asdatabase-cmdlet) e [cmdlet Restore-ASDatabase](/sql/analysis-services/powershell/restore-asdatabase-cmdlet).
  
 Como uma etapa de acompanhamento, remova a senha e a variável da sessão.  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default> $pwd.Dispose()  
PS SQLSERVER:\SQLAS\Localhost\default> Remove-Variable -Name pwd  
```  
  
##  <a name="bkmk_tasks"></a> Tarefas do PowerShell do Analysis Services  
 É possível executar o Analysis Services PowerShell por meio do shell de gerenciamento do Windows PowerShell ou de um prompt de comando do Windows. Não é possível executar o Analysis Services PowerShell por meio do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
 Esta seção descreve as tarefas comuns para usar o Analysis Services PowerShell.  
  
-   [A análise de carga dos serviços de provedor e Cmdlets](#bkmk_load)  
  
-   [Habilitar a administração remota](#bkmk_remote)  
  
-   [Conectar-se ao objeto de um Analysis Services](#bkmk_connect)  
  
-   [Administrar o serviço](#bkmk_admin)  
  
-   [Obter ajuda para o Analysis Services PowerShell](#bkmk_help)  
  
###  <a name="bkmk_load"></a> A análise de carga dos serviços de provedor e Cmdlets  
 O provedor do Analysis Services é uma extensão do provedor raiz do SQL Server que se torna disponível quando você importa o módulo SQLPS. Os cmdlets do Analysis Services são carregados simultaneamente; você também pode carregá-los de forma independente se desejar usá-los sem o provedor.  
  
-   Execute o cmdlet Import-module para carregar o SQLPS que inclui toda a funcionalidade do Analysis Services PowerShell. Se você não conseguir importar o módulo, poderá alterar temporariamente a política de execução para irrestrita com a finalidade de carregar o módulo. Para obter mais informações, consulte [Importar o módulo SQLPS](../../2014/database-engine/import-the-sqlps-module.md).  
  
    ```  
    Import-module “sqlps”  
    ```  
  
     Opcionalmente, use `import-module “sqlps” –disablenamechecking` para suprimir o aviso sobre nomes de verbos não aprovados.  
  
-   Para carregar apenas os cmdlets do Analysis Services específicos da tarefa, sem o provedor do Analysis Services ou o cmdlet Invoke-ASCmd, é possível carregar o módulo SQLASCmdlets como uma operação independente.  
  
    ```  
    Import-module “sqlascmdlets”  
    ```  
  
###  <a name="bkmk_remote"></a> Habilitar a administração remota  
 Antes de poder usar o Analysis Services PowerShell com uma instância remota do Analysis Services, é necessário primeiramente habilitar a administração remota e o compartilhamento de arquivos. O erro a seguir indica um problema de configuração de firewall: "O servidor RPC não está disponível. (Exceção de HRESULT: 0x800706BA) ".  
  
1.  Verifique se ambos os computadores local e remoto possuem as versões [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] das ferramentas de cliente e servidor.  
  
2.  No servidor remoto que está hospedando uma instância do Analysis Services, abra porta TCP 2383 no Firewall do Windows. Se você instalou o Analysis Services como instância nomeada ou está usando uma porta personalizada, o número da porta será diferente. Para obter mais informações, consulte [Configure the Windows Firewall to Allow Analysis Services Access](instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
3.  No servidor remoto, verifique se os seguintes serviços foram iniciados: serviço RPC (Chamada de Procedimento Remoto), serviço TCP/IP NetBIOS Helper, serviço WMI (Instrumentação de Gerenciamento do Windows), serviço WS-Management (Windows Remote Management).  
  
4.  No servidor remoto, inicie o snap-in do Editor de Objeto de Política de Grupo (gpedit.msc).  
  
5.  Abra: Configuração do Computador, Modelos Administrativos, Rede, Conexões de Rede, Firewall do Windows e Perfil do Domínio.  
  
6.  Clique duas vezes em **Firewall do Windows: Permitir exceção de administração remota de entrada**, selecione **Enabled**e, em seguida, clique em **Okey**.  
  
7.  Clique duas vezes em **Firewall do Windows: permitir que o arquivo de entrada e exceções no compartilhamento de impressora**, selecione **Enabled**e, em seguida, clique em **Okey**.  
  
8.  No computador local que tenha as ferramentas de cliente, use os cmdlets a seguir para verificar a administração remota, substituindo o nome real do servidor para o *nome de servidor remoto* espaço reservado. Omita o nome da instância se o Analysis Services for instalado como instância padrão. É necessário ter importado o módulo SQLPS previamente para que o comando funcione.  
  
    ```  
    PS SQLSERVER:\> cd sqlas  
    PS SQLSERVER:\sqlas> cd <remote-server-name\instance-name>  
    PS SQLSERVER:\sqlas\<remote-server-name\instance-name> dir  
    ```  
  
 Em alguns casos, as configurações adicionais podem ser necessárias. Talvez seja necessário digitar o seguinte no servidor remoto antes de poder emitir comandos para ele de outro computador:  
  
```  
Enable-psremoting  
```  
  
  
###  <a name="bkmk_connect"></a> Conectar-se ao objeto de um Analysis Services  
 O provedor do Analysis Services PowerShell oferece suporte à navegação na hierarquia de objetos do Analysis Services e define o contexto para a execução de comandos. O provedor é uma extensão do provedor raiz SQLSERVER disponível pelo módulo SQLPS. Depois de carregar o módulo SQLPS, é possível navegar pelo caminho.  
  
 É possível conectar-se a uma instância local ou remota, mas alguns cmdlets são executados somente em uma instância local (isto é, partição de mesclagem). É possível usar uma conexão nativa ou uma conexão HTTP para servidores do Analysis Services que você configurou para acesso HTTP. As ilustrações a seguir mostram o caminho de navegação para conexões nativas e HTTP. As ilustrações a seguir mostram o caminho de navegação para conexões nativas e HTTP.  
  
 **Conexões nativas com o Analysis Services**  
  
 ![Conexão nativa com o Analysis Services](media/ssas-powershell-nativeconnection.gif "conexão nativa com o Analysis Services")  
  
 O exemplo a seguir é uma demonstração de como usar uma conexão nativa para navegar na hierarquia de objetos. No provedor, é possível emitir `dir` para visualizar informações da instância. É possível usar `cd` para visualizar objetos dessa instância.  
  
```  
PS SQLSERVER:> cd sqlas  
PS SQLSERVER\sqlas:> dir  
PS SQLSERVER\sqlas:> cd localhost\default  
PS SQLSERVER\sqlas\localhost\default:> dir  
```  
  
 Você deverá ver as seguintes coleções: assemblies, bancos de dados, funções e rastreamentos. Se você continuar a usar `cd` e `dir`, poderá visualizar o conteúdo de cada coleção.  
  
 **Conexões de HTTP ao Analysis Services**  
  
 ![Conexão HTTP ao Analysis Services](media/ssas-powershell-httpconnection.gif "Conexão HTTP ao Analysis Services")  
  
 Conexões HTTP serão úteis se você tiver configurado o servidor de acesso HTTP, usando as instruções neste tópico: [configurar o acesso HTTP ao Analysis Services no serviços de informações da Internet &#40;IIS&#41; 8.0](instances/configure-http-access-to-analysis-services-on-iis-8-0.md)  
  
 Supondo que a URL de servidor http://localhost/olap/msmdpump.dll, uma conexão pode parecer com o seguinte:  
  
```  
PS SQLSERVER\sqlas:> cd http_ds  
PS SQLSERVER\sqlas\http_ds:> $Url=Encode-SqlName “http://localhost/olap/msmdpump.dll”  
PS SQLSERVER\sqlas\http_ds:> cd $Url  
PS SQLSERVER\sqlas\http_ds\http%3A%2F%2Flocalhost%2olap%2msmdpump%2Edll:> dir  
```  
  
 Você deverá ver as seguintes coleções: assemblies, bancos de dados, funções e rastreamentos. Se você não conseguir visualizar o conteúdo dessas coleções, verifique as configurações de autenticação no diretório virtual OLAP. Certifique-se de que Acesso Anônimo esteja desabilitado. Se você estiver usando a Autenticação do Windows, verifique se sua conta de usuário do Windows possui permissões administrativas na instância do Analysis Services.  
  
###  <a name="bkmk_admin"></a> Administrar o serviço  
 Verifique se o serviço está em execução. Retorna status, nome e nome para exibição dos serviços do SQL Server, incluindo Analysis Services (MSSQLServerOLAPService) e Mecanismo de Banco de Dados.  
  
```  
Get-service mssql*  
```  
  
 Retorna as propriedades de um processo, incluindo a ID do processo, contagem de identificadores e uso da memória:  
  
```  
Get-process msmdsrv  
```  
  
 Reinicia o serviço ao emitir o seguinte cmdlet a partir do shell de administrador:  
  
```  
Restart-service mssqlserverolapservice  
```  
  
###  <a name="bkmk_help"></a> Obter ajuda para o Analysis Services PowerShell  
 Use qualquer um dos cmdlets a seguir para verificar a disponibilidade do cmdlet e obter mais informações sobre serviços, processos e objetos.  
  
1.  `Get-help` retorna a ajuda interna sobre um cmdlet do Analysis Services, incluindo exemplos:  
  
    ```  
    Get-help invoke-ascmd -examples  
    ```  
  
2.  `Get-command` retorna uma lista dos onze cmdlets do Analysis Services PowerShell:  
  
    ```  
    get-command –module SQLASCmdlets  
    ```  
  
3.  `Get-member` retorna as propriedades ou os métodos de um serviço ou processo.  
  
    ```  
    Get-service mssqlserverolapservice | get-member –type Property  
    ```  
  
    ```  
    Get-service mssqlserverolapservice | get-member –type Method  
    ```  
  
    ```  
    Get-process msmdsrv | get-member –type Property  
    ```  
  
4.  `Get-member` também pode ser usado para retornar as propriedades ou os métodos de um objeto (por exemplo, métodos do AMO no objeto de servidor) usando o provedor SQLAS para especificar a instância do servidor.  
  
    ```  
    PS SQLSERVER:\sqlas\localhost\default > $serverObj = New-Object Microsoft.AnalysisServices.Server  
    PS SQLSERVER:\sqlas\localhost\default > $serverObj = | get-member –type Method  
    ```  
  
5.  `Get-PSdrive` retorna uma lista dos provedores instalados no momento. Se você tiver importado o módulo SQLPS, verá o provedor `SQLServer` na lista (SQLAS faz parte do provedor SQLServer e nunca aparece separadamente na lista):  
  
    ```  
    Get-PSDrive  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Instalar o SQL Server PowerShell](../database-engine/install-windows/install-sql-server-powershell.md)   
 [Gerenciar Tabular Models Using PowerShell (blog)](http://go.microsoft.com/fwlink/?linkID=227685)   
 [Configurar o acesso HTTP ao Analysis Services nos serviços de informações da Internet &#40;IIS&#41; 8.0](instances/configure-http-access-to-analysis-services-on-iis-8-0.md)  
  
  
