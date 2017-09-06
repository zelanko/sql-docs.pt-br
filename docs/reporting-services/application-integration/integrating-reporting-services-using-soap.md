---
title: Integrar o Reporting Services usando SOAP | Microsoft Docs
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
- Report Server Web service, application integration
- SOAP [Reporting Services]
- SOAP [Reporting Services], about report integration
- integrating reports [Reporting Services]
- Web service [Reporting Services], application integration
ms.assetid: 6bc17af5-883c-4bfa-87d9-48cd7056d145
caps.latest.revision: 45
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: f993204ae0c9140a5fba51c125ce1d57d0e3a125
ms.contentlocale: pt-br
ms.lasthandoff: 08/12/2017

---
# <a name="integrating-reporting-services-using-soap"></a>Integrando o Reporting Services por meio do acesso de SOAP
  O [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] API SOAP fornece vários pontos de extremidade de serviço de Web para o desenvolvimento de soluções de relatório personalizadas. Atualmente, os pontos de extremidade recaem em duas categorias: gerenciamento e execução. A funcionalidade de gerenciamento é exposta por meio dos pontos de extremidade <xref:ReportService2005>, <xref:ReportService2006> e <xref:ReportService2010>. O ponto de extremidade <xref:ReportService2005> é usado para o gerenciamento de um servidor de relatório configurado em modo nativo e o ponto de extremidade <xref:ReportService2006> é usado para o gerenciamento de um servidor de relatório configurado para modo integrado do SharePoint. O <xref:ReportService2010> mescla as funcionalidades de <xref:ReportService2005> e <xref:ReportService2006> e pode gerenciar um servidor de relatório configurado para modo nativo ou integrado do SharePoint.  
  
> [!NOTE]  
>  Os pontos de extremidade <xref:ReportService2005> e <xref:ReportService2006> foram preteridos no [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. O ponto de extremidade <xref:ReportService2010> inclui as funcionalidades dos dois pontos de extremidade e contém recursos de gerenciamento adicionais.  
  
 A funcionalidade de execução é exibida por meio do ponto de extremidade <xref:ReportExecution2005> e é usado quando um servidor de relatório é configurado em modo nativo ou integrado do SharePoint. Os tópicos a seguir mostram como esses pontos de extremidade podem ser usados para desenvolver soluções de relatório no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, SharePoint e em aplicativos Web.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Usando a API SOAP em um aplicativo do Windows](../../reporting-services/application-integration/integrating-reporting-services-using-soap-windows-application.md)  
 Descreve como usar a API SOAP para integrar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a um ambiente Windows.  
  
 [Usando a API SOAP em um aplicativo Web](../../reporting-services/application-integration/integrating-reporting-services-using-soap-web-application.md)  
 Descreve como usar a API SOAP para integrar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a um ambiente Web.  
  
## <a name="see-also"></a>Consulte também  
 [Integrando o Reporting Services em aplicativos](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [Serviço Web servidor de relatório](../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Criando aplicativos que usam o serviço Web e o .NET Framework](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
