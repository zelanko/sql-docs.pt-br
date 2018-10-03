---
title: Usar minhas assinaturas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], My Subscriptions page
- My Subscriptions page [Reporting Services]
ms.assetid: e96623ba-677e-4748-8787-f32bed3b5c12
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 3a45edaedce83d741d24ee085ccf962854303a68
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48129346"
---
# <a name="use-my-subscriptions"></a>Usar Minhas Assinaturas
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] Gerenciador de relatórios inclui um **Minhas assinaturas** página que organiza todas as suas assinaturas em um só lugar. É possível usar Minhas Assinaturas para exibir, modificar e excluir assinaturas existentes. Entretanto, você não pode usar Minhas Assinaturas para criar assinaturas.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] Modo nativo|  
  
 Em Minhas Assinaturas, você pode classificar assinaturas por pasta, relatório, descrição, gatilho, data da última execução ou status. Todos os valores são classificados por ordem alfabética, exceto Data da Última Execução, que está em ordem cronológica.  
  
 Minhas Assinaturas exibe somente as assinaturas criadas pelo usuário. Minhas Assinaturas não relaciona assinaturas de propriedade de outros usuários, ainda que você tenha sido adicionado como assinante dessas assinaturas, tampouco exibe assinaturas controladas por dados.  
  
 Não é possível procurar assinaturas por nome, nem procurar uma assinatura com base em informações de gatilho, informações de status, etc. Para obter mais informações, consulte [criar, modificar e excluir assinaturas padrão &#40;Reporting Services no modo nativo&#41;](create-and-manage-subscriptions-for-native-mode-report-servers.md).  
  
## <a name="how-to-use-my-subscriptions"></a>Como usar Minhas Assinaturas  
 Minhas Assinaturas está disponível através do Gerenciador de Relatórios. Para acessar Minhas Assinaturas, clique em **Minhas Assinaturas** na barra de ferramentas global do Gerenciador de Relatórios.  
  
## <a name="use-windows-powershell-to-list-mysubscriptions"></a>Usar o Windows PowerShell para listar MySubscriptions  
 ![Conteúdo relacionado ao PowerShell](../media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell")  
  
 O seguinte script do PowerShell retornará a lista de assinaturas e as propriedades de assinatura do usuário atual. Para obter mais informações, consulte [Método ReportingService2010.ListMySubscriptions](http://technet.microsoft.com/library/reportservice2010.reportingservice2010.listmysubscriptions.aspx).  
  
```  
#server -  all subscriptions of the current user at the given server or site  
$server="[server name]/reportserver"  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
  
$subscriptions=ListMySubscriptions(ItemPathOrSiteURL)  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status  
#uncomment the following to list all the subscription properties  
#$subscriptions  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Assinaturas controladas por dados](data-driven-subscriptions.md)   
 [Assinaturas e entrega de &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [Criar e gerenciar assinaturas de servidores de relatório no modo Nativo](../create-manage-subscriptions-native-mode-report-servers.md)  
  
  
