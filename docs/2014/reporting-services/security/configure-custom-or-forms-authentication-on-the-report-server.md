---
title: Configurar a autenticação personalizada ou de formulários no servidor de relatório | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Forms authentication, configuring
- custom authentication [Reporting Services]
ms.assetid: e8601a8f-e66d-4649-8e4d-a46ca20ec7d0
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: e568d04a58ad13479f0e3a58254f8e409c46164d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56010817"
---
# <a name="configure-custom-or-forms-authentication-on-the-report-server"></a>Configurar autenticação personalizada ou de formulários no servidor de relatório
  O Reporting Services fornece uma arquitetura extensível que lhe permite conectar módulos de autenticação personalizados ou baseados em formulários. Você poderá avaliar a possibilidade de implementar uma extensão de autenticação personalizada, caso os requisitos de implantação não incluam a segurança integrada do Windows ou a autenticação Básica. O cenário mais comum para uso da autenticação personalizada é no suporte ao acesso de Internet ou extranet para um aplicativo Web. Substituir a extensão de Autenticação do Windows padrão por uma extensão de personalizada proporciona a você mais controle sobre a forma como é concedido a usuários externos acesso ao servidor de relatório.  
  
 Na prática, a implantação de uma extensão de autenticação personalizada requer várias etapas que incluem a cópia de assemblies e arquivos de aplicativo, a modificação de arquivos de configuração e teste. Este tópico se concentra apenas nas configurações de autenticação que você especifica nos arquivos de configuração.  
  
> [!NOTE]  
>  A criação de uma extensão de autenticação personalizada requer código personalizado e experiência em segurança [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] . Se você não quiser criar uma extensão de autenticação personalizada, poderá usar grupos e contas do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory, mas deverá reduzir significativamente o escopo de uma implantação de servidor de relatório. Para obter mais informações sobre a autenticação personalizada, consulte [Implementando uma extensão de segurança](../extensions/security-extension/implementing-a-security-extension.md).  
  
 Além disso, se você desejar usar a autenticação de formulários ou uma extensão de autenticação personalizada em um ambiente do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrado a um produto do SharePoint, deverá configurar o site do SharePoint para usar o método de autenticação que escolher. Para obter mais informações sobre como configurar a autenticação no SharePoint, consulte [Amostras de autenticação](https://go.microsoft.com/fwlink/?LinkId=115575) no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Developer Network (MSDN).  
  
### <a name="to-configure-a-report-server-to-use-custom-authentication"></a>Para configurar um servidor de relatório para usar a autenticação personalizada  
  
1.  Abra o RSReportServer.config em um editor de texto.  
  
2.  Localize <`Authentication`>.  
  
3.  Copie a seguinte estrutura XML:  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <Custom />  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    </Authentication>  
    ```  
  
4.  Cole-a nas entradas existentes para <`Authentication`>.  
  
     Observe que não é possível usar `Custom` com outros tipos de autenticação.  
  
5.  Salve o arquivo.  
  
6.  Abra o arquivo Web.config do servidor de relatório. Por padrão, ele está localizado em \Arquivos de Programas\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\ReportServer.  
  
7.  Encontre `authentication mode` e defini-lo `Forms`.  
  
    ```  
    <authentication mode = "Forms" />  
    ```  
  
8.  Localize `identity impersonate` e defina-o como `False`.  
  
    ```  
    <identity impersonate = "false" />  
    ```  
  
9. Abra o arquivo Web.config para o Gerenciador de Relatórios. Por padrão, ele está localizado em \Arquivos de Programas\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\ReportManager.  
  
10. Encontre `authentication mode` e defini-lo `Forms`.  
  
    ```  
    <authentication mode = "Forms" />  
    ```  
  
11. Localize `identity impersonate` e defina-o como `False`.  
  
    ```  
    <identity impersonate = "false" />  
    ```  
  
12. Adicione a estrutura de elementos `PassThroughCookies` ao arquivo de configuração. Para obter mais informações, consulte [Configurar o Gerenciador de Relatórios para transmitir cookies de autenticação personalizados](configure-the-web-portal-to-pass-custom-authentication-cookies.md).  
  
13. Salve o arquivo.  
  
14. Se você configurou uma implantação em expansão, repita todas as etapas anteriores para outros servidores de relatório na implantação.  
  
15. Reinicie o servidor de relatório para terminar as sessões que estão atualmente abertas.  
  
## <a name="see-also"></a>Consulte também  
 [Implementando uma extensão de segurança](../extensions/security-extension/implementing-a-security-extension.md)   
 [Autenticação com o servidor de relatório](authentication-with-the-report-server.md)   
 [Arquivo de configuração RSReportServer](../report-server/rsreportserver-config-configuration-file.md)   
 [Configurar a autenticação Básica no servidor de relatório](configure-basic-authentication-on-the-report-server.md)   
 [Configurar a Autenticação do Windows no servidor de relatório](configure-windows-authentication-on-the-report-server.md)  
  
  
