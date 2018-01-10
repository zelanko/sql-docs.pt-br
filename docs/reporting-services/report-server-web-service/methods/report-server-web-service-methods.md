---
title: "Métodos do serviço Web Servidor de Relatórios | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-server-web-service
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- Report Server Web service, methods
- Web service [Reporting Services], methods
- XML Web service [Reporting Services], features
- Web service [Reporting Services], features
- Report Server Web service, features
- XML Web service [Reporting Services], methods
ms.assetid: ce5afa27-e90c-44a7-b204-098a065b3665
caps.latest.revision: "49"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: c577245ad46a2989d7e3c7fbc33a1f9e8cfc19e7
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="report-server-web-service-methods"></a>Métodos de serviço Web Servidor de Relatórios
  Os serviços Web Servidor de Relatórios incluem várias categorias de métodos que se baseiam em recursos de componente. Esses métodos são fornecidos através de vários pontos de extremidade de serviço Web (três para gerenciamento de relatórios e um para execução de relatórios), os quais são expostos como membros das classes <xref:ReportService2010.ReportingService2010> e <xref:ReportExecution2005.ReportExecutionService>. Essas classes podem ser geradas por meio de uma ferramenta de classe proxy como wsdl.exe, que está incluída no SDK do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Para obter mais informações sobre os serviços Web Servidor de Relatórios e o [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], consulte [Criando aplicativos usando o serviço Web e o .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md).  
  
## <a name="endpoints-and-methods"></a>Pontos de extremidade e métodos  
 A tabela a seguir lista os pontos de extremidade do serviço Web Servidor de Relatórios e as categorias de métodos fornecidas pelo ponto de extremidade <xref:ReportService2010.ReportingService2010>. Para obter informações sobre os métodos disponíveis nos outros pontos de extremidade, consulte [Referência técnica &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md).  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Pontos de extremidade do serviço Web Servidor de Relatórios](../../../reporting-services/report-server-web-service/methods/report-server-web-service-endpoints.md)|Descreve os pontos de extremidade de gerenciamento e execução do serviço Web Servidor de Relatórios.|  
|[Métodos de gerenciamento de namespace do Servidor de Relatório](../../../reporting-services/report-server-web-service/methods/report-server-namespace-management-methods.md)|Descreve métodos que você pode usar para gerenciar o banco de dados do servidor de relatório. Você pode especificamente gerenciar pastas e recursos e definir propriedades de item.|  
|[Métodos de autorização](../../../reporting-services/report-server-web-service/methods/authorization-methods.md)|Descreve métodos que você pode usar para gerenciar tarefas, funções e políticas.|  
|[Fontes de dados e métodos de conexão](../../../reporting-services/report-server-web-service/methods/data-sources-and-connection-methods.md)|Descreve métodos que você pode usar para definir e gerenciar informações da conexão da fonte de dados e de credenciais para relatórios.|  
|[Métodos de parâmetros de relatório](../../../reporting-services/report-server-web-service/methods/report-parameters-methods.md)|Descreve métodos que você pode usar para definir e recuperar parâmetros para relatórios.|  
|[Métodos de modelo – Serviço Web do Servidor de Relatório](../../../reporting-services/report-server-web-service/methods/model-methods-report-server-web-service.md)|Descreve métodos que você pode usar para gerenciar modelos.|  
|[Métodos de renderização e execução](../../../reporting-services/report-server-web-service/methods/rendering-and-execution-methods.md)|Descreve métodos que você pode usar para gerenciar a execução, a renderização e o armazenamento de relatórios em cache.|  
|[Métodos de histórico de relatório](../../../reporting-services/report-server-web-service/methods/report-history-methods.md)|Descreve métodos que você pode usar para criar e gerenciar instantâneos de histórico de relatório.|  
|[Métodos de agendamento](../../../reporting-services/report-server-web-service/methods/scheduling-methods.md)|Descreve métodos que você pode usar para criar e gerenciar agendas compartilhadas e armazenar em cache planos de atualização que são usados pelo servidor de relatório.|  
|[Métodos de assinatura e de entrega](../../../reporting-services/report-server-web-service/methods/subscription-and-delivery-methods.md)|Descreve métodos que você pode usar para criar e gerenciar assinaturas e entrega de relatório.|  
|[Métodos de relatórios vinculados](../../../reporting-services/report-server-web-service/methods/linked-reports-methods.md)|Descreve métodos que você pode usar para criar e gerenciar relatórios vinculados.|  
  
## <a name="see-also"></a>Consulte Também  
 [Acessando a API SOAP](../../../reporting-services/report-server-web-service/accessing-the-soap-api.md)   
 [Criando aplicativos usando o serviço Web e o .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Serviço Web do Servidor de Relatório](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Referência técnica &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
