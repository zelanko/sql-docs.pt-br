---
title: "Criação de aplicativos usando o serviço Web e o .NET Framework | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Report Server Web service, application building
- .NET Framework [Reporting Services]
- XML Web service [Reporting Services], client creation
- reports [Reporting Services], building
- Web service [Reporting Services], application building
- Report Server Web service, client creation
- client configuration [Reporting Services]
- XML Web service [Reporting Services], application building
- Web service [Reporting Services], client creation
ms.assetid: 92a9678c-bc4f-4d7a-ba44-85989bfe27ca
caps.latest.revision: 38
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 58588838e0e74b545290df5ff0e77dc68ad5e918
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="building-applications-using-the-web-service-and-the-net-framework"></a>Building Applications Using the Web Service and the .NET Framework
  Com o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], você pode usar construções de programação familiares, como métodos de tipos primitivos, e tipos complexos definidos pelo usuário para trabalhar com serviços Web. O [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] contém uma infraestrutura e ferramentas que você poderá usar para criar clientes do serviço Web que pode chamar qualquer serviço Web compatível com os padrões do W3C (World Wide Web Consortium).  
  
 Um cliente de serviço Web Servidor de Relatórios é qualquer componente ou aplicativo que se comunica com um servidor de relatório que usa mensagens SOAP.  
  
 **Para criar um cliente de serviço Web servidor de relatórios usando o .NET Framework, siga estas etapas básicas:**  
  
1.  Crie uma classe proxy para o serviço Web.  
  
     Para fazer isso, adicione uma classe proxy ou referência da Web ao seu projeto de desenvolvimento, referencie a classe proxy do seu código cliente e crie uma instância desse proxy. Para obter mais informações, consulte [criar o Proxy de serviço Web](../../../reporting-services/report-server-web-service/net-framework/creating-the-web-service-proxy.md).  
  
2.  Autentique o cliente de serviço Web com o servidor de relatório.  
  
     Para fazer isso, defina a propriedade <xref:System.Web.Services.Protocols.WebClientProtocol.Credentials%2A> igual às credenciais de um usuário autenticado no servidor de relatório. Para obter mais informações, consulte [autenticação de serviço Web](../../../reporting-services/report-server-web-service/net-framework/web-service-authentication.md).  
  
3.  Chame o método da classe proxy que corresponde à operação de serviço Web que você deseja invocar.  
  
     Para fazer isso, chame um método de serviço Web e forneça os argumentos necessários. Para obter mais informações sobre os métodos de serviço da Web, consulte [métodos de Web do serviço do servidor de relatório](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md). Para obter mais informações sobre como chamar, consulte [chamando métodos do serviço Web](../../../reporting-services/report-server-web-service/net-framework/calling-web-service-methods.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Criando o Proxy do serviço Web](../../../reporting-services/report-server-web-service/net-framework/creating-the-web-service-proxy.md)|Descreve as maneiras de adicionar uma classe proxy ao seu projeto usando [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].|  
|[Autenticação de serviço Web](../../../reporting-services/report-server-web-service/net-framework/web-service-authentication.md)|Descreve como as chamadas ao serviço Web Servidor de Relatório é autenticado.|  
|[Chamando métodos de serviço Web](../../../reporting-services/report-server-web-service/net-framework/calling-web-service-methods.md)|Descreve como usar a API SOAP para chamar métodos de serviço Web em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].|  
|[Definindo a propriedade Url do serviço Web](../../../reporting-services/report-server-web-service/net-framework/setting-the-url-property-of-the-web-service.md)|Explica como direcionar seu proxy de serviço Web programaticamente a uma URL do novo servidor depois de criar a sua referência da Web.|  
|[Fornecendo argumentos de método de serviço Web](../../../reporting-services/report-server-web-service/net-framework/supplying-web-service-method-arguments.md)|Descreve como invocar um método de serviço Web e fornecer argumentos de método.|  
|[Omitindo valores para objetos de serviço da Web opcionais](../../../reporting-services/report-server-web-service/net-framework/omitting-values-for-optional-web-service-objects.md)|Descreve como omitir valores para objetos de serviço Web opcionais.|  
|[Usando métodos do serviço da Web seguro](../../../reporting-services/report-server-web-service/net-framework/using-secure-web-service-methods.md)|Descreve o **SecureConnectionLevel** configuração e a maneira na qual ele afeta o uso da API de SOAP do Reporting Services.|  
|[Passando configurações de informações de dispositivos para extensões de renderização](../../../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)|Descreve as configurações de informações de dispositivo usadas para renderizar relatórios a formatos diferentes.|  
|[Configurações de extensão de entrega do Reporting Services](../../../reporting-services/report-server-web-service/net-framework/reporting-services-delivery-extension-settings.md)|Descreve as configurações usadas para entregar relatórios usando o email do servidor de relatório.|  
|[Usando o Reporting Services cabeçalhos SOAP](../../../reporting-services/report-server-web-service-net-framework-soap-headers/using-reporting-services-soap-headers.md)|Explica o uso de cabeçalhos SOAP no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
|[Introdução ao tratamento de exceção no Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)|Fornece informações sobre o modo no qual o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] manipula erros.|  
  
## <a name="see-also"></a>Consulte também  
 [Serviço Web servidor de relatório](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Referência técnica &#40; SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
