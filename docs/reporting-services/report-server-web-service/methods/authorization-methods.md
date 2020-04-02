---
title: Métodos de autorização | Microsoft Docs
description: No Reporting Services, você pode usar esses métodos de autorização para gerenciar tarefas, funções e políticas no servidor de relatório.
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- security [Reporting Services], reports
- authorization [Reporting Services]
- reports [Reporting Services], security
- tasks [Reporting Services]
- roles [Reporting Services], methods
ms.assetid: 45e9cf2c-facf-4801-9482-c855403f42a8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5a8c9ba25c3f9dfd03aa528b4d02f9e02e197546
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79509827"
---
# <a name="authorization-methods"></a>Métodos de autorização
  Você pode usar estes métodos para gerenciar tarefas, funções e políticas no servidor de relatório.  
  
|Método|Ação|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.CreateRole%2A>|Adiciona uma nova função ao banco de dados do servidor de relatório. Esse método aplica-se apenas ao modo nativo.|  
|<xref:ReportService2010.ReportingService2010.DeleteRole%2A>|Exclui uma função do banco de dados do servidor de relatório. Esse método aplica-se somente ao modo nativo.|  
|<xref:ReportService2010.ReportingService2010.GetPermissions%2A>|Retorna as permissões de usuário associadas a um item específico no banco de dados do servidor de relatório ou na biblioteca do SharePoint.|  
|<xref:ReportService2010.ReportingService2010.GetPolicies%2A>|Retorna as políticas associadas a um item específico no banco de dados do servidor de relatório ou na biblioteca do SharePoint.|  
|<xref:ReportService2010.ReportingService2010.GetRoleProperties%2A>|Retorna propriedades de metadados de função e uma coleção de tarefas associadas.|  
|<xref:ReportService2010.ReportingService2010.GetSystemPermissions%2A>|Retorna as permissões de sistema do usuário. Esse método aplica-se somente ao modo nativo.|  
|<xref:ReportService2010.ReportingService2010.GetSystemPolicies%2A>|Retorna as políticas do sistema, incluindo grupos e funções aos quais elas estão associadas. Esse método aplica-se somente ao modo nativo.|  
|<xref:ReportService2010.ReportingService2010.InheritParentSecurity%2A>|Exclui as políticas associadas a um item específico no banco de dados do servidor de relatório e define as políticas de segurança do item como as do respectivo pai.|  
|<xref:ReportService2010.ReportingService2010.IsSSLRequired%2A>|Retorna um valor booliano que indica se o protocolo SSL é exigido para usar o ponto de extremidade <xref:ReportService2010>.|  
|<xref:ReportService2010.ReportingService2010.ListRoles%2A>|Retorna os nomes e as descrições das funções gerenciadas pelo servidor de relatório.|  
|<xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A>|Retorna uma lista de métodos SOAP no ponto de extremidade <xref:ReportExecution2005> que exigem uma conexão segura quando invocados. A configuração de **SecureConnectionLevel** do servidor de relatório é usada para determinar quais métodos são retornados.|  
|<xref:ReportService2010.ReportingService2010.ListTasks%2A>|Retorna as tarefas gerenciadas pelo servidor de relatório.|  
|<xref:ReportService2010.ReportingService2010.SetPolicies%2A>|Define as políticas associadas a um item especificado.|  
|<xref:ReportService2010.ReportingService2010.SetRoleProperties%2A>|Define propriedades de metadados de função e associa um conjunto de tarefas a uma função. Esse método aplica-se somente ao modo nativo.|  
|<xref:ReportService2010.ReportingService2010.SetSystemPolicies%2A>|Define a política do sistema que define grupos e as funções associadas a eles. Esse método aplica-se somente ao modo nativo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Criando aplicativos usando o serviço Web e o .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Serviço Web Servidor de Relatórios](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Métodos do serviço Web Servidor de Relatórios](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)   
 [Referência técnica &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
