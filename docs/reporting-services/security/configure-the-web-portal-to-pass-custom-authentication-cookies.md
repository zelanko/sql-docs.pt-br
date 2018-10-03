---
title: Configurar o portal da Web para passar cookies de autenticação personalizados | Microsoft Docs
ms.date: 04/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- authentication [Reporting Services]
- extensions [Reporting Services], custom security
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b538523839be0260eda33934a18e682579aaa3f9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47810214"
---
# <a name="configure-the-web-portal-to-pass-custom-authentication-cookies"></a>Configurar o portal da Web para passar cookies de autenticação personalizados

Se estiver usando uma extensão de autenticação personalizada, configure o portal da Web para transmitir cookies de autenticação personalizados. Caso contrário, o portal da Web transmitirá cookies somente por solicitações HTTP específicas ao servidor de relatório. Se desejar transmitir cookies adicionais, modifique o arquivo RSReportServer.Config.

## <a name="modifying-the-rsreportserverconfig-file"></a>Modificando o arquivo RSReportServer.Config

Habilite o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] para transmitir cookies adicionais por meio do servidor de relatório adicionando um elemento \<**PassThroughCookies**> às configurações do portal da Web no arquivo RSReportServer.config. A transmissão de cookies adicionais é útil em uma solução de autenticação de logon único que requer não só cookies de autenticação do servidor de relatório, mas também cookies de um sistema de autenticação de terceiros.

Para permitir que cookies adicionais sejam transmitidos por meio de solicitações HTTP ao usar o portal da Web, defina os seguintes elementos no arquivo RSReportServer.config:
  
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
  
## <a name="see-also"></a>Consulte Também

[Autenticação com o servidor de relatório](../../reporting-services/security/authentication-with-the-report-server.md)   
[Arquivo de Configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[Visão geral de extensões de segurança](../../reporting-services/extensions/security-extension/security-extensions-overview.md)   
[Configurar e administrar um servidor de relatório &#40;modo nativo do SSRS&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
Ainda tem dúvidas? [Experimente o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
