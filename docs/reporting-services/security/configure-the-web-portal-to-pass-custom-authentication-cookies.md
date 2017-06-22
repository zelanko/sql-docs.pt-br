---
title: "Configurar o Portal da Web para transmitir Cookies de autenticação personalizados | Microsoft Docs"
ms.custom: 
ms.date: 04/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- authentication [Reporting Services]
- extensions [Reporting Services], custom security
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
caps.latest.revision: 18
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 0f1131c191fa64c6dc6f2a074a9cd5db7a8b0e1b
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="configure-the-web-portal-to-pass-custom-authentication-cookies"></a>Configurar o portal da Web para passar cookies de autenticação personalizados

Se você estiver usando uma extensão de autenticação personalizada, você deve configurar o portal da web para transmitir cookies de autenticação personalizados. Caso contrário, o portal da web transmitirá cookies somente por meio de solicitações HTTP específicas para o servidor de relatório. Se desejar transmitir cookies adicionais, modifique o arquivo RSReportServer.Config.

## <a name="modifying-the-rsreportserverconfig-file"></a>Modificando o arquivo RSReportServer.Config

Você pode habilitar o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] para transmitir cookies adicionais pelo servidor de relatório adicionando um \< **PassThroughCookies**> elemento para as configurações de configuração do portal da web no arquivo rsreportserver. config. A transmissão de cookies adicionais é útil em uma solução de autenticação de logon único que requer não só cookies de autenticação do servidor de relatório, mas também cookies de um sistema de autenticação de terceiros.

Para habilitar cookies adicionais sejam transmitidos por meio de solicitações HTTP ao usar o portal da web, defina os seguintes elementos no arquivo rsreportserver. config:
  
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
  
## <a name="see-also"></a>Consulte também

[Autenticação com o servidor de relatório](../../reporting-services/security/authentication-with-the-report-server.md)   
[Arquivo de Configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[Visão geral de extensões de segurança](../../reporting-services/extensions/security-extension/security-extensions-overview.md)   
[Configurar e administrar um servidor de relatório &#40; Modo nativo do SSRS &#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
Mais perguntas? [Tente o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
