---
title: Integrando o Reporting Services usando o SOAP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Report Server Web service, application integration
- SOAP [Reporting Services]
- SOAP [Reporting Services], about report integration
- integrating reports [Reporting Services]
- Web service [Reporting Services], application integration
ms.assetid: 6bc17af5-883c-4bfa-87d9-48cd7056d145
caps.latest.revision: 44
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 048542ac50d5be714bb56f044df7eaa524bf27e8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37309436"
---
# <a name="integrating-reporting-services-using-soap"></a>Integrando o Reporting Services por meio do acesso de SOAP
  A API SOAP do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece vários pontos de extremidade de serviço Web para o desenvolvimento de soluções de relatório personalizadas. Atualmente, os pontos de extremidade recaem em duas categorias: gerenciamento e execução. A funcionalidade de gerenciamento é exposta por meio dos pontos de extremidade <xref:ReportService2005>, <xref:ReportService2006> e <xref:ReportService2010>. O ponto de extremidade <xref:ReportService2005> é usado para o gerenciamento de um servidor de relatório configurado em modo nativo e o ponto de extremidade <xref:ReportService2006> é usado para o gerenciamento de um servidor de relatório configurado para modo integrado do SharePoint. O <xref:ReportService2010> mescla as funcionalidades de <xref:ReportService2005> e <xref:ReportService2006> e pode gerenciar um servidor de relatório configurado para modo nativo ou integrado do SharePoint.  
  
> [!NOTE]  
>  Os pontos de extremidade <xref:ReportService2005> e <xref:ReportService2006> foram preteridos no [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. O ponto de extremidade <xref:ReportService2010> inclui as funcionalidades dos dois pontos de extremidade e contém recursos de gerenciamento adicionais.  
  
 A funcionalidade de execução é exibida por meio do ponto de extremidade <xref:ReportExecution2005> e é usado quando um servidor de relatório é configurado em modo nativo ou integrado do SharePoint. Os tópicos a seguir mostram como esses pontos de extremidade podem ser usados para desenvolver soluções de relatório no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, SharePoint e em aplicativos Web.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Usando a API SOAP em um aplicativo do Windows](integrating-reporting-services-using-soap-windows-application.md)  
 Descreve como usar a API SOAP para integrar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a um ambiente Windows.  
  
 [Usando a API SOAP em um aplicativo Web](integrating-reporting-services-using-soap-web-application.md)  
 Descreve como usar a API SOAP para integrar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a um ambiente Web.  
  
## <a name="see-also"></a>Consulte também  
 [Integrando o Reporting Services em aplicativos](../application-integration/integrating-reporting-services-into-applications.md)   
 [Serviço Web do Servidor de Relatório](../report-server-web-service/report-server-web-service.md)   
 [Compilar aplicativos usando o Serviço Web e o .NET Framework](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
