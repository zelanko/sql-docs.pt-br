---
title: "Usar Minhas Assinaturas (Servidor de Relat&#243;rio no Modo Nativo) | Microsoft Docs"
ms.custom: ""
ms.date: "07/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "assinaturas [Reporting Services], página Minhas Assinaturas"
  - "página Minhas Assinaturas [Reporting Services]"
ms.assetid: e96623ba-677e-4748-8787-f32bed3b5c12
caps.latest.revision: 40
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 38
---
# Usar Minhas Assinaturas (Servidor de Relat&#243;rio no Modo Nativo)
O portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui uma página chamada **Minhas Assinaturas** que organiza todas as suas assinaturas em um único lugar. É possível usar *Minhas Assinaturas* para exibir, modificar, habilitar, desabilitar e excluir assinaturas existentes. Entretanto, você não pode usar Minhas Assinaturas para criar assinaturas.  Minhas Assinaturas exibe somente as assinaturas criadas pelo usuário. Minhas Assinaturas não relaciona assinaturas de propriedade de outros usuários, ainda que você tenha sido adicionado como assinante dessas assinaturas, tampouco exibe assinaturas controladas por dados.
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo nativo|  
  
O campo de pesquisa filtrará dinamicamente a lista de assinaturas, visto que não é possível procurar assinaturas por nome, nem procurar uma assinatura com base em informações de gatilho, informações de status etc. Para saber mais, consulte [Crie e gerencie assinaturas de servidores de relatório no modo Nativo](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md).
  
## Para abrir a página Minhas Assinaturas  
1. Abra o portal da Web do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)].
2. Clique em Configurações ![ssrs_portal_settings_gear](../../reporting-services/subscriptions/media/ssrs-portal-settings-gear.png) na barra de ferramentas.
3. Clique em **Minhas Assinaturas**.

Para obter mais informações, consulte [Portal da Web do Reporting Services](../../reporting-services/web-portal-ssrs-native-mode.md).

## Usar o Windows PowerShell para listar MySubscriptions  
 ![Conteúdo relacionado ao PowerShell](../../analysis-services/instances/install-windows/media/rs-powershellicon.png "Conteúdo relacionado ao PowerShell")  
  
 O seguinte script do PowerShell retornará a lista de assinaturas e as propriedades de assinatura do usuário atual. Para obter mais informações, consulte [Método ReportingService2010.ListMySubscriptions](http://technet.microsoft.com/library/reportservice2010.reportingservice2010.listmysubscriptions.aspx).  
  
```  
#server -  all subscriptions of the current user at the given server or site  
$server="[server name]/reportserver"  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
  
$subscriptions=ListMySubscriptions(ItemPathOrSiteURL)  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status  
#uncomment the following to list all the subscription properties  
#$subscriptions

```  
  
## Consulte também  
 [Assinaturas controladas por dados](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [Assinaturas e entrega &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [old_Crie e gerencie assinaturas de servidores de relatório no modo nativo](http://msdn.microsoft.com/pt-br/7f46cbdb-5102-4941-bca2-5e0ff9012c6b)  
  
  