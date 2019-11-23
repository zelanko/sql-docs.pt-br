---
title: Cmdlets do PowerShell para o modo do Reporting Services SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 7835bc97-2827-4215-b0dd-52f692ce5e02
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8cb603eebc75c03420300757bd09cae25fce3c52
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783306"
---
# <a name="powershell-cmdlets-for-reporting-services-sharepoint-mode"></a>Cmdlets do PowerShell para Modo do SharePoint do Reporting Services
  Quando você instala o modo do SharePoint do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , os cmdlets do PowerShell são instalados para oferecer suporte a servidores de relatório no modo do SharePoint. Os cmdlets abrangem três categorias de funcionalidade.  
  
-   Instalação do serviço compartilhado e proxy do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint.  
  
-   Provisionando e gerenciamento de aplicativos de serviço [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e proxy associados.  
  
-   Gerenciamento de recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , por exemplo, extensões e chave de criptografia.  
  
||  
|-|  
|[!INCLUDE[applies](../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint Mode|  
  
 **Este tópico inclui o seguinte:**  
  
-   [Resumo do cmdlet](#bkmk_cmdlet_sum)  
  
-   [Cmdlets de serviço compartilhado e proxy](#bkmk_sharedservice_cmdlets)  
  
-   [Cmdlets de serviço de aplicativo e proxy](#bkmk_serviceapp_cmdlets)  
  
-   [Cmdlets de funcionalidade personalizada do Reporting Services](#bkmk_ssrsfeatures_cmdlets)  
  
-   [Amostras básicas](#bkmk_basic_samples)  
  
-   [Exemplos detalhados](#bkmk_detailedsamples)  
  
    -   [Criar um aplicativo de serviço Reporting Services e um proxy](#bkmk_example_create_service_application)  
  
    -   [Revisar e atualizar uma extensão de entrega de Reporting Services](#bkmk_example_delivery_extension)  
  
    -   [Obter e definir propriedades do banco de dados de aplicativo do Reporting Services, por exemplo, tempo limite do banco de dados](#bkmk_example_db_properties)  
  
    -   [Listar extensões de dados do Reporting Services – modo do SharePoint](#bkmk_example_list_data_extensions)  
  
    -   [Alterar e listar proprietários de assinatura](#bkmk_change_subscription_owner)  
  
##  <a name="bkmk_cmdlet_sum"></a> Resumo do cmdlet  

 Para executar os cmdlets, é necessário abrir o Shell de Gerenciamento do SharePoint. Você também pode usar o editor de interface gráfica do usuário incluído no Microsoft Windows, o **Ambiente de Script Integrado do Windows PowerShell (ISE)** . Para obter mais informações, consulte [Starting Windows PowerShell on Windows Server (Iniciando o Windows PowerShell no Windows Server)](https://docs.microsoft.com/powershell/scripting/getting-started/starting-windows-powershell). Nos resumos de cmdlets a seguir, as referências a ' bancos de dados ' do aplicativo de serviço referem-se a todos os bancos de dados criados e usados por um aplicativo de serviço [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Isso inclui a os bancos de dados de configuração, alerta e temp.  

  
 Se uma mensagem de erro semelhante à seguinte for exibida quando você digitar os exemplos do PowerShell:  
  
-   Install-SPRSService: o termo 'Install-SPRSService' não é reconhecido como  
    nome de cmdlet, função, arquivo de script ou programa operável. Verifique a ortografia do nome ou, se um caminho tiver sido incluído, verifique se ele está correto e tente novamente.  
  
 Um destes problemas está ocorrendo:  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não está instalado e, portanto, os cmdlets do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] também não estão instalados.  
  
-   Você executou o comando do PowerShell no Windows PowerShell ou no ISE do Windows PowerShell, e não no Shell de Gerenciamento do SharePoint. Use o Shell de Gerenciamento do SharePoint ou adicione o Snap-in do SharePoint à janela do Windows PowerShell com o seguinte comando:  
  
    ```powershell
    Add-PSSnapin Microsoft.SharePoint.PowerShell  
    ```  
  
 Para obter mais informações, consulte [usar o Windows PowerShell para administrar o SharePoint 2013](https://technet.microsoft.com/library/ee806878.aspx) (https://technet.microsoft.com/library/ee806878.aspx).  
  
#### <a name="to-open-the-sharepoint-management-shell-and-run-cmdlets"></a>Para abrir p Shell de Gerenciamento do SharePoint e executar cmdlets  
  
1.  Clique no botão **Iniciar**  
  
2.  Clique no grupo **Produtos do Microsoft SharePoint** .  
  
3.  Abra o **Shell de Gerenciamento do SharePoint**.  
  
 Para exibir a ajuda da linha de comando de um cmdlet, use o comando 'Get-Help' do PowerShell no prompt de comando do PowerShell. Por exemplo:  
  
 `Get-Help Get-SPRSServiceApplicationServers`  
  
###  <a name="bkmk_sharedservice_cmdlets"></a> Cmdlets de serviço compartilhado e proxy  
 A tabela a seguir contém os cmdlets PowerShell do serviço compartilhado [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint.  
  
|Cmdlet|Descrição|  
|------------|-----------------|  
|Install-SPRSService|Instala e registra, ou desinstala, o aplicativo do serviço compartilhado [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Só pode ser feito em um computador que tenha o SQL Server [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] instalado no modo integrado do SharePoint. Para instalação, há duas operações:<br /><br /> 1) o serviço de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] está instalado no farm.<br /><br /> 2) a instância do serviço de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] está instalada no computador atual.<br /><br /> Para desinstalação, há duas operações:<br />1) o serviço de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] é desinstalado do computador atual.<br />2) o serviço de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] é desinstalado do farm.<br /><br /> <br /><br /> OBSERVAÇÃO: se houver outros computadores no farm que tenham o serviço [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] instalado, ou se ainda houver aplicativos do serviço [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] em execução no farm, uma mensagem de aviso será exibida.|  
|Install-SPRSServiceProxy|Instala e registra, ou desinstala, o proxy do serviço Reporting Services no farm do SharePoint.|  
|Obtém-SPRSProxyUrl|Obtém as URLs para acessar o serviço [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .|  
|Get-SPRSServiceApplicationServers|Acessa todos os servidores no farm local do SharePoint que contém uma instalação do serviço compartilhado [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Esse cmdlet é útil para as atualizações do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , para determinar quais servidores executam o serviço compartilhado e, portanto, quais precisam ser atualizados.|  
  
###  <a name="bkmk_serviceapp_cmdlets"></a> Cmdlets de serviço de aplicativo e proxy  
 A tabela a seguir contém cmdlets PowerShell para aplicativos de serviço [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e seus proxies associados.  
  
|Cmdlet|Descrição|  
|------------|-----------------|  
|Get-SPRSServiceApplication|Obtém um ou mais objetos do aplicativo do serviço [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .|  
|New-SPRSServiceApplication|Cria um novo aplicativo do serviço Reporting Services e os bancos de dados associados.<br /><br /> Parâmetro LogonType: especifica se o servidor de relatório usa a conta do Pool de Aplicativos SSRS ou um logon do SQL Server para acessar o banco de dados do servidor de relatório. Pode ser um dos seguintes:<br /><br /> 0 Autenticação do Windows<br /><br /> 1 SQL Server<br /><br /> 2 Conta do pool de aplicativos (padrão)|  
|Remove-SPRSServiceApplication|Remove o aplicativo do serviço Reporting Services especificado. Isso também removerá os bancos de dados associados.|  
|Set-SPRSServiceApplication|Edita as propriedades de um aplicativo do serviço Reporting Services existente.|  
|New-SPRSServiceApplicationProxy|Cria um novo proxy do aplicativo do serviço Reporting Services.|  
|Get-SPRSServiceApplicationProxy|Obtém um ou mais proxies de aplicativo do serviço [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .|  
|Dismount-SPRSDatabase|Desmonta os bancos de dados do aplicativo de serviço de um aplicativo do serviço [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .|  
|Remove-SPRSDatabase|Remove os bancos de dados do aplicativo de serviço de um aplicativo do serviço [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .|  
|Set-SPRSDatabase|Define as propriedades dos bancos de dados associados a um aplicativo do serviço [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .|  
|Mount-SPRSDatabase|Monta bancos de dados para um aplicativo de serviço [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .|  
|New-SPRSDatabase|Cria novos bancos de dados do aplicativo de serviço para o aplicativo do serviço [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] especificado.|  
|Get-SPRSDatabaseCreationScript|Imprime o script de criação do banco de dados na tela do banco de dados de aplicativo do serviço [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Assim, você pode executar o script no SQL Server Management Studio.|  
|Get-SPRSDatabase|Obtém um ou mais proxies de bancos de dados do aplicativo do serviço [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Use o comando para obter a ID do banco de dados do aplicativo de serviço para que você possa usar o comdlet Set-SPRSDatabase para alterar as propriedades, por exemplo `querytimeout`. Veja os exemplos neste tópico, [Obter e definir propriedades do banco de dados do aplicativo Reporting Services, por exemplo, limite de banco de dados](#bkmk_example_db_properties).|  
|Get-SPRSDatabaseRightsScript|Imprime o script de direitos do banco de dados na tela do banco de dados de aplicativo do serviço [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . O usuário e o banco de dados desejados serão solicitados e o transact SQL que você pode executar para modificar permissões é retornado. Assim, você pode executar esse script no SQL Server Management Studio.|  
|Get-SPRSDatabaseUpgradeScript|Gera um script de atualização de banco de dados na tela. O script atualizará os bancos de dados do aplicativo de serviço [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para a versão do banco de dados da instalação atual do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .|  
  
###  <a name="bkmk_ssrsfeatures_cmdlets"></a> Cmdlets de funcionalidade personalizada do Reporting Services  
  
|Cmdlet|Descrição|  
|------------|-----------------|  
|Update-SPRSEncryptionKey|Atualiza a chave de criptografia do aplicativo do serviço Reporting Services especificado e recriptografa seus dados.|  
|Restore-SPRSEncryptionKey|Restaura a chave de criptografia com backup anterior para um aplicativo do serviço Reporting Services.|  
|Remove-SPRSEncryptedData|Exclui os dados criptografados do aplicativo do serviço Reporting Services especificado.|  
|Backup-SPRSEncryptionKey|Atualiza a chave de criptografia do aplicativo de serviço especificado do Reporting Services e recriptografa seus dados.|  
|New-SPRSExtension|Registra uma nova extensão com um aplicativo do serviço Reporting Services.|  
|Set-SPRSExtension|Define as propriedades de uma extensão existente do Reporting Services.|  
|Remove-SPRSExtension|Remove uma extensão de um aplicativo do serviço Reporting Services.|  
|Get-SPRSExtension|Obtém uma ou mais extensões do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para um aplicativo do serviço [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .<br /><br /> Os valores válidos são:<br /><br /> **Entrega**<br /><br /> **DeliveryUI**<br /><br /> **Render**<br /><br /> **Dados**<br /><br /> **Segurança**<br /><br /> **Autenticação**<br /><br /> **EventProcessing**<br /><br /> **ReportItems**<br /><br /> **Designer**<br /><br /> **ReportItemDesigner**<br /><br /> **ReportItemConverter**<br /><br /> **ReportDefinitionCustomization**|  
|Get-SPRSSite|Acessa sites do SharePoint com base na habilitação ou não do recurso "ReportingService". Por padrão, os sites que habilitam o recurso "ReportingService" são retornados.|  
  
##  <a name="bkmk_basic_samples"></a>Amostras básicas  
 Retorne uma lista de cmdlets que contém 'SPRS' no nome. Essa será a lista completa de cmdlets [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
```powershell
Get-command -noun *SPRS*  
```  
  
 Ou com um pouco mais de detalhes, conectada a um arquivo de texto denominado commandlist.txt  
  
```powershell
Get-Command -Noun *SPRS* | Select name, definition | Format-List | Out-File c:\commandlist.txt  
```  
  
 Instala o serviço e o proxy de serviço do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint.  
  
```powershell
Install-SPRSService  
```  
  
```powershell
Install-SPRSServiceProxy  
```  
  
 Inicie o serviço [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]  
  
```powershell
Get-SPServiceInstance -all | where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
```  
  
 Digite o seguinte comando do SharePoint Management Shell para retornar uma lista filtrada de linhas de um arquivo de log. O comando filtrará por linhas que contêm "ssrscustomactionerror". Este exemplo examina o arquivo de log criado quando o rssharepoint.msi foi instalado.  
  
```powershell
Get-Content -Path C:\Users\testuser\AppData\Local\Temp\rs_sp_0.log | Select-String "ssrscustomactionerror"  
```  
  
##  <a name="bkmk_detailedsamples"></a>Exemplos detalhados  
 Além das amostras a seguir, confira a seção "Script do Windows PowerShell" no tópico [Scripts do Windows PowerShell para as Etapas 1 a 4](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md#bkmk_full_script).  
  
###  <a name="bkmk_example_create_service_application"></a>Criar um aplicativo de serviço Reporting Services e um proxy  
 Este script de exemplo conclui as tarefas seguintes:  
  
1.  Cria um aplicativo de serviço e proxy Reporting Services. O script supõe que o pool de aplicativos "My App Pool" já existe.  
  
2.  Adicione o proxy ao grupo proxy padrão.  
  
3.  Permita para o aplicativo de serviço o acesso ao banco de dados de conteúdo do aplicativo Web na porta 80. O script pressupõe que o site "http://sitename" já existe.  
  
```powershell
# Create service application and service application proxy  
$appPool = Get-SPServiceApplicationPool "My App Pool"  
$serviceApp = New-SPRSServiceApplication "My RS Service App" -ApplicationPool $appPool  
$serviceAppProxy = New-SPRSServiceApplicationProxy -Name "My RS Service App Proxy" -ServiceApplication $serviceApp  
  
# Add service application proxy to default proxy group.  Any web application that uses the default proxy group will now be able to use this service application.  
Get-SPServiceApplicationProxyGroup -default | Add-SPServiceApplicationProxyGroupMember -Member $serviceAppProxy  
  
# Grant application pool account access to the port 80 web application's content database.  
$webApp = Get-SPWebApplication "http://sitename"  
$appPoolAccountName = $appPool.ProcessAccount.LookupName()  
$webApp.GrantAccessToProcessIdentity($appPoolAccountName)
```  
  
###  <a name="bkmk_example_delivery_extension"></a>Revisar e atualizar uma extensão de entrega de Reporting Services  
 O exemplo de script PowerShell a seguir atualiza a configuração completa da extensão de entrega de email do servidor de relatório para o aplicativo de serviço denominado `My RS Service App`. Atualize os valores do servidor SMTP (`<email server name>`) e o alias de email FROM (`<your FROM email address>`).  
  
```powershell
$app = Get-SPRSServiceApplication -Name "My RS Service App"  
$emailCfg = Get-SPRSExtension -Identity $app -ExtensionType "Delivery" -Name "Report Server Email" | Select -ExpandProperty ConfigurationXml
$emailXml = [xml]$emailCfg
$emailXml.SelectSingleNode("//SMTPServer").InnerText = "<email server name>"  
$emailXml.SelectSingleNode("//SendUsing").InnerText = "2"  
$emailXml.SelectSingleNode("//SMTPAuthenticate").InnerText = "2"  
$emailXml.SelectSingleNode("//From").InnerText = '<your FROM email address>'  
Set-SPRSExtension -Identity $app -ExtensionType "Delivery" -Name "Report Server Email" -ExtensionConfiguration $emailXml.OuterXml  
```  
  
 No exemplo acima, se você não sabia o nome exato do aplicativo de serviço, poderia reescrever a primeira instrução para obter o aplicativo de serviço com base em uma pesquisa de nome parcial. Por exemplo:  
  
```powershell
$app = Get-SPRSServiceApplication | Where {$_.name -like " ssrs_testapp *"}  
```  
  
 O script a seguir retornará os valores de configuração atuais da extensão de entrega de email do servidor de relatório para o aplicativo de serviço denominado “Aplicativo Reporting Services”. A primeira etapa define o valor da variável $app para o objeto do aplicativo de serviço denominado "My RS Service App"  
  
 A segunda instrução obterá a extensão de entrega 'Report Server Email' para o objeto de aplicativo de serviço na variável $app e selecionará configurationXML  
  
```powershell
$app = Get-SPRSServiceapplication -Name "Reporting Services Application"  
Get-SPRSExtension -Identity $app -ExtensionType "Delivery" -Name "Report Server Email" | Select -ExpandProperty ConfigurationXml  
```  
  
 Você também pode reescrever as duas instruções acima como se fossem uma:  
  
```powershell
Get-SPRSServiceApplication -Name "Reporting Services Application" | Get-SPRSExtension -ExtensionType "Delivery" -Name "Report Server Email" | Select -ExpandProperty ConfigurationXml  
```  
  
###  <a name="bkmk_example_db_properties"></a>Obter e definir propriedades do banco de dados de aplicativo do Reporting Services, por exemplo, tempo limite do banco de dados  
 O exemplo a seguir primeiro retorna uma lista dos bancos de dados e propriedades para que seja possível determinar o guid do banco de dados (ID) que você fornecerá para o comando set. Para obter uma lista completa das propriedades, consulte `Get-SPRSDatabase | format-list`.  
  
```powershell
Get-SPRSDatabase | Select id, querytimeout,connectiontimeout, status, server, ServiceInstance
```  
  
 O item a seguir é um exemplo de saída. Determine a ID para o banco de dados que você deseja modificar e use a ID no cmdlet SET.  
  
-   `Id                : 56f8d1bc-cb04-44cf-bd41-a873643c5a14`  
  
     `QueryTimeout      : 120`  
  
     `ConnectionTimeout : 15`  
  
     `Status            : Online`  
  
     `Server            : SPServer Name=uetestb01`  
  
     `ServiceInstance   : SPDatabaseServiceInstance`  
  
```powershell
Set-SPRSDatabase -Identity 56f8d1bc-cb04-44cf-bd41-a873643c5a14 -QueryTimeout 300  
```  
  
 Para verificar se o valor está definido, execute o cmdlet GET novamente.  
  
```powershell
Get-SPRSDatabase -Identity 56f8d1bc-cb04-44cf-bd41-a873643c5a14 | Select id, querytimeout,connectiontimeout, status, server, ServiceInstance  
```  
  
###  <a name="bkmk_example_list_data_extensions"></a>Listar extensões de dados do Reporting Services – modo do SharePoint  
 O exemplo a seguir executa um loop em cada aplicativo de serviço do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e lista as extensões de dados atuais de cada um deles.  
  
```powershell
$apps = Get-SPRSServiceApplication  
foreach ($app in $apps)
{  
Write-host -ForegroundColor "yellow" Service App Name $app.Name  
Get-SPRSExtension -identity $app -ExtensionType "Data" | select name, extensiontype | Format-Table -AutoSize  
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
  
###  <a name="bkmk_change_subscription_owner"></a>Alterar e listar proprietários de assinatura  
 Consulte [Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription](subscriptions/manage-subscription-owners-and-run-subscription-powershell.md).  
  
## <a name="see-also"></a>Consulte também  
 [Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription](subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)   
 [Lista de verificação: Use o PowerShell para verificar PowerPivot para SharePoint](https://docs.microsoft.com/analysis-services/instances/install-windows/checklist-use-powershell-to-verify-power-pivot-for-sharepoint)   
 [Scripts do PowerShell de gerenciamento do SharePoint para CodePlex](http://sharepointpsscripts.codeplex.com/)   
 [Como administrar o SSRS usando o PowerShell](https://curatedviews.cloudapp.net/13107/how-to-administer-ssrs-using-powershell)  
