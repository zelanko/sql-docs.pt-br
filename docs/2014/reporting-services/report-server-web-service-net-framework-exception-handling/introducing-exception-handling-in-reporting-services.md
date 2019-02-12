---
title: Introdução ao tratamento de exceção no Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], exception handling
- errors [Reporting Services]
- exceptions [Reporting Services]
- Report Server Web service, exception handling
- XML Web service [Reporting Services], exception handling
ms.assetid: 54381870-ce67-482b-aa83-6a838cdbf9b9
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: b0415d5344999b61b026ef69879b607220a72031
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56014917"
---
# <a name="introducing-exception-handling-in-reporting-services"></a>Introduzindo a manipulação de exceção no Reporting Services
  Se o seu aplicativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] enviar uma solicitação ao serviço Web Servidor de Relatórios que o serviço não for capaz de processar, ele retornará uma exceção SOAP ao cliente. A manipulação de exceções lançada pelo serviço Web Servidor de Relatórios é uma parte importante dos aplicativos desenvolvidos por você, já que é possível retornar informações úteis para os usuários quando erros ocorrerem.  
  
 Esta seção contém informações específicas sobre a manipulação de exceções, como impedir a entrada de usuário que não seja válida e o retorno de informações de erro significativas para usuários. Para obter informações gerais sobre o tratamento de exceção, consulte “Tratando e gerando exceções” na documentação do SDK do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Tratamento de exceções no Reporting Services](handling-exceptions-in-reporting-services.md)|Oferece uma visão geral sobre exceções no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e sobre a função de SOAP no retorno de erros de um serviço Web.|  
|[Práticas recomendadas para tratamento de exceções do Reporting Services](best-practices/best-practices-for-reporting-services-exception-handling.md)|Oferece recomendações sobre como manipular exceções no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[Classe SoapException do Reporting Services +](soapexception-class/reporting-services-soapexception-class.md)|Descreve a classe **SoapException** no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
## <a name="see-also"></a>Consulte também  
 [Compilar aplicativos usando o Serviço Web e o .NET Framework](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
