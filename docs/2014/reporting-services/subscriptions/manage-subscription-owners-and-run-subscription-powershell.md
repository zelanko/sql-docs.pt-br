---
title: Use o PowerShell para alterar e listar proprietários de assinaturas do Reporting Services e executar uma assinatura | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 0fa6cb36-68fc-4fb8-b1dc-ae4f12bf6ff0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 53fc7b585edf852d04256c9e85fa0bd96aa7eced
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59960892"
---
# <a name="use-powershell-to-change-and-list-reporting-services-subscription-owners-and-run-a-subscription"></a>Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription
  A partir do [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] , você pode transferir de forma programática a propriedade de uma assinatura do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] de um usuário para outro. Este tópico fornece vários scripts do Windows PowerShell que você pode usar para mudar ou simplesmente listar a propriedade das assinaturas. Cada amostra inclui a sintaxe de amostra do modo Nativo e do modo SharePoint. Após mudar o proprietário da assinatura, está será executada no contexto de segurança do novo proprietário, e o campo User!UserID no relatório exibirá o valor do novo proprietário. Para obter mais informações sobre o modelo de objeto que as amostras do PowerShell chamam, consulte <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>  
  
 ![Conteúdo relacionado ao PowerShell](../media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell")  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] Modo nativo &#124; [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] Modo do SharePoint|  
  
 **Neste tópico:**  
  
-   [Como usar os scripts](#bkmk_how_to)  
  
-   [Script: Listar a propriedade de todas as assinaturas](#bkmk_list_ownership_all)  
  
-   [Script: Listar todas as assinaturas pertencentes a um usuário específico](#bkmk_list_all_one_user)  
  
-   [Script: Alterar a propriedade de todas as assinaturas pertencentes a um usuário específico](#bkmk_change_all)  
  
-   [Script: Lista todas as assinaturas associadas a um relatório específico](#bkmk_list_for_1_report)  
  
-   [Script: Alterar a propriedade de uma assinatura específica](#bkmk_change_all_1_subscription)  
  
-   [Script: Executar (acionar) uma única assinatura](#bkmk_run_1_subscription)  
  
##  <a name="bkmk_how_to"></a> Como usar os scripts  
  
### <a name="permissions"></a>Permissões  
 Esta seção resume os níveis de permissão necessários para usar cada um dos métodos para o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]em modo Nativo e SharePoint. Os scripts neste tópico usam os seguintes métodos [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] :  
  
-   [Método ReportingService2010.ListSubscriptions](https://technet.microsoft.com/library/reportservice2010.reportingservice2010.listsubscriptions.aspx)  
  
-   [Método ReportingService2010.ChangeSubscriptionOwner](https://technet.microsoft.com/library/reportservice2010.reportingservice2010.changesubscriptionowner.aspx)  
  
-   [ReportingService2010.ListChildren](https://technet.microsoft.com/library/reportservice2010.reportingservice2010.listchildren.aspx)  
  
-   O método [ReportingService2010.FireEvent](https://technet.microsoft.com/library/reportservice2010.reportingservice2010.fireevent.aspx) é usado apenas no último script para disparar uma assinatura específica a ser executada. Se você não planeja usar esse script, é possível ignorar os requisitos de permissão para o método FireEvent.  
  
 **Modo Nativo:**  
  
-   Listar assinaturas: (HYPERLINK "https://technet.microsoft.com/library/microsoft.reportingservices.interfaces.reportoperation.aspx" ReadSubscription no relatório e o usuário é o proprietário da assinatura) ou ReadAnySubscription  
  
-   Alterar assinaturas: O usuário deve ser um membro do grupo BUILTIN\Administrators  
  
-   Listar filhos: ReadProperties no Item  
  
-   Acionar evento: GenerateEvents (System)  
  
 **Modo SharePoint:**  
  
-   Listar assinaturas: ManageAlerts ou (HYPERLINK "https://technet.microsoft.com/library/microsoft.sharepoint.spbasepermissions.aspx" CreateAlerts no relatório e o usuário é o proprietário da assinatura e a assinatura é cronometrada).  
  
-   Alterar assinaturas: ManageWeb  
  
-   Listar filhos: ViewListItems  
  
-   Acionar evento: ManageWeb  
  
 Para obter mais informações, consulte [Comparar funções e tarefas no Reporting Services com grupos e permissões do SharePoint](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md).  
  
### <a name="script-usage"></a>Uso de script  
 **Criar arquivos de script (.ps1)**  
  
1.  Crie uma pasta chamada **c:\scripts**. Se você escolher uma pasta diferente, mude o nome da pasta usado nas instruções de sintaxe da linha de comando do exemplo.  
  
2.  Crie um arquivo de texto para cada script e salve os arquivos na pasta c:\scripts. Quando criar os arquivos .ps1, use o nome de cada sintaxe de linha de comando do exemplo.  
  
3.  Abra um prompt de comando com privilégios administrativos.  
  
4.  Execute cada arquivo de script, usando a respectiva sintaxe de linha de comando de exemplo fornecida.  
  
 **Ambientes testados**  
  
 Os scripts neste tópico foram testados no PowerShell versão 3 e com as seguintes versões do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]:  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]  
  
##  <a name="bkmk_list_ownership_all"></a> Script: Listar a propriedade de todas as assinaturas  
 Esse script lista todas as assinaturas em um site. Você pode usar esse script para testar sua conexão ou para verificar o caminho do relatório e a identificação de assinatura para uso em outros scripts. Ele também é um script útil para simplesmente auditar as assinaturas existentes e seus proprietários.  
  
 **Sintaxe do modo Nativo:**  
  
```  
powershell c:\scripts\ListAll_SSRS_Subscriptions.ps1 "[server]/reportserver" "/"  
```  
  
 **Sintaxe do modo SharePoint:**  
  
```  
powershell c:\scripts\ListAll_SSRS_Subscriptions.ps1 "[server]/_vti_bin/reportserver" "http://[server]"  
```  
  
 **Script:**  
  
```  
# Parameters  
#    server   - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
  
Param(  
    [string]$server,  
    [string]$site  
   )  
  
$rs2010 += New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
$subscriptions += $rs2010.ListSubscriptions($site); # use "/" for default native mode site  
  
Write-Host " "  
Write-Host "----- $server's Subscriptions: "  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted, Status  
```  
  
> [!TIP]  
>  Para verificar URLs de sites no modo do SharePoint, use o cmdlet **Get-SPSite**do SharePoint. Para obter mais informações, consulte [Get-SPSite](https://technet.microsoft.com/library/ff607950\(v=office.15\).aspx).  
  
##  <a name="bkmk_list_all_one_user"></a> Script: Listar todas as assinaturas pertencentes a um usuário específico  
 Esse script lista todas as assinaturas de propriedade de um usuário específico. Você pode usar esse script para testar sua conexão ou para verificar o caminho do relatório e a identificação de assinatura para uso em outros scripts. Esse script é útil quando alguém sai da organização e você deseja verificar quais assinaturas essa pessoa possuía para alterar o proprietário ou excluir a assinatura.  
  
 **Sintaxe do modo Nativo:**  
  
```  
powershell c:\scripts\ListAll_SSRS_Subscriptions4User.ps1 "[Domain]\[user]" "[server]/reportserver" "/"  
```  
  
 **Sintaxe do modo SharePoint:**  
  
```  
powershell c:\scripts\ListAll_SSRS_Subscriptions4User.ps1 "[Domain]\[user]"  "[server]/_vti_bin/reportserver" "http://[server]"  
```  
  
 **Script:**  
  
```  
# Parameters:  
#    currentOwner - DOMAIN\USER that owns the subscriptions you wish to change  
#    server        - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
#    site        - use "/" for default native mode site  
Param(  
    [string]$currentOwner,  
    [string]$server,  
    [string]$site  
)  
  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
$subscriptions += $rs2010.ListSubscriptions($site);  
  
Write-Host " "  
Write-Host " "  
Write-Host "----- $currentOwner's Subscriptions: "  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status | where {$_.owner -eq $currentOwner}  
```  
  
##  <a name="bkmk_change_all"></a> Script: Alterar a propriedade de todas as assinaturas pertencentes a um usuário específico  
 Esse script muda a propriedade de todas as assinaturas de um usuário específico para o parâmetro do novo proprietário.  
  
 **Sintaxe do modo Nativo:**  
  
```  
powershell c:\scripts\ChangeALL_SSRS_SubscriptionOwner.ps1 "[Domain]\current owner]" "[Domain]\[new owner]" "[server]/reportserver"  
```  
  
 **Sintaxe do modo SharePoint:**  
  
```  
powershell c:\scripts\ChangeALL_SSRS_SubscriptionOwner.ps1 "[Domain]\{current owner]" "[Domain]\[new owner]" "[server]/_vti_bin/reportserver"  
```  
  
 **Script:**  
  
```  
# Parameters:  
#    currentOwner - DOMAIN\USER that owns the subscriptions you wish to change  
#    newOwner      - DOMAIN\USER that will own the subscriptions you wish to change  
#    server        - server and instance name (e.g. myserver/reportserver, myserver/reportserver_db2, myserver/_vti_bin/reportserver)  
  
Param(  
    [string]$currentOwner,  
    [string]$newOwner,  
    [string]$server  
)  
  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
$items = $rs2010.ListChildren("/", $true);  
  
$subscriptions = @();  
  
ForEach ($item in $items)  
{  
    if ($item.TypeName -eq "Report")  
    {  
        $curRepSubs = $rs2010.ListSubscriptions($item.Path);  
        ForEach ($curRepSub in $curRepSubs)  
        {  
            if ($curRepSub.Owner -eq $previousOwner)  
            {  
                $subscriptions += $curRepSub;  
            }  
        }  
    }  
}  
  
Write-Host " "  
Write-Host " "  
Write-Host -foregroundcolor "green" "-----  $currentOwner's Subscriptions changing ownership to $newOwner : "  
$subscriptions | select SubscriptionID, Owner, Path, Description,  Status  | format-table -AutoSize  
  
ForEach ($sub in $subscriptions)  
{  
    $rs2010.ChangeSubscriptionOwner($sub.SubscriptionID, $newOwner);  
}  
  
$subs2 = @();  
  
ForEach ($item in $items)  
{  
    if ($item.TypeName -eq "Report")  
    {  
        $subs2 += $rs2010.ListSubscriptions($item.Path);  
    }  
}  
```  
  
##  <a name="bkmk_list_for_1_report"></a> Script: Lista todas as assinaturas associadas a um relatório específico  
 Esse script lista todas as assinaturas associadas a um relatório específico. A sintaxe do caminho do relatório é um modo SharePoint diferente que exige uma URL completa. Nos exemplos de sintaxe, o nome do relatório usado é "somente título", que contém um espaço e, portanto, requer aspas simples em torno do nome do relatório.  
  
 **Sintaxe do modo Nativo:**  
  
```  
powershell c:\scripts\List_SSRS_One_Reports_Subscriptions.ps1 "[server]/reportserver" "'/reports/title only'" "/"  
```  
  
 **Sintaxe do modo SharePoint:**  
  
```  
powershell c:\scripts\List_SSRS_One_Reports_Subscriptions.ps1 "[server]/_vti_bin/reportserver"  "'http://[server]/shared documents/title only.rdl'" "http://[server]"  
```  
  
 **Script:**  
  
```  
# Parameters:  
#    server      - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
#    reportpath  - path to report in the report server, including report name e.g. /reports/test report >> pass in  "'/reports/title only'"  
#    site        - use "/" for default native mode site  
Param  
(  
      [string]$server,  
      [string]$reportpath,  
      [string]$site  
)  
  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
$subscriptions += $rs2010.ListSubscriptions($site);  
  
Write-Host " "  
Write-Host " "  
Write-Host "----- $reportpath 's Subscriptions: "  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status | where {$_.path -eq $reportpath}  
```  
  
##  <a name="bkmk_change_all_1_subscription"></a> Script: Alterar a propriedade de uma assinatura específica  
 Esse script altera a propriedade de uma assinatura específica. A assinatura é identificada pela SubscriptionID que você passa no script. Você pode usar um dos scripts de assinatura da lista para determinar a SubscriptionID correta.  
  
 **Sintaxe do modo Nativo:**  
  
```  
powershell c:\scripts\Change_SSRS_Owner_One_Subscription.ps1 "[Domain]\[new owner]" "[server]/reportserver" "/" "ac5637a1-9982-4d89-9d69-a72a9c3b3150"  
```  
  
 **Sintaxe do modo SharePoint:**  
  
```  
powershell c:\scripts\Change_SSRS_Owner_One_Subscription.ps1 "[Domain]\[new owner]" "[server]/_vti_bin/reportserver" "http://[server]" "9660674b-f020-453f-b1e3-d9ba37624519"  
```  
  
 **Script:**  
  
```  
# Parameters:  
#    newOwner       - DOMAIN\USER that will own the subscriptions you wish to change  
#    server         - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
#    site        - use "/" for default native mode site  
#    subscriptionID - guid for the single subscription to change  
  
Param(  
    [string]$newOwner,  
    [string]$server,  
    [string]$site,  
    [string]$subscriptionid  
   )  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
  
$subscription += $rs2010.ListSubscriptions($site) | where {$_.SubscriptionID -eq $subscriptionid};  
  
Write-Host " "  
Write-Host "----- $subscriptionid's Subscription properties: "  
$subscription | select Path, report, Description, SubscriptionID, Owner, Status  
  
$rs2010.ChangeSubscriptionOwner($subscription.SubscriptionID, $newOwner)  
  
#refresh the list  
$subscription = $rs2010.ListSubscriptions($site) | where {$_.SubscriptionID -eq $subscriptionid}; # use "/" for default native mode site  
Write-Host "----- $subscriptionid's Subscription properties: "  
$subscription | select Path, report, Description, SubscriptionID, Owner, Status  
```  
  
##  <a name="bkmk_run_1_subscription"></a> Script: Executar (acionar) uma única assinatura  
 Esse script executa uma assinatura específica usando o método FireEvent. O script executa a assinatura de maneira imediata, independentemente da agenda configurada para a assinatura. O EventType é comparado com o conjunto conhecido de eventos que estão definidos no arquivo de configuração do servidor do relatório **rsreportserver.config** O script usa o tipo de evento a seguir para assinaturas padrão:  
  
 `<Event>`  
  
 `<Type>TimedSubscription</Type>`  
  
 `</Event>`  
  
 Para obter mais informações sobre o arquivo de configuração, confira [RSReportServer Configuration File](../report-server/rsreportserver-config-configuration-file.md).  
  
 O script inclui a lógica de atraso "`Start-Sleep -s 6`" para que haja tempo após o evento ser acionado e para que o status atualizado fique disponível com o método ListSubscription.  
  
 **Sintaxe do modo Nativo:**  
  
```  
powershell c:\scripts\FireSubscription.ps1 "[server]/reportserver" $null "70366e82-2d3c-4edd-a216-b97e51e26de9"  
```  
  
 **Sintaxe do modo SharePoint:**  
  
```  
powershell c:\scripts\FireSubscription.ps1 "[server]/_vti_bin/reportserver" "http://[server]" "c3425c72-580d-423e-805a-41cf9799fd25"  
```  
  
 **Script:**  
  
```  
  
# Parameters  
#    server         - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
#    site           - use $null for a native mode server  
#    subscriptionid - subscription guid  
  
Param(  
  [string]$server,  
  [string]$site,  
  [string]$subscriptionid  
  )  
  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
#event type is case sensative to what is in the rsreportserver.config  
$rs2010.FireEvent("TimedSubscription",$subscriptionid,$site)  
  
Write-Host " "  
Write-Host "----- Subscription ($subscriptionid) status: "  
#get list of subscriptions and filter to the specific ID to see the Status and LastExecuted  
Start-Sleep -s 6 # slight delay in processing so ListSubscription returns the updated Status and LastExecuted  
$subscriptions = $rs2010.ListSubscriptions($site);   
$subscriptions | select Status, Path, report, Description, Owner, SubscriptionID, EventType, lastexecuted | where {$_.SubscriptionID -eq $subscriptionid}  
  
```  
  
## <a name="see-also"></a>Consulte também  
 <xref:ReportService2010.ReportingService2010.ListSubscriptions%2A>   
 <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>   
 <xref:ReportService2010.ReportingService2010.ListChildren%2A>   
 <xref:ReportService2010.ReportingService2010.FireEvent%2A>  
  
  
