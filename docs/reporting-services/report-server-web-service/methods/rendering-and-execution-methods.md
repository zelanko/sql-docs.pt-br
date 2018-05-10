---
title: Métodos de renderização e execução | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: report-server-web-service
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- rendered reports [Reporting Services]
- reports [Reporting Services], execution options
- methods [Reporting Services], execution options
- methods [Reporting Services], rendering
ms.assetid: 12626aad-f0be-4653-87d0-60eb3a3fff78
caps.latest.revision: 36
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 1d4da662ed770c6b104e53e9397321a56d4b065b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="rendering-and-execution-methods"></a>Métodos de renderização e execução
  Você pode usar estes métodos para gerenciar a execução e o cache de itens e a renderização de relatórios.  
  
|Método|Ação|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.FlushCache%2A>|Invalida o cache de um item.|  
|<xref:ReportService2010.ReportingService2010.GetCacheOptions%2A>|Retorna a configuração de cache de um item e as configurações que descrevem quando a cópia do item armazenada em cache irá expirar.|  
|<xref:ReportService2010.ReportingService2010.GetExecutionOptions%2A>|Retorna a opção de execução e as configurações associadas de um item individual.|  
|<xref:ReportService2010.ReportingService2010.ListExecutionSettings%2A>|Retorna uma lista de configurações de execução com suporte.|  
|<xref:ReportExecution2005.ReportExecutionService.Render%2A>|Processa o relatório especificado e o renderiza em um formato especificado.|  
|<xref:ReportService2010.ReportingService2010.SetCacheOptions%2A>|Configura um item a ser armazenado em cache e fornece configurações que especificam quando a cópia do item armazenada em cache irá expirar.|  
|<xref:ReportService2010.ReportingService2010.SetExecutionOptions%2A>|Define as opções de execução e as propriedades de execução associadas de um item individual.|  
|<xref:ReportService2010.ReportingService2010.UpdateItemExecutionSnapshot%2A>|Gera um instantâneo da execução de um item especificado.|  
  
## <a name="see-also"></a>Consulte Também  
 [Criando aplicativos usando o serviço Web e o .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Serviço Web do Servidor de Relatório](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Métodos do serviço Web Servidor de Relatórios](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)   
 [Referência técnica &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
