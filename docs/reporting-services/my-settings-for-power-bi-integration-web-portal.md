---
title: "Minhas configurações para integração do Power BI (portal da web) | Microsoft Docs"
ms.date: 05/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- pbi
- power bi
- power bi integration
ms.assetid: 85c2fac7-80bf-45b7-8654-764b5f5231f5
caps.latest.revision: 15
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 91be669329ea6d822dcc489584d649e5a01ce018
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="my-settings-for-power-bi-integration-web-portal"></a>Minhas Configurações para integração do Power BI (portal Web)

[!INCLUDE[ssrs-appliesto-sql2016-xpreview](../includes/ssrs-appliesto-sql2016-xpreview.md)]

A página **Minhas Configurações** no [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] é usada por usuários individuais para gerenciar sua entrada com o [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]. Ao percorrer as etapas para fixar um item de relatório, você será automaticamente solicitado a entrar.  No entanto, você poderá usar a página **Minhas Configurações** se precisar entrar manualmente ou se precisar sair da página.  Se a opção de menu **Minhas Configurações** não estiver visível, isso indicará que o servidor de relatório não foi integrado ao  [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)].  Para obter mais informações, consulte [Integração do servidor de relatório do Power BI &#40;Configuration Manager&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md).  
  
![ssRS_WebPortal_MySettings](../reporting-services/media/ssrs-webportal-mysettings.png)  
  
## <a name="why-sign-in"></a>Por que entrar  
 Ao entrar, você estabelece um relacionamento entre sua conta de usuário do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e sua conta do [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] .  A entrada cria um token de segurança que é válido por 90 dias. Se o token expirar e houver itens fixados no Power BI, você verá uma notificação.  
   
 ![ssRS_WebPortal_PowerBI_Notification](../reporting-services/media/ssrs-webportal-powerbi-notification.png)    
   
Os blocos nos painéis do [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] não serão atualizada até que você entre novamente pelo **MySettings**.  
  
![ssRS_WebPortal_PowerBI_SignIn_Again](../reporting-services/media/ssrs-webportal-powerbi-signin-again.png)  
  
Após entrar, será criado um novo token de segurança.  Seus blocos do painel começarão a ser atualizados de acordo com as agendas previamente configuradas.  

## <a name="next-steps"></a>Próximas etapas

[Integração do servidor de relatórios de BI de energia](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)   
[Fixar itens do Reporting Services nos painéis do Power BI](../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md)   
[Painéis no Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)  
[Portal da Web](../reporting-services/web-portal-ssrs-native-mode.md)  

Mais perguntas? [Tente fazer o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
