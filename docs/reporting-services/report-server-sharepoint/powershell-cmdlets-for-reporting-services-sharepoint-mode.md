---
title: "Cmdlets PowerShell para Modo do SharePoint do Reporting Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7835bc97-2827-4215-b0dd-52f692ce5e02
caps.latest.revision: 32
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 31
---
# Cmdlets PowerShell para Modo do SharePoint do Reporting Services
  Quando você instala o modo do SharePoint do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , os cmdlets do PowerShell são instalados para oferecer suporte a servidores de relatório no modo do SharePoint. Os cmdlets abrangem três categorias de funcionalidade.  
  
-   Instalação do serviço compartilhado e proxy do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint.  
  
-   Provisionando e gerenciamento de aplicativos de serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e proxy associados.  
  
-   Gerenciamento de recursos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , por exemplo, extensões e chave de criptografia.  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint Mode|  
  
 **Este tópico inclui o seguinte:**  
  
-   [Resumo do cmdlet](#bkmk_cmdlet_sum)  
  
-   [Cmdlets de serviço compartilhado e proxy](#bkmk_sharedservice_cmdlets)  
  
-   [Cmdlets de serviço de aplicativo e proxy](#bkmk_serviceapp_cmdlets)  
  
-   [Cmdlets de funcionalidade personalizada do Reporting Services](#bkmk_ssrsfeatures_cmdlets)  
  
-   [Exemplos Básicos do PowerShell Reporting Services](#bkmk_basic_samples)  
  
-   [Exemplos Detalhados do PowerShell Reporting Services](#bkmk_detailedsamples)  
  
    -   [Cria um aplicativo de serviço e proxy Reporting Services](#bkmk_example_create_service_application)  
  
    -   [Examinar e atualizar uma extensão de entrega do Reporting Services](#bkmk_example_delivery_extension)  
  
    -   [Obter e definir propriedades do banco de dados do aplicativo Reporting Services](#bkmk_example_db_properties)  
  
    -   [Listar extensões de dados do Microsoft Reporting Services](#bkmk_example_list_data_extensions)  
  
    -   [Alterar e listar proprietários de assinaturas do Reporting Services](#bkmk_change_subscription_owner)  
  
##  <a name="bkmk_cmdlet_sum"></a> Resumo do cmdlet  
 Para executar os cmdlets, é necessário abrir o Shell de Gerenciamento do SharePoint. Você também pode usar o editor de interface gráfica do usuário incluído no Microsoft Windows, o **Ambiente de Script Integrado do Windows PowerShell (ISE)**. Para obter mais informações, consulte [Starting Windows PowerShell on Windows Server (Iniciando o Windows PowerShell no Windows Server)](http://technet.microsoft.com/library/hh847814.aspx) (http://technet.microsoft.com/library/hh847814.aspx). Nos resumos de cmdlet a seguir, as referências a 'bancos de dados' de aplicativo de serviço referem-se a todos os bancos de dados criados e usados por um aplicativo de serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Isso inclui a os bancos de dados de configuração, alerta e temp.  
  
 Se uma mensagem de erro semelhante à seguinte for exibida quando você digitar os exemplos do PowerShell:  
  
-   Install-SPRSService: o termo 'Install-SPRSService' não é reconhecido como  
    nome de cmdlet, função, arquivo de script ou programa operável. Verifique a ortografia do nome ou, se um caminho tiver sido incluído, verifique se ele está correto e tente novamente.  
  
 Um destes problemas está ocorrendo:  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não está instalado e, portanto, os cmdlets do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] também não estão instalados.  
  
-   Você executou o comando do PowerShell no Windows PowerShell ou no ISE do Windows PowerShell, e não no Shell de Gerenciamento do SharePoint. Use o Shell de Gerenciamento do SharePoint ou adicione o Snap-in do SharePoint à janela do Windows PowerShell com o seguinte comando:  
  
    ```  
    Add-PSSnapin Microsoft.SharePoint.PowerShell  
    ```  
  
 Para obter mais informações, consulte [Usar o Windows PowerShell para administrar o SharePoint 2013](http://technet.microsoft.com/library/ee806878.aspx) (http://technet.microsoft.com/library/ee806878.aspx).  
  
#### Para abrir p Shell de Gerenciamento do SharePoint e executar cmdlets  
  
1.  Clique no botão **Iniciar**  
  
2.  Clique no grupo **Produtos do Microsoft SharePoint** .  
  
3.  Abra o **Shell de Gerenciamento do SharePoint**.  
  
 Para exibir a ajuda de linha de comando de um cmdlet, use o comando 'Get-Help' do PowerShell no prompt de comando do PowerShell. Por exemplo:  
  
 `Get-Help Get-SPRSServiceApplicationServers`  
  
###  <a name="bkmk_sharedservice_cmdlets"></a> Cmdlets de serviço compartilhado e proxy  
 A tabela a seguir contém os cmdlets PowerShell do serviço compartilhado [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint.  
  
|Cmdlet|Description|  
|------------|-----------------|  
|Install-SPRSService|Instala e registra, ou desinstala, o aplicativo do serviço compartilhado [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Só pode ser feito em um computador que tenha o SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado no modo integrado do SharePoint. Para instalação, há duas operações:<br /><br /> O serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é instalado no farm.<br /><br /> - A instância do serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é instalada no computador atual.<br /><br /> Para desinstalação, há duas operações:<br /><br /> - Desinstalar o serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do computador atual.<br /><br /> O serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é desinstalado do farm.<br /><br /> <br /><br /> OBSERVAÇÃO: se houver outros computadores no farm que tenham o serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado, ou se ainda houver aplicativos do serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em execução no farm, uma mensagem de aviso será exibida.|  
|Install-SPRSServiceProxy|Instala e registra, ou desinstala, o proxy do serviço Reporting Services no farm do SharePoint.|  
|Obtém-SPRSProxyUrl|Obtém as URLs para acessar o serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|Get-SPRSServiceApplicationServers|Acessa todos os servidores no farm local do SharePoint que contém uma instalação do serviço compartilhado [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Esse cmdlet é útil para as atualizações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , para determinar quais servidores executam o serviço compartilhado e, portanto, quais precisam ser atualizados.|  
  
###  <a name="bkmk_serviceapp_cmdlets"></a> Cmdlets de serviço de aplicativo e proxy  
 A tabela a seguir contém cmdlets PowerShell para aplicativos de serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e seus proxies associados.  
  
|Cmdlet|Description|  
|------------|-----------------|  
|Get-SPRSServiceApplication|Obtém um ou mais objetos do aplicativo do serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|New-SPRSServiceApplication|Cria um novo aplicativo do serviço Reporting Services e os bancos de dados associados.<br /><br /> Parâmetro LogonType: especifica se o servidor de relatório usa a conta do Pool de Aplicativos do SSRS ou um logon do SQL Server para acessar o banco de dados do servidor de relatório. Os valores válidos são:<br /><br /> 0 Autenticação do Windows<br /><br /> 1 SQL Server<br /><br /> 2 Conta do pool de aplicativos (padrão)|  
|Remove-SPRSServiceApplication|Remove o aplicativo do serviço Reporting Services especificado. Isso também removerá os bancos de dados associados.|  
|Set-SPRSServiceApplication|Edita as propriedades de um aplicativo do serviço Reporting Services existente.|  
|New-SPRSServiceApplicationProxy|Cria um novo proxy do aplicativo do serviço Reporting Services.|  
|Get-SPRSServiceApplicationProxy|Obtém um ou mais proxies de aplicativo do serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|Dismount-SPRSDatabase|Desmonta os bancos de dados do aplicativo de serviço de um aplicativo do serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|Remove-SPRSDatabase|Remove os bancos de dados do aplicativo de serviço de um aplicativo do serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|Set-SPRSDatabase|Define as propriedades dos bancos de dados associados a um aplicativo do serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|Mount-SPRSDatabase|Monta bancos de dados para um aplicativo de serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|New-SPRSDatabase|Cria novos bancos de dados do aplicativo de serviço para o aplicativo do serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] especificado.|  
|Get-SPRSDatabaseCreationScript|Imprime o script de criação do banco de dados na tela do banco de dados de aplicativo do serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Assim, você pode executar o script no SQL Server Management Studio.|  
|Get-SPRSDatabase|Obtém um ou mais proxies de bancos de dados do aplicativo do serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Use o comando para obter a ID do banco de dados do aplicativo de serviço para que você possa usar o comdlet Set-SPRSDatabase para alterar as propriedades, por exemplo `querytimeout`. Veja o exemplo neste tópico, [Obter e definir propriedades do Banco de dados do aplicativo Reporting Services](#bkmk_example_db_properties).|  
|Get-SPRSDatabaseRightsScript|Imprime o script de direitos do banco de dados na tela do banco de dados de aplicativo do serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . O usuário e o banco de dados desejados serão solicitados e o transact SQL que você pode executar para modificar permissões é retornado. Assim, você pode executar esse script no SQL Server Management Studio.|  
|Get-SPRSDatabaseUpgradeScript|Gera um script de atualização de banco de dados na tela. O script atualizará os bancos de dados do aplicativo de serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para a versão do banco de dados da instalação atual do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
  
###  <a name="bkmk_ssrsfeatures_cmdlets"></a> Cmdlets de funcionalidade personalizada do Reporting Services  
  
|Cmdlet|Description|  
|------------|-----------------|  
|Update-SPRSEncryptionKey|Atualiza a chave de criptografia do aplicativo do serviço Reporting Services especificado e recriptografa seus dados.|  
|Restore-SPRSEncryptionKey|Restaura a chave de criptografia com backup anterior para um aplicativo do serviço Reporting Services.|  
|Remove-SPRSEncryptedData|Exclui os dados criptografados do aplicativo do serviço Reporting Services especificado.|  
|Backup-SPRSEncryptionKey|Atualiza a chave de criptografia do aplicativo de serviço especificado do Reporting Services e recriptografa seus dados.|  
|New-SPRSExtension|Registra uma nova extensão com um aplicativo do serviço Reporting Services.|  
|Set-SPRSExtension|Define as propriedades de uma extensão existente do Reporting Services.|  
|Remove-SPRSExtension|Remove uma extensão de um aplicativo do serviço Reporting Services.|  
|Get-SPRSExtension|Obtém uma ou mais extensões do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para um aplicativo do serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .<br /><br /> Os valores válidos são:<br /><br /> <br /><br /> Entrega<br /><br /> DeliveryUI<br /><br /> Renderizar<br /><br /> Dados<br /><br /> Segurança<br /><br /> Autenticação<br /><br /> EventProcessing<br /><br /> ReportItems<br /><br /> Designer<br /><br /> ReportItemDesigner<br /><br /> ReportItemConverter<br /><br /> ReportDefinitionCustomization|  
|Get-SPRSSite|Acessa sites do SharePoint com base na habilitação ou não do recurso "ReportingService". Por padrão, os sites que habilitam o recurso "ReportingService" são retornados.|  
  
##  <a name="bkmk_basic_samples"></a> Exemplos Básicos do PowerShell Reporting Services  
 Retorna uma lista de cmdlets que contém 'SPRS' no nome. Essa será a lista completa de cmdlets [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
```  
Get-command –noun *SPRS*  
```  
  
 Ou com um pouco mais de detalhes, conectada a um arquivo de texto denominado commandlist.txt  
  
```  
Get-command -noun *SPRS* | Select name, definition | Format-List | Out-File c:\commandlist.txt  
```  
  
 Instala o serviço e o proxy de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint.  
  
```  
Install-SPRSService  
```  
  
```  
Install-SPRSServiceProxy  
```  
  
 Inicie o serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
```  
get-spserviceinstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
```  
  
 Digite o seguinte comando do SharePoint Management Shell para retornar uma lista filtrada de linhas de um arquivo de log. O comando filtrará por linhas que contêm “ssrscustomactionerror”. Este exemplo examina o arquivo de log criado quando o rssharepoint.msi foi instalado.  
  
```  
Get-content -path C:\Users\testuser\AppData\Local\Temp\rs_sp_0.log | select-string "ssrscustomactionerror"  
```  
  
##  <a name="bkmk_detailedsamples"></a> Exemplos Detalhados do PowerShell Reporting Services  
 Além das amostras seguintes, veja a seção "Script do Windows PowerShell" no tópico [Windows PowerShell script for Steps 1–4](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md#bkmk_full_script).  
  
###  <a name="bkmk_example_create_service_application"></a> Cria um aplicativo de serviço e proxy Reporting Services  
 Este script de exemplo conclui as tarefas seguintes:  
  
1.  Cria um aplicativo de serviço e proxy Reporting Services. O script assume que o pool de aplicativos "My App Pool" já existe.  
  
2.  Adicione o proxy ao grupo proxy padrão.  
  
3.  Conceda o acesso de aplicativo de serviço à porta 80 ao banco de dados de conteúdo de aplicativo Web. O script assume que "http://sitename" de site já existe.  
  
```  
# Create service application and service application proxy  
$appPool = Get-SPServiceApplicationPool “My App Pool”  
$serviceApp = New-SPRSServiceApplication “My RS Service App” –ApplicationPool $appPool  
$serviceAppProxy = New-SPRSServiceApplicationProxy –Name “My RS Service App Proxy” –ServiceApplication $serviceApp  
  
# Add service application proxy to default proxy group.  Any web application that uses the default proxy group will now be able to use this service application.  
Get-SPServiceApplicationProxyGroup –default | Add-SPServiceApplicationProxyGroupMember –Member $serviceAppProxy  
  
# Grant application pool account access to the port 80 web application’s content database.  
$webApp = Get-SPWebApplication “http://sitename”  
$appPoolAccountName = $appPool.ProcessAccount.LookupName()  
$webApp.GrantAccessToProcessIdentity($appPoolAccountName)  
  
```  
  
###  <a name="bkmk_example_delivery_extension"></a> Examinar e atualizar uma extensão de entrega do Reporting Services  
 O exemplo de script PowerShell a seguir atualiza a configuração completa da extensão de entrega de email do servidor de relatório para o aplicativo de serviço denominado `My RS Service App`. Atualize os valores do servidor SMTP (`<email server name>`) e o alias de email FROM (`<your FROM email address>`).  
  
```  
$app=get-sprsserviceapplication -Name "My RS Service App"  
$emailCfg = Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml   
$emailXml = [xml]$emailCfg   
$emailXml.SelectSingleNode("//SMTPServer").InnerText = “<email server name>”  
$emailXml.SelectSingleNode("//SendUsing").InnerText = "2"  
$emailXml.SelectSingleNode("//SMTPAuthenticate").InnerText = "2"  
$emailXml.SelectSingleNode("//From").InnerText = '<your FROM email address>'  
Set-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" -ExtensionConfiguration $emailXml.OuterXml  
```  
  
 No exemplo acima, se você não sabia o nome exato do aplicativo de serviço, poderia reescrever a primeira instrução para obter o aplicativo de serviço com base em uma pesquisa de nome parcial. Por exemplo:  
  
```  
$app=get-sprsserviceapplication | where {$_.name -like " ssrs_testapp *"}  
```  
  
 O exemplo de script a seguir retornará os valores de configuração atuais da extensão de entrega de email do servidor de relatório para o aplicativo de serviço denominado “Reporting Services Application”. A primeira etapa define o valor da variável $app para o objeto do aplicativo de serviço denominado "My RS Service App"  
  
 A segunda instrução obterá a extensão de entrega 'Email de Servidor de Relatório' para o objeto de aplicativo de serviço na variável $app e selecionará configurationXML  
  
```  
$app=get-sprsserviceapplication –Name "Reporting Services Application"  
Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml  
```  
  
 Você também pode reescrever as duas instruções acima como se fossem uma:  
  
```  
get-sprsserviceapplication –Name "Reporting Services Application" | Get-SPRSExtension -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml  
```  
  
###  <a name="bkmk_example_db_properties"></a> Obter e definir propriedades do banco de dados do aplicativo Reporting Services  
 O seguinte exemplo retorna primeiro uma lista de banco de dados e propriedades, de forma que é possível determinar o banco de dados guid (ID) que você fornecerá ao comando do conjunto. Para obter uma lista completa das propriedades, consulte `Get-SPRSDatabase | format-list`.  
  
```  
get-SPRSDatabase | select id, querytimeout,connectiontimeout, status, server, ServiceInstance   
```  
  
 O item a seguir é um exemplo de saída. Determine a ID para o banco de dados que você deseja modificar e use a ID no cmdlet SET.  
  
-   `Id                : 56f8d1bc-cb04-44cf-bd41-a873643c5a14`  
  
     `QueryTimeout      : 120`  
  
     `ConnectionTimeout : 15`  
  
     `Status            : Online`  
  
     `Server            : SPServer Name=uetestb01`  
  
     `ServiceInstance   : SPDatabaseServiceInstance`  
  
```  
Set-SPRSDatabase –identity 56f8d1bc-cb04-44cf-bd41-a873643c5a14 -QueryTimeout 300  
```  
  
 Para verificar se o valor está definido, execute o cmdlet GET novamente.  
  
```  
Get-SPRSDatabase –identity 56f8d1bc-cb04-44cf-bd41-a873643c5a14 | select id, querytimeout,connectiontimeout, status, server, ServiceInstance  
```  
  
###  <a name="bkmk_example_list_data_extensions"></a> Listar extensões de dados do Microsoft Reporting Services  
 O exemplo a seguir executa um loop em cada aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e lista as extensões de dados atuais de cada um deles.  
  
```  
$apps = Get-SPRSServiceApplication  
foreach ($app in $apps)   
{  
Write-host -ForegroundColor "yellow" Service App Name $app.Name  
Get-SPRSExtension -identity $app -ExtensionType “Data” | select name,extensiontype | Format-Table -AutoSize  
}  
```  
  
 **Exemplo de saída:**  
  
-   `Name           ExtensionType`  
  
     `----           -------------`  
  
     `SQL                     Data`  
  
     `SQLAZURE                Data`  
  
     `SQLPDW                  Data`  
  
     `OLEDB                   Data`  
  
     `OLEDB-MD                Data`  
  
     `ORACLE                  Data`  
  
     `ODBC                    Data`  
  
     `XML                     Data`  
  
     `SHAREPOINTLIST          Data`  
  
###  <a name="bkmk_change_subscription_owner"></a> Alterar e listar proprietários de assinaturas do Reporting Services  
 Consulte [Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription](../../reporting-services/subscriptions/manage subscription owners and run subscription - powershell.md).  
  
## Consulte também  
 [Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription](../../reporting-services/subscriptions/manage subscription owners and run subscription - powershell.md)   
 [Lista de verificação: usar o PowerShell para verificar o Power Pivot para SharePoint](../../analysis-services/instances/install-windows/checklist-use-powershell-to-verify-power-pivot-for-sharepoint.md)   
 [Obter Ajuda do SQL Server PowerShell](../../relational-databases/scripting/get-help-sql-server-powershell.md)   
 [Scripts PowerShell scripts de gerenciamento do CodePlex SharePoint](http://sharepointpsscripts.codeplex.com/)   
 [Como administrar SSRS usando o PowerShell](https://curatedviews.cloudapp.net/13107/how-to-administer-ssrs-using-powershell)  
  
  