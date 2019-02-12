---
title: Configurar o Gerenciador de relatórios para passar Cookies de autenticação personalizados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- authentication [Reporting Services]
- extensions [Reporting Services], custom security
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 6787ec73d91b32e0bdb90f8a5f25499f0ac35620
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034479"
---
# <a name="configure-report-manager-to-pass-custom-authentication-cookies"></a>Configurar o Gerenciador de Relatórios para transmitir cookies de autenticação personalizados
  Se você estiver usando uma extensão de autenticação personalizada, configure o Gerenciador de Relatórios para transmitir cookies de autenticação personalizados. Caso contrário, o Gerenciador de Relatórios transmitirá cookies somente por solicitações HTTP específicas do servidor de relatório. Se desejar transmitir cookies adicionais, modifique o arquivo RSReportServer.Config.  
  
## <a name="modifying-the-rsreportserverconfig-file"></a>Modificando o arquivo RSReportServer.Config  
 Você pode habilitar o Gerenciador de Relatórios para transmitir cookies adicionais pelo servidor de relatório adicionando um elemento <`PassThroughCookies`> às configurações do Gerenciador de Relatórios no arquivo RSReportServer.config. A transmissão de cookies adicionais é útil em uma solução de autenticação de logon único que requer não só cookies de autenticação do servidor de relatório, mas também cookies de um sistema de autenticação de terceiros.  
  
 Para permitir que cookies adicionais sejam transmitidos através de solicitações HTTP ao usar o Gerenciador de Relatórios, defina os seguintes elementos no arquivo RSReportServer.config:  
  
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
 [Autenticação com o servidor de relatório](authentication-with-the-report-server.md)   
 [Arquivo de configuração RSReportServer](../report-server/rsreportserver-config-configuration-file.md)   
 [Visão geral de extensões de segurança](../extensions/security-extension/security-extensions-overview.md)   
 [Configurar e administrar um servidor de relatório &#40;modo nativo do SSRS&#41;](../report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
  
  
