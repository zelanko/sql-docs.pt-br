---
title: Desabilitar ou pausar o processamento de relatório e assinatura | Microsoft Docs
description: Gerencie assinaturas, pause agendas compartilhadas, desabilite fontes de dados compartilhadas, bloqueie o acesso a relatórios, gerencie permissões de assinatura e remova as extensões de entrega.
ms.date: 06/19/2019
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
ms.openlocfilehash: 1ea16180c9a4e67f40302de7d70ae357b8393010
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91986622"
---
# <a name="disable-or-pause-report-and-subscription-processing"></a>Desabilitar ou pausar o processamento de relatório e assinatura  
Há várias abordagens que você pode usar para desabilitar ou pausar o processamento de relatório e assinatura do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . As abordagens neste artigo abrangem a desabilitação de uma assinatura para interromper a conexão com a fonte de dados. Nem todas as abordagens são possíveis com ambos os modos de servidor do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. As seguintes tabelas resumem os métodos e os modos de servidor compatíveis do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]:  
  
##  <a name="in-this-article"></a><a name="bkmk_top"></a> Neste artigo  
  
|Abordagem|Modo de servidor com suporte|  
|-|---------------------------|  
|[Habilitar e desabilitar assinaturas](#bkmk_disable_subscription)|nativo|  
|[Pausar uma agenda compartilhada](#bkmk_pause_schedule)|Modo nativo e do SharePoint|  
|[Desabilitar uma fonte de dados compartilhada](#bkmk_disable_shared_datasource)|Modo nativo e do SharePoint|  
|[Modificar atribuições de função para impedir o acesso a um relatório (Modo Nativo)](#bkmk_modify_role_assignment)|nativo|  
|[Remover permissões de gerenciamento de assinatura da função (modo Nativo)](#bkmk_remove_manage_subscriptions_permission)|nativo|  
|[Desabilitar extensões de entrega](#bkmk_disable_extensions)|Modo nativo e do SharePoint|  
  
##  <a name="enable-and-disable-subscriptions"></a><a name="bkmk_disable_subscription"></a>Habilitar e desabilitar assinaturas  
  
>[!TIP]  
>Novo no SQL 2016 Reporting Services, *habilitar e desabilitar assinaturas*. Novas opções de interface de usuário permitem que você habilite e desabilite rapidamente as assinaturas. As assinaturas desabilitadas mantêm suas outras propriedades de configuração, como o cronograma, e podem ser facilmente reabilitadas. Você também pode habilitar e desabilitar programaticamente assinaturas ou auditar quais assinaturas são desabilitadas.  
  
  ![Os botões habilitar e desabilitar da página Assinaturas ](../../reporting-services/subscriptions/media/disable-or-pause-report-and-subscription-processing/subscription-enable-and-disable-buttons.png)  
  
No portal da Web, navegue até a assinatura na página **Minhas Assinaturas** ou na página **Assinaturas** de uma assinatura individual. Selecione uma ou mais assinaturas e clique no botão desabilitar ou no botão habilitar na faixa de opções (veja a imagem acima). A coluna de status será alterada para "Desabilitado" ou "Habilitado", respectivamente.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] grava uma linha no log do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] quando uma assinatura está habilitada ou desabilitada. Por exemplo, no arquivo de log do servidor de relatório:  
  
 `C:\Program Files\Microsoft SQL Server Reporting Services\SSRS\LogFiles\RSPortal_2019_06_20_00_49_22.log`  
  
 você verá linhas parecidas com as seguintes:  
  
 `RSPortal!subscription!RSPortal.exe!93!06/20/2019-01:16:47:: i INFO: Subscription 2b409d66-d4ea-408a-918c-0f9e41ce49ca disabled at 06/20/2019 01:16:47`  
  
 `RSPortal!subscription!RSPortal.exe!93!06/20/2019-01:16:51:: i INFO: Subscription 2b409d66-d4ea-408a-918c-0f9e41ce49ca enabled at 06/20/2019 01:16:51`  
  
![Conteúdo relacionado ao PowerShell](/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell"): **Use o Windows PowerShell para desabilitar uma assinatura única:** Use o script do PowerShell a seguir para desabilitar uma assinatura específica. Atualize o nome do servidor e a ID da assinatura no script.  
  
```PS  
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
  
 ![Conteúdo relacionado ao PowerShell](/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell") **Use o Windows PowerShell para listar todas as assinaturas desabilitadas:** Use o script do PowerShell a seguir para listar todas as assinaturas desabilitadas no servidor de relatório atual em modo nativo. Atualize o nome do servidor.  
  
```  
#list all disabled subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://uetestb03/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
Write-Host "--- Disabled Subscriptions ---";  
Write-Host "----------------------------------- ";  
$subscriptions | Where-Object {$_.Active.DisabledByUserSpecified -and $_.Active.DisabledByUser } | select subscriptionid, report, status, lastexecuted,path | format-table -auto  
```  
  
 ![Conteúdo relacionado ao PowerShell](/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell") **Use o Windows PowerShell para habilitar todas as assinaturas desabilitadas:** Use o script do PowerShell a seguir para habilitar todas as assinaturas desabilitadas no momento. Atualize o nome do servidor.  
  
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
  
 ![Conteúdo relacionado ao PowerShell](/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell") **Use o Windows PowerShell para DESABILITAR todas as assinaturas:** Use o script do PowerShell a seguir para desabilitar **TODAS** as assinaturas.  
  
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
  
##  <a name="pause-a-shared-schedule"></a><a name="bkmk_pause_schedule"></a> Pausar uma agenda compartilhada  
 Se um relatório ou assinatura for executado a partir de uma agenda compartilhada, você pode pausar a agenda para impedir o processamento. Todos os processamentos de relatório e assinatura controlados pelo agendamento serão adiados até o agendamento ser retomado.  
  
-   **Modo SharePoint:** ![configurações do SharePoint:](/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "Configurações do SharePoint") nas **Configurações do site**, selecione **Gerenciar agendas compartilhadas**. Selecione a agenda e clique em **Pausar agendamentos selecionados**.  
  
-   **Modo Nativo:** No portal da Web, selecione o botão **Configurações** ![botão Configurações](media/ssrs-portal-settings-gear.png) na barra de menus, na parte superior da tela do portal da Web, depois selecione **Configurações do site** no menu suspenso. Selecione a guia **Agendamentos** para exibir a página de agendamentos. Marque as caixas de seleção ao lado dos agendamentos que deseja habilitar ou desabilitar e, em seguida, selecione o botão **Habilitar** ou **Desabilitar**, respectivamente, para executar a ação desejada. A coluna de status será atualizada para "Desabilitado" ou "Habilitado", conforme a opção escolhida.  
  
##  <a name="disable-a-shared-data-source"></a><a name="bkmk_disable_shared_datasource"></a> Desabilitar uma fonte de dados compartilhada  
 Uma vantagem de usar fontes de dados compartilhadas é poder desabilitá-las para impedir a execução de um relatório ou assinatura controlada por dados. Desabilitar uma fonte de dados compartilhada desconecta o relatório de sua fonte externa. Enquanto está desabilitada, a fonte de dados fica indisponível para todos os relatórios e assinaturas que a utilizam.  
  
 Observe que o relatório ainda é carregado mesmo que a fonte de dados não esteja disponível. O relatório não contém dados, mas os usuários com as permissões adequadas podem acessar as páginas de propriedade, as configurações de segurança, o histórico de relatórios e as informações de assinatura associadas ao relatório.  
  
-   **Modo SharePoint:** para desabilitar uma fonte de dados compartilhada em um servidor de relatório no modo do SharePoint, navegue até a biblioteca de documentos que contém a fonte de dados. ![Ícone de fonte de dados compartilhada](../../reporting-services/report-data/media/hlp-16datasource.png "Ícone da fonte de dados compartilhada") Clique na fonte de dados e, em seguida, desmarque a caixa de seleção **Habilitar esta fonte de dados**.  
  
-   **Modo Nativo:** para desabilitar uma fonte de dados compartilhada em um servidor de relatório no modo nativo, abra a fonte de dados no portal da Web e desmarque a caixa de seleção **Habilitar esta fonte de dados**.  
  
##  <a name="modify-role-assignments-to-prevent-access-to-a-report-native-mode"></a><a name="bkmk_modify_role_assignment"></a> Modificar atribuições de função para impedir o acesso a um relatório (modo nativo)  
Uma maneira de tornar um relatório indisponível é remover temporariamente a atribuição de função que fornece acesso ao relatório. Esta abordagem pode ser usada em todos os relatórios, independentemente de como a conexão de fonte de dados seja feita. Esta abordagem visa apenas o relatório, sem afetar a operação de outros relatórios ou itens.  
  
 Para remover a atribuição de função, abra a página **Segurança** do relatório no portal da Web. Se o relatório herda a segurança de um pai, é possível selecionar **Personalizar segurança** e selecionar **Confirmar** na caixa de diálogo **Segurança do item** para criar uma política de segurança restritiva que omite as atribuições de função que fornecem amplo acesso (por exemplo, você pode remover uma atribuição de função que fornece acesso a Todos e manter a atribuição de função que fornece acesso a um pequeno grupo de usuários, como Administradores).  
  
##  <a name="remove-manage-subscription-permissions-from-role-native-mode"></a><a name="bkmk_remove_manage_subscriptions_permission"></a> Remover permissões de gerenciamento de assinatura da função (modo nativo)  
 Para impedir que os usuários criem assinaturas, desmarque a tarefa **Gerenciar assinaturas individuais** da função. Quando essa tarefa é removida, as páginas Assinatura não estão disponíveis. No portal da Web, a página Minhas Assinaturas parece estar vazia (não é possível excluí-la), mesmo que contivesse assinaturas anteriormente. A remoção de tarefas relacionadas à assinatura impede que os usuários criem e modifiquem assinaturas, mas não exclui as assinaturas existentes. As assinaturas existentes continuarão sendo executadas até serem excluídas. Para remover a permissão:  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 
  
2.  Conecte-se ao servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
3.  Expanda o nó **Segurança** .  
  
4.  Expanda o nó **Funções** e selecione a função desejada.  
  
5.  Clique com o botão direito do mouse na função e selecione **Propriedades**.  
  
6.  Desmarque as tarefas **Gerenciar assinaturas individuais** e **Gerenciar todas as assinaturas**.  
  
7.  Clique em **OK** para aplicar as alterações.

  
##  <a name="disable-delivery-extensions"></a><a name="bkmk_disable_extensions"></a> Desabilitar extensões de entrega  
 Todas as extensões de entrega instaladas em um servidor de relatório estão disponíveis para qualquer usuário que tenha permissão para criar uma assinatura em um relatório específico. As extensões de entrega a seguir estão disponíveis e são configuradas automaticamente:  
  
-   Compartilhamento de Arquivos do Windows  
  
-   Biblioteca do SharePoint (disponível somente a partir de um site do SharePoint que é integrado com um servidor de relatório no modo integrado do SharePoint)  
  
 A entrega de email deve ser configurada antes de ser usada. Se você não configurá-la, esse recurso não estará disponível. Para obter mais informações, confira [Configurações de email – Modo nativo do Reporting Services (Configuration Manager)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md).  
  
 Se você desejar desabilitar extensões específicas, remova as entradas de extensão no arquivo **RSReportServer.config** . Para obter mais informações, confira [Arquivos de configuração do Reporting Services](../../reporting-services/report-server/reporting-services-configuration-files.md) e [Configurações de email – Modo nativo do Reporting Services (Configuration Manager)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md).  
  
 Depois de ser removida, a extensão de entrega não fica mais disponível no portal da Web ou em um site do SharePoint. A remoção de uma extensão de entrega pode resultar em assinaturas inativas. Exclua as assinaturas ou configure-as para usar uma extensão de entrega diferente antes de remover uma extensão.  
  
## <a name="see-also"></a>Confira também  
 [Assinaturas e entrega &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Arquivos de configuração do Reporting Services](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Configurar o portal da Web](../../reporting-services/report-server/configure-web-portal.md)   
 [Servidor de relatório do Reporting Services &#40;Modo Nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [O portal da Web de um servidor de relatório (modo nativo do SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md)   
 [Itens protegíveis](../../reporting-services/security/securable-items.md) 
