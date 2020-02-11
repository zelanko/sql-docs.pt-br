---
title: Criando aplicativos usando o serviço Web e o .NET Framework | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
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
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5136c67077ff90e7bbbd66ae72fed891267ba7a3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62520336"
---
# <a name="building-applications-using-the-web-service-and-the-net-framework"></a>Building Applications Using the Web Service and the .NET Framework
  Com o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], você pode usar construções de programação familiares, como métodos, tipos primitivos e tipos complexos definidos pelo usuário para trabalhar com serviços Web. O [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] contém uma infraestrutura e ferramentas que você poderá usar para criar clientes do serviço Web que pode chamar qualquer serviço Web compatível com os padrões do W3C (World Wide Web Consortium).  
  
 Um cliente de serviço Web Servidor de Relatórios é qualquer componente ou aplicativo que se comunica com um servidor de relatório que usa mensagens SOAP.  
  
 **Para criar um cliente de serviço Web servidor de relatórios usando o .NET Framework, siga estas etapas básicas:**  
  
1.  Crie uma classe proxy para o serviço Web.  
  
     Para fazer isso, adicione uma classe proxy ou referência da Web ao seu projeto de desenvolvimento, referencie a classe proxy do seu código cliente e crie uma instância desse proxy. Para obter mais informações, consulte [Criando o proxy do serviço Web](creating-the-web-service-proxy.md).  
  
2.  Autentique o cliente de serviço Web com o servidor de relatório.  
  
     Para fazer isso, defina a propriedade <xref:System.Web.Services.Protocols.WebClientProtocol.Credentials%2A> igual às credenciais de um usuário autenticado no servidor de relatório. Para obter mais informações, consulte [Autenticação de serviço Web](web-service-authentication.md).  
  
3.  Chame o método da classe proxy que corresponde à operação de serviço Web que você deseja invocar.  
  
     Para fazer isso, chame um método de serviço Web e forneça os argumentos necessários. Para obter mais informações sobre os métodos de serviço Web, consulte [Métodos do serviço Web Servidor de Relatórios](../methods/report-server-web-service-methods.md). Para obter mais informações sobre chamadas, consulte [Chamando métodos de serviço Web](calling-web-service-methods.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|DESCRIÇÃO|  
|-----------|-----------------|  
|[Criando o proxy de serviço Web](creating-the-web-service-proxy.md)|Descreve as maneiras de adicionar uma classe proxy ao seu projeto usando [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]o.|  
|[Autenticação de serviço Web](web-service-authentication.md)|Descreve como as chamadas ao serviço Web Servidor de Relatório é autenticado.|  
|[Chamando métodos do serviço Web](calling-web-service-methods.md)|Descreve como usar a API SOAP para chamar métodos de serviço Web no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].|  
|[Definindo a propriedade Url do serviço Web](setting-the-url-property-of-the-web-service.md)|Explica como direcionar seu proxy de serviço Web programaticamente a uma URL do novo servidor depois de criar a sua referência da Web.|  
|[Fornecendo argumentos de método de serviço Web](supplying-web-service-method-arguments.md)|Descreve como invocar um método de serviço Web e fornecer argumentos de método.|  
|[Omitindo valores para objetos de serviço Web opcionais](omitting-values-for-optional-web-service-objects.md)|Descreve como omitir valores para objetos de serviço Web opcionais.|  
|[Usando métodos seguros do serviço Web](using-secure-web-service-methods.md)|Descreve a configuração **SecureConnectionLevel** e a forma como ela afeta o uso da API SOAP do Reporting Services.|  
|[Passando configurações de informações de dispositivos para extensões de renderização](passing-device-information-settings-to-rendering-extensions.md)|Descreve as configurações de informações de dispositivo usadas para renderizar relatórios a formatos diferentes.|  
|[Configurações da extensão de entrega do Reporting Services](reporting-services-delivery-extension-settings.md)|Descreve as configurações usadas para entregar relatórios usando o email do servidor de relatório.|  
|[Usar cabeçalhos SOAP do Reporting Services](../../report-server-web-service-net-framework-soap-headers/using-reporting-services-soap-headers.md)|Explica o uso de cabeçalhos SOAP no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
|[Introduzindo a manipulação de exceção no Reporting Services](../../report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)|Fornece informações sobre o modo no qual o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] manipula erros.|  
  
## <a name="see-also"></a>Consulte Também  
 [Serviço Web Servidor de Relatórios](../report-server-web-service.md)   
 [Referência técnica &#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  
