---
title: "Melhores práticas para tratamento de exceção do Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-server-web-service-net-framework-exception-handling
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: exceptions [Reporting Services], best practices
ms.assetid: 72fecf28-f02e-4338-b50f-0b21f520302d
caps.latest.revision: "34"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e6ae230c7d3e21ad4b5ac19ab791f63db8d51c50
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
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
|[Usar a propriedade Detail para manipular erros específicos](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)|Explica como tratar erros específicos de forma programática usando a propriedade **Detail** do objeto **SoapException**.|  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade Detail](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)   
 [Introdução ao tratamento de exceção no Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Classe SoapException do Reporting Services +](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
