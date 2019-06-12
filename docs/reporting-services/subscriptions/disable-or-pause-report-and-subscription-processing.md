---
title: Desabilitar ou pausar o processamento de relatório e assinatura | Microsoft Docs
ms.date: 09/29/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- pausing schedules
- subscriptions [Reporting Services], pausing
- report processing [Reporting Services], pausing
- shared data sources [Reporting Services]
- pausing subscription processing
- pausing report processing
- temporarily stopping report processing
- disabling shared data sources
- roles [Reporting Services], modifying
- shared schedules [Reporting Services], pausing
ms.assetid: 3cf9a240-24cc-46d4-bec6-976f82d8f830
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 66c9072f10165b520120b80a9264a828a4e037db
ms.sourcegitcommit: 1800fc15075bb17b50d0c18b089d8a64d87ae726
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66499881"
---
# <a name="disable-or-pause-report-and-subscription-processing"></a>Desabilitar ou pausar o processamento de relatório e assinatura
  Há várias abordagens que você pode usar para desabilitar ou pausar o processamento de relatório e assinatura do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . As abordagens neste tópico abrangem a desabilitação de uma assinatura para interromper a conexão com a fonte de dados. Nem todas as abordagens são possíveis com os dois modos de servidor do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . As tabelas a seguir resumem os métodos e os modos de servidor do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] com suporte:  
  
##  <a name="bkmk_top"></a> Neste tópico  
  
