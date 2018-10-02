---
title: Propriedades do Reporting Services | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- report servers [Reporting Services], properties
- properties [Reporting Services], about properties
- reports [Reporting Services], properties
- Report Server Web service, properties
- report properties [Reporting Services]
- XML Web service [Reporting Services], properties
- Web service [Reporting Services], properties
- properties [Reporting Services]
ms.assetid: 8c855194-4c20-4ecc-a328-5137d54b560c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e2b7495edef06da522112932c75d5f35684313f7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47742614"
---
# <a name="reporting-services-properties"></a>Propriedades do Reporting Services
  O servidor de relatório define um conjunto de propriedades do sistema globais para ele e um conjunto de propriedades de item associadas a um item individual armazenado no banco de dados do servidor de relatório. As propriedades definidas pelo servidor de relatório não podem ser excluídas e, em alguns casos, são somente leitura. Um aplicativo pode estender as propriedades do sistema e as propriedades do item acrescentando propriedades definidas pelo usuário adicionais a elas.  
  
 Os métodos de serviço Web a seguir recuperam e definem propriedades do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
|Método|Ação|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.GetProperties%2A>|Retorna os valores de uma ou mais propriedades de um item do banco de dados do servidor de relatório.|  
|<xref:ReportService2010.ReportingService2010.GetSystemProperties%2A>|Retorna uma ou mais propriedades do sistema.|  
|<xref:ReportService2010.ReportingService2010.SetProperties%2A>|Define uma ou mais propriedades de um item no banco de dados do servidor de relatório.|  
|<xref:ReportService2010.ReportingService2010.SetSystemProperties%2A>|Define uma ou mais propriedades do sistema.|  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Propriedades do item do servidor de relatório](../../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-item-properties.md)|Descreve as propriedades específicas do item no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
|[Propriedades do sistema do Servidor de Relatório](../../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)|Descreve as propriedades específicas do sistema no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
  
## <a name="see-also"></a>Consulte Também  
 [Criando aplicativos usando o serviço Web e o .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Serviço Web do Servidor de Relatório](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Referência técnica &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
