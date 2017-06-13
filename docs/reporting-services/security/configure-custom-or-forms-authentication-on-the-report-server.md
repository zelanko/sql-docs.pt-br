---
title: "Configurar a autenticação de formulários ou personalizado no servidor de relatório | Microsoft Docs"
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
- Forms authentication, configuring
- custom authentication [Reporting Services]
ms.assetid: e8601a8f-e66d-4649-8e4d-a46ca20ec7d0
caps.latest.revision: 20
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 325b7d6f1015b6e5e81565df37d1c02d20e5802f
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="configure-custom-or-forms-authentication-on-the-report-server"></a>Configurar autenticação personalizada ou de formulários no servidor de relatório

O Reporting Services fornece uma arquitetura extensível que lhe permite conectar módulos de autenticação personalizados ou baseados em formulários. Você poderá avaliar a possibilidade de implementar uma extensão de autenticação personalizada, caso os requisitos de implantação não incluam a segurança integrada do Windows ou a autenticação Básica. O cenário mais comum para uso da autenticação personalizada é no suporte ao acesso de Internet ou extranet para um aplicativo Web. Substituir a extensão de Autenticação do Windows padrão por uma extensão de personalizada proporciona a você mais controle sobre a forma como é concedido a usuários externos acesso ao servidor de relatório.  

Na prática, a implantação de uma extensão de autenticação personalizada requer várias etapas que incluem a cópia de assemblies e arquivos de aplicativo, a modificação de arquivos de configuração e teste. Este tópico se concentra apenas nas configurações de autenticação que você especifica nos arquivos de configuração.  

> [!NOTE]
>  A criação de uma extensão de autenticação personalizada requer código personalizado e experiência em segurança [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] . Se você não quiser criar uma extensão de autenticação personalizada, poderá usar grupos e contas do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory, mas deverá reduzir significativamente o escopo de uma implantação de servidor de relatório. Para obter mais informações sobre a autenticação personalizada, consulte [Implementando uma extensão de segurança](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md).

Além disso, se você quiser usar a autenticação de formulários ou uma extensão de autenticação em um ambiente de SQL Server Reporting Services que esteja integrado com um produto do SharePoint, configure o site do SharePoint para usar o método de autenticação que você escolher. Para obter mais informações sobre como configurar a autenticação no SharePoint, consulte [Amostras de autenticação](http://go.microsoft.com/fwlink/?LinkId=115575) no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Developer Network (MSDN).



### <a name="to-configure-a-report-server-to-use-custom-authentication"></a>Para configurar um servidor de relatório para usar a autenticação personalizada

1.  Abra o RSReportServer.config em um editor de texto.

2.  Localizar \< **autenticação**>.

3.  Copie a seguinte estrutura XML:

    ```
    <Authentication>
          <AuthenticationTypes>
                 <Custom />
          </AuthenticationTypes>
          <EnableAuthPersistence>true</EnableAuthPersistence>
    </Authentication>
    ```

4.  Cole-o sobre entradas existentes para \< **autenticação**>.

     Observe que não é possível usar **Personalizada** com outros tipos de autenticação.

5.  Salve o arquivo.

6.  Abra o arquivo Web.config do servidor de relatório. Por padrão, ele está localizado em \Arquivos de Programas\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\ReportServer.

7.  Localize **modo de autenticação** e defina-o para **Formulários**.

    ```
    <authentication mode = "Forms" />
    ```

8.  Localize **representação da identidade** e defina-o como **Falso**.

    ```
    <identity impersonate = "false" />  
    ```
9. Adicione a estrutura de elementos **PassThroughCookies** ao arquivo de configuração. Para obter mais informações, consulte [configurar o Portal da Web para transmitir Cookies de autenticação personalizados](../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)
  
10. Salve o arquivo.  
  
11. Se você configurou uma implantação em expansão, repita todas as etapas anteriores para outros servidores de relatório na implantação.  
  
12. Reinicie o servidor de relatório para terminar as sessões que estão atualmente abertas.  

## <a name="see-also"></a>Consulte também

[Implementando uma extensão de segurança](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)  
[Exemplo de segurança personalizada do Reporting Services (GitHub)](https://github.com/Microsoft/Reporting-Services/tree/master/CustomSecuritySample)  
[Autenticação com o servidor de relatório](../../reporting-services/security/authentication-with-the-report-server.md)   
[Arquivo de Configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[Configurar a autenticação Básica no servidor de relatório](../../reporting-services/security/configure-basic-authentication-on-the-report-server.md)   
[Configurar a Autenticação do Windows no servidor de relatório](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)  
Mais perguntas? [Tente o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
