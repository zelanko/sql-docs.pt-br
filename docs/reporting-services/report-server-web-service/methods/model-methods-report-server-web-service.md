---
title: "Métodos de modelo – serviço Web Servidor de Relatórios | Microsoft Docs"
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
applies_to: SQL Server 2016 Preview
ms.assetid: d3e658c9-bb22-480b-a3d5-bcde8f537ab2
caps.latest.revision: "4"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: c9730c12ed92d1035238b6836016b0f62e03bba0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="model-methods---report-server-web-service"></a>Métodos de modelo – serviço Web Servidor de Relatórios
  Você pode usar estes métodos para gerenciar modelos.  
  
|Método|Ação|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.GenerateModel%2A>|Gera um modelo padrão com base em uma fonte de dados compartilhada.|  
|<xref:ReportService2010.ReportingService2010.GetModelItemPermissions%2A>|Recupera as permissões de usuário associadas ao item de modelo.|  
|<xref:ReportService2010.ReportingService2010.GetModelItemPolicies%2A>|Recupera as políticas associadas a um item de modelo.|  
|<xref:ReportService2010.ReportingService2010.GetUserModel%2A>|Retorna a parte semântica de um modelo para o usuário atual.|  
|<xref:ReportService2010.ReportingService2010.InheritModelItemParentSecurity%2A>|Exclui as políticas associadas com um item de modelo e faz com que o item de modelo herde as políticas de seu pai.|  
|<xref:ReportService2010.ReportingService2010.ListModelDrillthroughReports%2A>|Lista os relatórios de detalhamento associados a uma entidade em um modelo.|  
|<xref:ReportService2010.ReportingService2010.ListModelItemChildren%2A>|Retorna uma matriz de elementos filho de item de modelo.|  
|<xref:ReportService2010.ReportingService2010.ListModelItemTypes%2A>|Retorna uma lista de itens de modelo com suporte.|  
|<xref:ReportService2010.ReportingService2010.ListModelPerspectives%2A>|Lista os modelos e as perspectivas disponíveis para o usuário.|  
|<xref:ReportService2010.ReportingService2010.RegenerateModel%2A>|Atualiza um modelo existente com base nas alterações no esquema da fonte de dados.|  
|<xref:ReportService2010.ReportingService2010.RemoveAllModelItemPolicies%2A>|Exclui todas as políticas associadas a itens de modelo no modelo especificado.|  
|<xref:ReportService2010.ReportingService2010.SetModelDrillthroughReports%2A>|Associa um conjunto de relatórios detalhados junto com um modelo.|  
|<xref:ReportService2010.ReportingService2010.SetModelItemPolicies%2A>|Define as políticas de segurança em um item de modelo.|  
  
## <a name="see-also"></a>Consulte também  
 [Criando aplicativos usando o serviço Web e o .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Serviço Web do Servidor de Relatório](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Métodos do serviço Web Servidor de Relatórios](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)   
 [Referência técnica &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
