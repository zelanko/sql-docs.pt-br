---
title: Introdução ao tratamento de exceção no Reporting Services | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service-net-framework-exception-handling
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], exception handling
- errors [Reporting Services]
- exceptions [Reporting Services]
- Report Server Web service, exception handling
- XML Web service [Reporting Services], exception handling
ms.assetid: 54381870-ce67-482b-aa83-6a838cdbf9b9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ee084e9d85a1bee21db3994be8b9473daefc7c0f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "62992235"
---
# <a name="introducing-exception-handling-in-reporting-services"></a>Introduzindo a manipulação de exceção no Reporting Services
  Se o seu aplicativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] enviar uma solicitação ao serviço Web Servidor de Relatórios que o serviço não for capaz de processar, ele retornará uma exceção SOAP ao cliente. A manipulação de exceções lançada pelo serviço Web Servidor de Relatórios é uma parte importante dos aplicativos desenvolvidos por você, já que é possível retornar informações úteis para os usuários quando erros ocorrerem.  
  
 Esta seção contém informações específicas sobre a manipulação de exceções, como impedir a entrada de usuário que não seja válida e o retorno de informações de erro significativas para usuários. Para obter informações gerais sobre o tratamento de exceção, confira “Tratar e gerar exceções” na documentação do SDK do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Tratamento de exceções no Reporting Services](../../reporting-services/report-server-web-service-net-framework-exception-handling/handling-exceptions-in-reporting-services.md)|Oferece uma visão geral sobre exceções no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e sobre a função de SOAP no retorno de erros de um serviço Web.|  
|[Práticas recomendadas para tratamento de exceções do Reporting Services](../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/best-practices-for-reporting-services-exception-handling.md)|Oferece recomendações sobre como manipular exceções no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[Classe SoapException do Reporting Services +](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)|Descreve a classe **SoapException** no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
## <a name="see-also"></a>Consulte Também  
 [Compilar aplicativos usando o Serviço Web e o .NET Framework](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
