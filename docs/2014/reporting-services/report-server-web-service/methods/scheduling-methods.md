---
title: Métodos de agendamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- schedules [Reporting Services], methods
- reports [Reporting Services], scheduling
- shared schedules [Reporting Services], methods
- methods [Reporting Services], scheduling
ms.assetid: 68ae13f9-d91e-4572-a82a-8fa42001569e
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 030eb0575b52ea6f0008b76658f94eaa03a04341
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56022537"
---
# <a name="scheduling-methods"></a>Métodos de agendamento
  É possível usar esses métodos para criar e gerenciar agendas compartilhadas para execução e entrega de relatório e para planos de atualização do cache utilizados pelo servidor de relatório.  
  
|Método|Ação|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.CreateCacheRefreshPlan%2A>|Cria um plano de atualização do cache para um item.|  
|<xref:ReportService2010.ReportingService2010.CreateSchedule%2A>|Cria uma nova agenda compartilhada.|  
|<xref:ReportService2010.ReportingService2010.DeleteCacheRefreshPlan%2A>|Exclui um plano de atualização do cache.|  
|<xref:ReportService2010.ReportingService2010.DeleteSchedule%2A>|Exclui uma agenda compartilhada com base em uma ID de agenda específica.|  
|<xref:ReportService2010.ReportingService2010.GetCacheRefreshPlanProperties%2A>|Retorna as propriedades do plano de atualização do cache especificado.|  
|<xref:ReportService2010.ReportingService2010.GetScheduleProperties%2A>|Retorna os valores de propriedades de uma agenda compartilhada.|  
|<xref:ReportService2010.ReportingService2010.ListCacheRefreshPlans%2A>|Retorna uma lista dos planos de atualização do cache associados a um item do catálogo.|  
|<xref:ReportService2010.ReportingService2010.ListScheduledItems%2A>|Retorna uma lista de itens associados a uma agenda compartilhada.|  
|<xref:ReportService2010.ReportingService2010.ListSchedules%2A>|Retorna uma lista de todas as agendas compartilhadas no servidor de relatório ou no site do SharePoint.|  
|<xref:ReportService2010.ReportingService2010.ListScheduleStates%2A>|Retorna uma lista de estados de agenda com suporte.|  
|<xref:ReportService2010.ReportingService2010.PauseSchedule%2A>|Pausa a execução de uma determinada agenda.|  
|<xref:ReportService2010.ReportingService2010.ResumeSchedule%2A>|Retoma uma agenda compartilhada que foi pausada.|  
|<xref:ReportService2010.ReportingService2010.SetCacheRefreshPlanProperties%2A>|Define as propriedades de um plano de atualização do cache.|  
|<xref:ReportService2010.ReportingService2010.SetScheduleProperties%2A>|Define o valor de propriedades de uma agenda compartilhada.|  
  
## <a name="see-also"></a>Consulte também  
 [Criando aplicativos usando o serviço Web e o .NET Framework](../net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Serviço Web do Servidor de Relatório](../report-server-web-service.md)   
 [Métodos do serviço Web Servidor de Relatórios](report-server-web-service-methods.md)   
 [Referência técnica &#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  
