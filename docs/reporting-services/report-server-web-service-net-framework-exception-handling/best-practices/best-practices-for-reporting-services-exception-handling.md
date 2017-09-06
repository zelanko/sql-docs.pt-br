---
title: "Práticas recomendadas para tratamento de exceções de serviços de relatório | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
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
- exceptions [Reporting Services], best practices
ms.assetid: 72fecf28-f02e-4338-b50f-0b21f520302d
caps.latest.revision: 34
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 8f6546605af6bb6c23b6b380fbaf7042d093addf
ms.contentlocale: pt-br
ms.lasthandoff: 08/12/2017

---
# <a name="best-practices-for-reporting-services-exception-handling"></a>Práticas recomendadas para a manipulação de exceção do Reporting Services
  Durante o desenvolvimento de aplicativos do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], existem várias metodologias que você pode usar para eliminar ou reduzir a ocorrência de exceções. Quando houver exceções, forneça mensagens de erro claras e concisas ao usuário e adicione manipulação de exceção adequada para impedir que seus aplicativos sejam encerrados de forma inesperada.  
  
 Um aplicativo que envia solicitações ao serviço Web Servidor de Relatório deve fazer o seguinte:  
  
-   Evitar as exceções impedindo quantas solicitações inválidas for possível.  
  
-   Capturar exceções e fornecer código de manipulação de erro específico sempre que possível.  
  
-   Lidar com casos de erro que não lançam exceções.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Impedir solicitações inválidas](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/preventing-invalid-requests.md)|Descreve técnicas para impedir que solicitações que não são válidas sejam enviadas ao servidor de relatório.|  
|[Usar blocos try e catch](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-try-and-catch-blocks.md)|Descreve como aprimorar ainda mais a confiabilidade de seu aplicativo com blocos try/catch.|  
|[Manipular avisos e casos que não causam exceções](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/handling-warnings-and-cases-that-do-not-cause-exceptions.md)|Explica como manipular erros que não resultam em uma exceção é lançada pelo [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
|[Usando a propriedade Detail para manipular erros específicos](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)|Explica como manipular programaticamente erros específicos usando o **detalhes** propriedade o **SoapException** objeto.|  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade Detail](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)   
 [Introdução ao tratamento de exceção no Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services classe SoapException](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
