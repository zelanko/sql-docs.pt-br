---
title: "Tratamento de exceções no Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- SOAP [Reporting Services], exceptions
- .NET Framework [Reporting Services]
- exceptions [Reporting Services], about exception handling
- SoapException object
ms.assetid: 1a443432-2db5-48c5-bc29-433b4688082f
caps.latest.revision: 31
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 7e1472c11575ba8bed99992ec9630e408c347291
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="handling-exceptions-in-reporting-services"></a>Manipulando exceções no Reporting Services
  Quando uma solicitação de cliente API SOAP do Reporting Services não pode ser concluída, o servidor de relatório retorna um erro em vez dos resultados esperados da chamada. Quando uma chamada não pode ser concluída, será retornado um erro para o serviço Web do servidor de relatório como um SOAP **falha** elemento XML. O principal elemento descritivo da falha é o **detalhes** elemento, que inclui todas as informações de erro fornecidas pelo servidor de relatório, bem como quaisquer informações adicionais de erro de serviço da Web. As informações de chave de **detalhes** elemento é o código de erro do servidor de relatório. com base na mensagem e no código de erro, você poderá determinar a próxima ação apropriada a ser tomada levar em seus aplicativos. Para obter mais informações sobre falhas SOAP, consulte o site do W3C (World Wide Web Consortium), http://www.w3.org/TR/SOAP.  
  
## <a name="soap-faults-and-the-net-framework"></a>As falhas SOAP e o .NET Framework  
 No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], se ocorrer um erro em uma solicitação de cliente para o serviço Web, o servidor de relatório comunicará o erro para o código de cliente que chama o serviço Web lançando um **SoapException** objeto. O **SoapException** encapsula as informações contidas em uma falha SOAP. O **detalhes** propriedade o **SoapException** mapeia para o **detalhes** elemento na Falha SOAP. Aplicativos devem capturar a **SoapException** do objeto com um bloco try/catch e usar o **detalhes** propriedade o **SoapException** para tomar as devidas providências. Para obter mais informações sobre o **SoapException** classe e o **detalhes** propriedade [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [classe SoapException dos serviços de relatório](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md). Para obter mais informações sobre o **SoapException** de classe, consulte o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] documentação do SDK.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade Detail](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)   
 [Introdução ao tratamento de exceção no Reporting Services](../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services classe SoapException](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
