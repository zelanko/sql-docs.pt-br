---
title: "Configurar o Gerenciador de Relat&#243;rios para transmitir cookies de autentica&#231;&#227;o personalizados | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "autenticação [Reporting Services]"
  - "extensões [Reporting Services], segurança personalizada"
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
caps.latest.revision: 18
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 18
---
# Configurar o Gerenciador de Relat&#243;rios para transmitir cookies de autentica&#231;&#227;o personalizados
  Se você estiver usando uma extensão de autenticação personalizada, configure o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] para transmitir cookies de autenticação personalizados. Caso contrário, o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] transmitirá cookies somente por solicitações HTTP específicas do servidor de relatório. Se desejar transmitir cookies adicionais, modifique o arquivo RSReportServer.Config.  
  
## Modificando o arquivo RSReportServer.Config  
 Você pode habilitar o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] para transmitir cookies adicionais pelo servidor de relatório adicionando um elemento \<**PassThroughCookies**> às configurações do [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] no arquivo RSReportServer.config. A transmissão de cookies adicionais é útil em uma solução de autenticação de logon único que requer não só cookies de autenticação do servidor de relatório, mas também cookies de um sistema de autenticação de terceiros.  
  
 Para permitir que cookies adicionais sejam transmitidos através de solicitações HTTP ao usar o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)], defina os seguintes elementos no arquivo RSReportServer.config:  
  
```  
<UI>  
   <CustomAuthenticationUI>  
      ...  
      <PassThroughCookies>  
         <PassThroughCookie>cookiename1</PassThroughCookie>  
         <PassThroughCookie>cookiename2</PassThroughCookie>  
      </PassThroughCookies>  
   </CustomAuthenticationUI>  
      ...  
</UI>  
```  
  
## Consulte também  
 [Autenticação com o servidor de relatório](../../reporting-services/security/authentication-with-the-report-server.md)   
 [Arquivo de Configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Visão geral de extensões de segurança](../../reporting-services/extensions/security-extension/security-extensions-overview.md)   
 [Configurar e administrar um servidor de relatório &#40;modo nativo do SSRS&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
  
  