||Modo de servidor com suporte|  
|-|---------------------------|  
|[Habilitar e desabilitar assinaturas](#bkmk_disable_subscription)|nativo|  
|[Pausar uma agenda compartilhada](#bkmk_pause_schedule)|Modo nativo e do SharePoint|  
|[Desabilitar uma fonte de dados compartilhada](#bkmk_disable_shared_datasource)|Modo nativo e do SharePoint|  
|[Modificar atribuições de função para impedir o acesso a um relatório (Modo Nativo)](#bkmk_modify_role_assignment)|nativo|  
|[Remover permissões de gerenciamento de assinatura da função (modo Nativo)](#bkmk_remove_manage_subscriptions_permission)|nativo|  
|[Desabilitar extensões de entrega](#bkmk_disable_extensions)|Modo nativo e do SharePoint|  
  
##  <a name="bkmk_disable_subscription"></a> Habilitar e desabilitar assinaturas  
  
> [!TIP]  
>  Novo no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]! **Habilitar e desabilitar assinaturas**. Novas opções de interface de usuário permitem que você desabilite e habilite rapidamente as assinaturas. As assinaturas desabilitadas mantêm suas outras propriedades de configuração, como o cronograma, e podem ser facilmente habilitadas. Você também pode habilitar e desabilitar programaticamente assinaturas ou auditar quais assinaturas são desabilitadas.  
  
 ![faixa de opções da assinatura do Reporting Services](../../reporting-services/subscriptions/media/ssrs-subscription-ribbon.png "faixa de opções da assinatura do Reporting Services")  
  
 No Gerenciador de Relatórios no modo Nativo, navegue até a assinatura na página **Minhas Assinaturas** ou na página **Gerenciar** de uma assinatura individual. Selecione uma ou mais assinaturas e, em seguida, clique no botão Desabilitar ![desabilitar uma assinatura do Reporting Services](../../reporting-services/subscriptions/media/ssrs-disable-subscription.png "desabilitar uma assinatura do Reporting Services") ou no botão Habilitar ![habilitar uma assinatura do Reporting Services](../../reporting-services/subscriptions/media/ssrs-enable-subscription.png "habilitar uma assinatura do Reporting Services") na faixa de opções. As assinaturas desabilitadas são sinalizadas com um ícone de aviso ![aviso do status de uma assinatura do Reporting Services](../../reporting-services/subscriptions/media/ssrs-subscription-warning.png "aviso do status de uma assinatura do Reporting Services") e o status é listado como **Desabilitado**.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] escreve uma linha no log do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] quando uma assinatura é desabilitada, e outra entrada quando a assinatura é habilitada. Por exemplo, no arquivo de log do servidor de relatório:  
  
 `C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\LogFiles\ReportServerService__10_16_2014_00_02_18.log`  
  
 você verá linhas parecidas com as seguintes:  
  
 `library!ReportServer_0-1!b08!10/16/2014-16:21:14:: i INFO: Call to DisableSubscriptionAction(SubscriptionID=e843bc2b-023e-45a3-ba23-22f9dc9a0934)`  
  
 `library!ReportServer_0-1!2eec!10/16/2014-16:44:18:: i INFO: Call to EnableSubscriptionAction(SubscriptionID=e843bc2b-023e-45a3-ba23-22f9dc9a0934).`  
  
 ![Conteúdo relacionado ao PowerShell](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell") **Usar o Windows PowerShell para desabilitar uma assinatura única:** use o seguinte script do PowerShell para desabilitar uma assinatura específica. Atualize o nome do servidor e a ID da assinatura.  
  
```  
#disable specific subscription  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptionID = "subscription guid";  
$rs2010.DisableSubscription($subscriptionID);  
  
```  
  
 Você pode usar o script a seguir para listar todas as assinaturas com suas IDs. Atualize o nome do servidor.  
  
```  
#list all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME /ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
$subscriptions | select subscriptionid, report, status, path  
  
```  
  
 ![Conteúdo relacionado ao PowerShell](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell") **Usar o Windows PowerShell para listar todas as assinaturas desabilitadas:** use o seguinte script do PowerShell para listar todas as assinaturas desabilitadas no servidor de relatório atual no modo Nativo. Atualize o nome do servidor.  
  
```  
#list all disabled subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://uetestb03/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
Write-Host "--- Disabled Subscriptions ---";  
Write-Host "----------------------------------- ";  
$subscriptions | Where-Object {$_.Active.DisabledByUserSpecified -and $_.Active.DisabledByUser } | select subscriptionid, report, status, lastexecuted,path | format-table -auto  
```  
  
 ![Conteúdo relacionado ao PowerShell](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell") **Usar o Windows PowerShell para habilitar todas as assinaturas desabilitadas:** use o seguinte script do PowerShell para habilitar todas as assinaturas desabilitadas no momento. Atualize o nome do servidor.  
  
```  
#enable all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/") | Where-Object {$_.status -eq "disabled" } ;  
ForEach ($subscription in $subscriptions)  
{  
    $rs2010.EnableSubscription($subscription.SubscriptionID);  
    $subscription | select subscriptionid, report, path  
}  
  
```  
  
 ![Conteúdo relacionado ao PowerShell](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell") **Usar o Windows PowerShell para DESABILITAR todas as assinaturas:** use o seguinte script do PowerShell para desabilitar **TODAS** as assinaturas.  
  
```  
#DISABLE all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/") ;  
ForEach ($subscription in $subscriptions)  
{  
    $rs2010.DisableSubscription($subscription.SubscriptionID);  
    $subscription | select subscriptionid, report, path  
}  
```  
  
##  <a name="bkmk_pause_schedule"></a> Pausar uma agenda compartilhada  
 Se um relatório ou assinatura for executado a partir de uma agenda compartilhada, você pode pausar a agenda para impedir o processamento. Todos os processamentos de relatório e assinatura controlados pelo agendamento serão adiados até o agendamento ser retomado.  
  
-   **Modo do SharePoint:** ![configurações do SharePoint](../../analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint Settings") Em **Configurações de site**, selecione **Gerenciar agendamentos compartilhados**. Selecione a agenda e clique em **Pausar agendamentos selecionados**.  
  
-   **Modo Nativo:** no Gerenciador de Relatórios, clique em **Configurações do Site**. Selecione a agenda e clique em **Pausar**.  
  
##  <a name="bkmk_disable_shared_datasource"></a> Desabilitar uma fonte de dados compartilhada  
 Uma vantagem de usar fontes de dados compartilhadas é poder desabilitá-las para impedir a execução de um relatório ou assinatura controlada por dados. Desabilitar uma fonte de dados compartilhada desconecta o relatório de sua fonte externa. Enquanto está desabilitada, a fonte de dados fica indisponível para todos os relatórios e assinaturas que a utilizam.  
  
 Observe que o relatório ainda é carregado mesmo que a fonte de dados não esteja disponível. O relatório não contém dados, mas os usuários com as permissões adequadas podem acessar as páginas de propriedade, as configurações de segurança, o histórico de relatórios e as informações de assinatura associadas ao relatório.  
  
-   **Modo do SharePoint:** para desabilitar uma fonte de dados compartilhada em um servidor de relatório no modo do SharePoint, navegue até a biblioteca de documentos que contém a fonte de dados. ![Ícone de fonte de dados compartilhada](../../reporting-services/report-data/media/hlp-16datasource.png "Ícone de fonte de dados compartilhada") Clique na fonte de dados e, em seguida, desmarque a caixa de seleção **Habilitar esta fonte de dados**.  
  
-   **Modo Nativo:** Para desabilitar uma fonte de dados compartilhada, abra a fonte de dados no Gerenciador de Relatórios e desmarque a caixa de seleção **Habilitar esta fonte de dados** .  
  
##  <a name="bkmk_modify_role_assignment"></a> Modificar atribuições de função para impedir o acesso a um relatório (Modo Nativo)  
 Uma maneira de tornar um relatório indisponível é remover temporariamente a atribuição de função que fornece acesso ao relatório. Esta abordagem pode ser usada em todos os relatórios, independentemente de como a conexão de fonte de dados seja feita. Esta abordagem visa apenas o relatório, sem afetar a operação de outros relatórios ou itens.  
  
 Para remover a atribuição de função, abra a página Propriedades de Segurança do relatório no Gerenciador de Relatórios. Se o relatório herda a segurança de um pai, clique em **Editar Segurança de Item** para criar uma política de segurança restritiva que omite as atribuições de função que fornecem amplo acesso (por exemplo, você pode remover uma atribuição de função que fornece acesso a Todos e manter a atribuição de função que fornece acesso a um pequeno grupo de usuários, como Administradores).  
  
##  <a name="bkmk_remove_manage_subscriptions_permission"></a> Remover permissões de gerenciamento de assinatura da função (modo Nativo)  
 Para impedir que os usuários criem assinaturas, desmarque a tarefa **Gerenciar assinaturas individuais** da função. Quando essa tarefa é removida, as páginas Assinatura não estão disponíveis. No Gerenciador de Relatórios, a página Minhas Assinaturas parece estar vazia (não é possível excluí-la), mesmo que contivesse assinaturas anteriormente. A remoção de tarefas relacionadas à assinatura impede que os usuários criem e modifiquem assinaturas, mas não exclui as assinaturas existentes. As assinaturas existentes continuarão sendo executadas até serem excluídas. Para remover a permissão:  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
2.  Conecte-se ao servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
3.  Expanda o nó **Segurança** .  
  
4.  Selecione a função e desmarque a tarefa **Gerenciar assinaturas individuais** .  
  
##  <a name="bkmk_disable_extensions"></a> Desabilitar extensões de entrega  
 Todas as extensões de entrega instaladas em um servidor de relatório estão disponíveis para qualquer usuário que tenha permissão para criar uma assinatura em um relatório específico. As extensões de entrega a seguir estão disponíveis e são configuradas automaticamente:  
  
-   Compartilhamento de Arquivos do Windows  
  
-   Biblioteca do SharePoint (disponível somente a partir de um site do SharePoint que é integrado com um servidor de relatório no modo integrado do SharePoint)  
  
 A entrega de email deve ser configurada antes de ser usada. Se você não configurá-la, esse recurso não estará disponível. Para obter mais informações, consulte [configurações de email – modo nativo do Reporting Services (Configuration Manager)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md).  
  
 Se você desejar desabilitar extensões específicas, remova as entradas de extensão no arquivo **RSReportServer.config** . Para obter mais informações, consulte [arquivos de configuração do Reporting Services](../../reporting-services/report-server/reporting-services-configuration-files.md) e [configurações de email – modo nativo do Reporting Services (Configuration Manager)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md).  
  
 Depois de ser removida, a extensão de entrega não está mais disponível no Gerenciador de Relatórios ou em um site do SharePoint. A remoção de uma extensão de entrega pode resultar em assinaturas inativas. Exclua as assinaturas ou configure-as para usar uma extensão de entrega diferente antes de remover uma extensão.  
  
## <a name="see-also"></a>Consulte Também  
 [Assinaturas e entrega &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Arquivos de configuração do Reporting Services](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Configurar o Gerenciador de Relatórios &#40;Modo Nativo&#41;](../../reporting-services/report-server/configure-report-manager-native-mode.md)   
 [Servidor de relatório do Reporting Services &#40;Modo Nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Página Propriedades de Segurança, Itens &#40;Gerenciador de Relatórios&#41;](https://msdn.microsoft.com/library/351b8503-354f-4b1b-a7ac-f1245d978da0)  
  
  
