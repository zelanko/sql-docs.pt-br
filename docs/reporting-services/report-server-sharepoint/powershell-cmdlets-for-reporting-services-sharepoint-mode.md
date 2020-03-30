---
title: Cmdlets do PowerShell para o modo do SharePoint do Reporting Services | Microsoft Docs
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 3e415fee08a9723419c7d8a4258fc88670c5e262
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "68892401"
---
# <a name="powershell-cmdlets-for-reporting-services-sharepoint-mode"></a>Cmdlets do PowerShell para o modo do SharePoint do Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Quando você instala o modo do SharePoint do SQL Server 2016 Reporting Services, os cmdlets do PowerShell são instalados para dar suporte aos Servidores de relatório no modo do SharePoint. Os cmdlets abrangem três categorias de funcionalidade.  
  
-   Instalação do serviço compartilhado e proxy do SharePoint do Reporting Services.  
  
-   Provisionamento e gerenciamento de aplicativos de serviço do Reporting Services e proxies associados.  
  
-   Gerenciamento de recursos do Reporting Services, por exemplo, extensões e chaves de criptografia.  

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.

## <a name="cmdlet-summary"></a>Resumo do cmdlet

 Para executar os cmdlets, é necessário abrir o Shell de Gerenciamento do SharePoint. Você também pode usar o editor de interface gráfica do usuário incluído no Microsoft Windows, o **Ambiente de Script Integrado do Windows PowerShell (ISE)** . Para obter mais informações, consulte [Starting Windows PowerShell on Windows Server (Iniciando o Windows PowerShell no Windows Server)](https://docs.microsoft.com/powershell/scripting/getting-started/starting-windows-powershell). Nos resumos de cmdlet a seguir, as referências a ‘bancos de dados’ do aplicativo de serviço referem-se a todos os bancos de dados criados e usados por um aplicativo de serviço do Reporting Services. Isso inclui a os bancos de dados de configuração, alerta e temp.  
  
 Se uma mensagem de erro semelhante à seguinte for exibida quando você digitar os exemplos do PowerShell:  
  
-   Install-SPRSService: o termo 'Install-SPRSService' não é reconhecido como  
    nome de cmdlet, função, arquivo de script ou programa operável. Verifique a ortografia do nome ou se um caminho foi incluído, verifique se ele está correto e tente novamente.  
  
 Um destes problemas está ocorrendo:  
  
-   O modo do SharePoint do Reporting Services não está instalado e, portanto, os cmdlets do Reporting Services não estão instalados.  
  
-   Você executou o comando do PowerShell no Windows PowerShell ou no ISE do Windows PowerShell, e não no Shell de Gerenciamento do SharePoint. Use o Shell de Gerenciamento do SharePoint ou adicione o Snap-in do SharePoint à janela do Windows PowerShell com o seguinte comando:  
  
    ```  
    Add-PSSnapin Microsoft.SharePoint.PowerShell  
    ```  
  
 Para obter mais informações, consulte [Usar o Windows PowerShell para administrar o SharePoint 2013](https://technet.microsoft.com/library/ee806878.aspx).  
  
### <a name="open-the-sharepoint-management-shell-and-run-cmdlets"></a>Abrir o Shell de Gerenciamento do SharePoint e executar cmdlets
  
1.  Clique no botão **Iniciar**  
  
2.  Clique no grupo **Produtos do Microsoft SharePoint** .  
  
3.  Abra o **Shell de Gerenciamento do SharePoint**.  
  
 Para exibir a ajuda da linha de comando de um cmdlet, use o comando 'Get-Help' do PowerShell no prompt de comando do PowerShell. Por exemplo:  
  
 `Get-Help Get-SPRSServiceApplicationServers`  
  
##  <a name="shared-service-and-proxy-cmdlets"></a>Cmdlets de serviço compartilhado e proxy

 A tabela a seguir contém os cmdlets do PowerShell do serviço compartilhado SharePoint e Reporting Services.  
  
|Cmdlet|DESCRIÇÃO|  
|------------|-----------------|  
|Install-SPRSService|Instala e registra, ou desinstala, o serviço compartilhado Reporting Services. Isso só pode ser feito em um computador que tem o SQL Server Reporting Services instalado no modo do SharePoint. Para instalação, há duas operações:<br /><br /> \- O serviço Reporting Services é instalado no farm.<br /><br /> \- A instância do serviço Reporting Services é instalada no computador atual.<br /><br /> Para desinstalação, há duas operações:<br /><br /> \- O serviço Reporting Services é desinstalado do computador atual.<br /><br /> \- O serviço Reporting Services é desinstalado do farm.<br /><br /> <br /><br /> Se houver outros computadores no farm que têm o serviço Reporting Services instalado ou, se ainda houver aplicativos de serviço Reporting Services em execução no farm, será exibida uma mensagem de aviso.|  
|Install-SPRSServiceProxy|Instala e registra, ou desinstala, o proxy do serviço Reporting Services no farm do SharePoint.|  
|Obtém-SPRSProxyUrl|Obtém a(s) URL(s) de acesso ao serviço do Reporting Services.|  
|Get-SPRSServiceApplicationServers|Acessa todos os servidores no farm local do SharePoint que contém uma instalação do serviço compartilhado Reporting Services. Esse cmdlet é útil para upgrades do Reporting Services, para determinar quais servidores executam o serviço compartilhado e, portanto, quais precisam ser atualizados.|  
  
## <a name="service-application-and-proxy-cmdlets"></a>Cmdlets de aplicativo de serviço e proxy

 A tabela a seguir contém cmdlets do PowerShell para aplicativos do serviço Reporting Services e seus proxies associados.  
  
|cmdlet|DESCRIÇÃO|  
|------------|-----------------|  
|Get-SPRSServiceApplication|Obtém um ou mais objetos de aplicativo do serviço Reporting Services.|  
|New-SPRSServiceApplication|Cria um novo aplicativo do serviço Reporting Services e os bancos de dados associados.<br /><br /> Parâmetro LogonType: especifica se o servidor de relatório usa a conta do Pool de Aplicativos do SSRS ou um logon do SQL Server para acessar o banco de dados do servidor de relatório. Os valores válidos são:<br /><br /> 0 Autenticação do Windows<br /><br /> 1 SQL Server<br /><br /> 2 Conta do pool de aplicativos (padrão)|  
|Remove-SPRSServiceApplication|Remove o aplicativo do serviço Reporting Services especificado. Isso também removerá os bancos de dados associados.|  
|Set-SPRSServiceApplication|Edita as propriedades de um aplicativo do serviço Reporting Services existente.|  
|New-SPRSServiceApplicationProxy|Cria um novo proxy do aplicativo do serviço Reporting Services.|  
|Get-SPRSServiceApplicationProxy|Obtém um ou mais proxies de aplicativo do serviço Reporting Services.|  
|Dismount-SPRSDatabase|Desmonta os bancos de dados do aplicativo de serviço de um aplicativo do serviço Reporting Services.|  
|Remove-SPRSDatabase|Remove os bancos de dados do aplicativo de serviço de um aplicativo do serviço Reporting Services.|  
|Set-SPRSDatabase|Define as propriedades dos bancos de dados associados a um aplicativo do serviço Reporting Services.|  
|Mount-SPRSDatabase|Monta os bancos de dados de um aplicativo do serviço Reporting Services.|  
|New-SPRSDatabase|Cria novos bancos de dados do aplicativo de serviço para o aplicativo do serviço Reporting Services especificado.|  
|Get-SPRSDatabaseCreationScript|Gera o script de criação de banco de dados na tela de um aplicativo do serviço Reporting Services. Assim, você pode executar o script no SQL Server Management Studio.|  
|Get-SPRSDatabase|Obtém um ou mais bancos de dados de aplicativo do serviço Reporting Services. Use o comando para obter a ID do banco de dados do aplicativo de serviço para que você possa usar o comdlet Set-SPRSDatabase para alterar as propriedades, por exemplo `querytimeout`. Veja o exemplo neste tópico, [Obter e definir propriedades do Banco de dados do aplicativo Reporting Services](#get-and-set-properties-of-the-reporting-service-application-database).|  
|Get-SPRSDatabaseRightsScript|Gera o script de direitos de banco de dados na tela de um aplicativo do serviço Reporting Services. O usuário e o banco de dados desejados serão solicitados e o transact SQL que você pode executar para modificar permissões é retornado. Assim, você pode executar esse script no SQL Server Management Studio.|  
|Get-SPRSDatabaseUpgradeScript|Gera um script de atualização de banco de dados na tela. O script atualizará os bancos de dados do aplicativo do serviço Reporting Services para a versão de banco de dados da instalação atual do Reporting Services.|  
  
## <a name="reporting-services-custom-functionality-cmdlets"></a>Cmdlets de funcionalidade personalizada do Reporting Services
  
|Cmdlet|DESCRIÇÃO|  
|------------|-----------------|  
|Update-SPRSEncryptionKey|Atualiza a chave de criptografia do aplicativo do serviço Reporting Services especificado e recriptografa seus dados.|  
|Restore-SPRSEncryptionKey|Restaura a chave de criptografia com backup anterior para um aplicativo do serviço Reporting Services.|  
|Remove-SPRSEncryptedData|Exclui os dados criptografados do aplicativo do serviço Reporting Services especificado.|  
|Backup-SPRSEncryptionKey|Atualiza a chave de criptografia do aplicativo de serviço especificado do Reporting Services e recriptografa seus dados.|  
|New-SPRSExtension|Registra uma nova extensão com um aplicativo do serviço Reporting Services.|  
|Set-SPRSExtension|Define as propriedades de uma extensão existente do Reporting Services.|  
|Remove-SPRSExtension|Remove uma extensão de um aplicativo do serviço Reporting Services.|  
|Get-SPRSExtension|Obtém uma ou mais extensões do Reporting Services para um aplicativo do serviço Reporting Services.<br /><br /> Os valores válidos são:<br /><br /> <br /><br /> Entrega<br /><br /> DeliveryUI<br /><br /> Renderizar<br /><br /> data<br /><br /> Segurança<br /><br /> Autenticação<br /><br /> EventProcessing<br /><br /> ReportItems<br /><br /> Designer<br /><br /> ReportItemDesigner<br /><br /> ReportItemConverter<br /><br /> ReportDefinitionCustomization|  
|Get-SPRSSite|Acessa sites do SharePoint com base na habilitação ou não do recurso "ReportingService". Por padrão, os sites que habilitam o recurso "ReportingService" são retornados.|  
  
## <a name="basic-samples"></a>Amostras básicas

 Retorne uma lista de cmdlets que contém 'SPRS' no nome. Esta será a lista completa de cmdlets do Reporting Services.  
  
```  
Get-command -noun *SPRS*  
```  
  
 Ou com um pouco mais de detalhes, conectada a um arquivo de texto denominado commandlist.txt  
  
```  
Get-command -noun *SPRS* | Select name, definition | Format-List | Out-File c:\commandlist.txt  
```  
  
 Instale o serviço SharePoint do Reporting Services e o proxy de serviço.  
  
```  
Install-SPRSService  
```  
  
```  
Install-SPRSServiceProxy  
```  
  
 Iniciar o serviço Reporting Services  
  
```  
get-spserviceinstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
```  
  
 Digite o seguinte comando do SharePoint Management Shell para retornar uma lista filtrada de linhas de um arquivo de log. O comando filtrará por linhas que contêm "ssrscustomactionerror". Este exemplo examina o arquivo de log criado quando o rssharepoint.msi foi instalado.  
  
```  
Get-content -path C:\Users\testuser\AppData\Local\Temp\rs_sp_0.log | select-string "ssrscustomactionerror"  
```  
  
## <a name="detailed-samples"></a>Amostras detalhadas

 Além das amostras a seguir, confira a seção "Script do Windows PowerShell" no tópico [Scripts do Windows PowerShell para as Etapas 1 a 4](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md#bkmk_full_script).  
  
### <a name="create-a-reporting-services-service-application-and-proxy"></a>Cria um aplicativo de serviço e proxy Reporting Services

 Este script de exemplo conclui as tarefas seguintes:  
  
1.  Cria um aplicativo de serviço e proxy Reporting Services. O script supõe que o pool de aplicativos "My App Pool" já existe.  
  
2.  Adicione o proxy ao grupo proxy padrão.  
  
3.  Permita para o aplicativo de serviço o acesso ao banco de dados de conteúdo do aplicativo Web na porta 80. O script pressupõe que o site `https://sitename` já exista.  
  
```  
# Create service application and service application proxy  
$appPool = Get-SPServiceApplicationPool "My App Pool"  
$serviceApp = New-SPRSServiceApplication "My RS Service App" -ApplicationPool $appPool  
$serviceAppProxy = New-SPRSServiceApplicationProxy -Name "My RS Service App Proxy" -ServiceApplication $serviceApp  
  
# Add service application proxy to default proxy group.  Any web application that uses the default proxy group will now be able to use this service application.  
Get-SPServiceApplicationProxyGroup -default | Add-SPServiceApplicationProxyGroupMember -Member $serviceAppProxy  
  
# Grant application pool account access to the port 80 web application's content database.  
$webApp = Get-SPWebApplication "https://sitename"  
$appPoolAccountName = $appPool.ProcessAccount.LookupName()  
$webApp.GrantAccessToProcessIdentity($appPoolAccountName)  
  
```  
  
### <a name="review-and-update-a-reporting-services-delivery-extension"></a>Examinar e atualizar uma extensão de entrega do Reporting Services

 O exemplo de script PowerShell a seguir atualiza a configuração completa da extensão de entrega de email do servidor de relatório para o aplicativo de serviço denominado `My RS Service App`. Atualize os valores do servidor SMTP (`<email server name>`) e o alias de email FROM (`<your FROM email address>`).  
  
```  
$app=get-sprsserviceapplication -Name "My RS Service App"  
$emailCfg = Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml   
$emailXml = [xml]$emailCfg   
$emailXml.SelectSingleNode("//SMTPServer").InnerText = "<email server name>"  
$emailXml.SelectSingleNode("//SendUsing").InnerText = "2"  
$emailXml.SelectSingleNode("//SMTPAuthenticate").InnerText = "2"  
$emailXml.SelectSingleNode("//From").InnerText = '<your FROM email address>'  
Set-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" -ExtensionConfiguration $emailXml.OuterXml  
```  
  
 No exemplo acima, se você não sabia o nome exato do aplicativo de serviço, poderia reescrever a primeira instrução para obter o aplicativo de serviço com base em uma pesquisa de nome parcial. Por exemplo:  
  
```  
$app=get-sprsserviceapplication | where {$_.name -like " ssrs_testapp *"}  
```  
  
 O script a seguir retornará os valores de configuração atuais da extensão de entrega de email do servidor de relatório para o aplicativo de serviço denominado “Aplicativo Reporting Services”. A primeira etapa define o valor da variável $app para o objeto do aplicativo de serviço denominado "My RS Service App"  
  
 A segunda instrução obterá a extensão de entrega 'Report Server Email' para o objeto de aplicativo de serviço na variável $app e selecionará configurationXML  
  
```  
$app=get-sprsserviceapplication -Name "Reporting Services Application"  
Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml  
```  
  
 Você também pode reescrever as duas instruções acima como se fossem uma:  
  
```  
get-sprsserviceapplication -Name "Reporting Services Application" | Get-SPRSExtension -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml  
```  
  
### <a name="get-and-set-properties-of-the-reporting-service-application-database"></a>Obter e definir as propriedades do banco de dados de aplicativo do Reporting Services

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
Set-SPRSDatabase -identity 56f8d1bc-cb04-44cf-bd41-a873643c5a14 -QueryTimeout 300  
```  
  
 Para verificar se o valor está definido, execute o cmdlet GET novamente.  
  
```  
Get-SPRSDatabase -identity 56f8d1bc-cb04-44cf-bd41-a873643c5a14 | select id, querytimeout,connectiontimeout, status, server, ServiceInstance  
```  
  
### <a name="list-reporting-services-data-extensions"></a>Listar extensões de dados do Microsoft Reporting Services

 O exemplo a seguir executa um loop em cada aplicativo do serviço Reporting Services e lista as extensões de dados atuais de cada um.  
  
```  
$apps = Get-SPRSServiceApplication  
foreach ($app in $apps)   
{  
Write-host -ForegroundColor "yellow" Service App Name $app.Name  
Get-SPRSExtension -identity $app -ExtensionType "Data" | select name,extensiontype | Format-Table -AutoSize  
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
  
### <a name="change-and-list-reporting-services-subscription-owners"></a>Alterar e listar proprietários de assinaturas do Reporting Services

 Consulte [Usar o PowerShell para alterar e listar os proprietários da assinatura do Reporting Services e executar uma assinatura](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md).  
  
## <a name="next-steps"></a>Próximas etapas

[Usar o PowerShell para alterar e listar os proprietários da assinatura do Reporting Services e executar uma assinatura](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
[Lista de verificação: Usar o PowerShell para verificar o Power Pivot para SharePoint](https://docs.microsoft.com/analysis-services/instances/install-windows/checklist-use-powershell-to-verify-power-pivot-for-sharepoint)   
[Obter ajuda para o PowerShell do SQL Server](../../relational-databases/scripting/get-help-sql-server-powershell.md)   

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
