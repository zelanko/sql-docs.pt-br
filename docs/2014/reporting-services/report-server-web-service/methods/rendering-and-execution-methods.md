---
title: Métodos de renderização e execução | Microsoft Docs
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
- rendered reports [Reporting Services]
- reports [Reporting Services], execution options
- methods [Reporting Services], execution options
- methods [Reporting Services], rendering
ms.assetid: 12626aad-f0be-4653-87d0-60eb3a3fff78
caps.latest.revision: 35
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: bd1745f845cda954c0e447a8a1d035646fd298dc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116290"
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
  
## <a name="see-also"></a>Consulte também  
 [Criando aplicativos usando o serviço Web e o .NET Framework](../net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Serviço Web do Servidor de Relatório](../report-server-web-service.md)   
 [Métodos do serviço Web Servidor de Relatórios](report-server-web-service-methods.md)   
 [Referência técnica &#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  