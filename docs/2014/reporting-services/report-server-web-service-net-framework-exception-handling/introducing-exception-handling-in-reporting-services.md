---
title: Introdução ao tratamento de exceção no Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
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
manager: kfile
ms.openlocfilehash: 091b1f40d293515617e369b750a5f18dfe12951b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63012321"
---
# <a name="introducing-exception-handling-in-reporting-services"></a>Introduzindo a manipulação de exceção no Reporting Services
  Se o seu aplicativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] enviar uma solicitação ao serviço Web Servidor de Relatórios que o serviço não for capaz de processar, ele retornará uma exceção SOAP ao cliente. A manipulação de exceções lançada pelo serviço Web Servidor de Relatórios é uma parte importante dos aplicativos desenvolvidos por você, já que é possível retornar informações úteis para os usuários quando erros ocorrerem.  
  
 Esta seção contém informações específicas sobre a manipulação de exceções, como impedir a entrada de usuário que não seja válida e o retorno de informações de erro significativas para usuários. Para obter informações gerais sobre a manipulação de exceções, consulte "manipulando e gerando exceções" na documentação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|DESCRIÇÃO|  
|-----------|-----------------|  
|[Manipulando exceções no Reporting Services](handling-exceptions-in-reporting-services.md)|Oferece uma visão geral sobre exceções no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e sobre a função de SOAP no retorno de erros de um serviço Web.|  
|[Práticas recomendadas para a manipulação de exceção do Reporting Services](best-practices/best-practices-for-reporting-services-exception-handling.md)|Oferece recomendações sobre como manipular exceções no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[Classe SoapException do Reporting Services +](soapexception-class/reporting-services-soapexception-class.md)|Descreve a classe **SoapException** no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
## <a name="see-also"></a>Consulte Também  
 [Compilar aplicativos usando o Serviço Web e o .NET Framework](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
