---
title: "Minhas Configura&#231;&#245;es para integra&#231;&#227;o do Power BI (portal Web) | Microsoft Docs"
ms.date: "05/18/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "pbi"
  - "power bi"
  - "power bi integration"
ms.assetid: 85c2fac7-80bf-45b7-8654-764b5f5231f5
caps.latest.revision: 15
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 15
---
# Minhas Configura&#231;&#245;es para integra&#231;&#227;o do Power BI (portal Web)
  A página **Minhas Configurações** no [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] é usada por usuários individuais para gerenciar sua entrada com o [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]. Ao percorrer as etapas para fixar um item de relatório, você será automaticamente solicitado a entrar.  No entanto, você poderá usar a página **Minhas Configurações** se precisar entrar manualmente ou se precisar sair da página.  Se a opção de menu **Minhas Configurações** não estiver visível, isso indicará que o servidor de relatório não foi integrado ao  [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)].  Para obter mais informações, consulte [Integração do Servidor de Relatório do Power BI &#40;Configuration Manager&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md).  
  
![ssRS_WebPortal_MySettings](../reporting-services/media/ssrs-webportal-mysettings.png)  
  
## Por que entrar  
 Ao entrar, você estabelece um relacionamento entre sua conta de usuário do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e sua conta do [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] .  A entrada cria um token de segurança que é válido por 90 dias. Se o token expirar e houver itens fixados no Power BI, você verá uma notificação.  
   
 ![ssRS_WebPortal_PowerBI_Notification](../reporting-services/media/ssrs-webportal-powerbi-notification.png)    
   
Os blocos nos painéis do [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] não serão atualizada até que você entre novamente pelo **MySettings**.  
  
![ssRS_WebPortal_PowerBI_SignIn_Again](../reporting-services/media/ssrs-webportal-powerbi-signin-again.png)  
  
Após entrar, será criado um novo token de segurança.  Seus blocos do painel começarão a ser atualizados de acordo com as agendas previamente configuradas.  
  
## Consulte também  
 [Integração do servidor de relatório do Power BI &#40;Configuration Manager&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)   
 [Fixar itens do Reporting Services nos painéis do Power BI](../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md)   
 [Painéis no Power BI](https://support.powerbi.com/knowledgebase/articles/424868-dashboards-in-power-bi)  
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../includes/feedback-stackoverflow-msdn-connect-md.md)]
