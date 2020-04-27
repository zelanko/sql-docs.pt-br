---
title: Métodos de gerenciamento de namespace do Servidor de Relatório | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- reports [Reporting Services], managing
- management methods [Reporting Services]
- methods [Reporting Services], about methods
- methods [Reporting Services]
ms.assetid: 2aa43ce9-f51e-408a-8ce0-b40d3dd62561
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 64827063e6e406f91307e7db1b33d6b42a196168
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63283982"
---
# <a name="report-server-namespace-management-methods"></a>Métodos de gerenciamento de namespace do Servidor de Relatório
  O serviço Web de Gerenciamento do Servidor de Relatório contém métodos que podem ser usados para gerenciar relatórios, pastas e recursos no banco de dados do servidor de relatório.  
  
|Método|Ação|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.CancelJob%2A>|Cancela a execução de um trabalho.|  
|<xref:ReportService2010.ReportingService2010.CreateFolder%2A>|Adiciona uma pasta ao banco de dados do servidor de relatório ou à biblioteca do SharePoint.|  
|<xref:ReportService2010.ReportingService2010.CreateCatalogItem%2A>|Adiciona um novo item a um banco de dados do servidor de relatório ou à biblioteca do SharePoint. Esse método aplica-se aos tipos de item `Report`, `Model`, `Dataset`, `Component`, `Resource` e `DataSource`.|  
|M:ReportService2010.ReportingService2010.CreateReportEditSession(System.String,System.String,System.Byte[],ReportService2010.Warning[]@)|Cria uma nova sessão de edição de relatório.|  
|<xref:ReportService2010.ReportingService2010.DeleteItem%2A>|Remove um item do banco de dados do servidor de relatório ou da biblioteca do SharePoint.|  
|<xref:ReportService2010.ReportingService2010.FindItems%2A>|Retorna os itens do banco de dados do servidor de relatório ou da biblioteca do SharePoint que correspondem aos critérios de pesquisa especificados.|  
|<xref:ReportService2010.ReportingService2010.FireEvent%2A>|Dispara um evento baseado nos parâmetros fornecidos.|  
|<xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A>|Retorna uma lista de configurações para uma determinada extensão.|  
|<xref:ReportService2010.ReportingService2010.GetItemType%2A>|Recupera o tipo de um item no banco de dados do servidor de relatório ou na biblioteca do SharePoint, se o item existir.|  
|<xref:ReportService2010.ReportingService2010.GetProperties%2A>|Retorna os valores de uma ou mais propriedades de um item do banco de dados do servidor de relatório ou da biblioteca do SharePoint.|  
|<xref:ReportService2010.ReportingService2010.GetItemDefinition%2A>|Recupera a definição ou o conteúdo de um item. Esse método aplica-se aos tipos de item `Report`, `Model`, `Dataset`, `Component`, `Resource` e `DataSource`.|  
|<xref:ReportService2010.ReportingService2010.GetItemReferences%2A>|Retorna uma lista de referências de itens do catálogo associadas a um item.|  
|<xref:ReportService2010.ReportingService2010.GetReportServerConfigInfo%2A>|Retorna informações sobre a instância do servidor de relatório conectada ou sobre todas as instâncias do servidor de relatório em uma implantação em expansão.|  
|<xref:ReportService2010.ReportingService2010.GetSystemProperties%2A>|Retorna uma ou mais propriedades do sistema.|  
|<xref:ReportService2010.ReportingService2010.ListChildren%2A>|Obtém uma lista de filhos de uma pasta especificada.|  
|<xref:ReportService2010.ReportingService2010.ListDatabaseCredentialRetrievalOptions%2A>|Retorna uma lista de opções de recuperação de credenciais com suporte.|  
|<xref:ReportService2010.ReportingService2010.ListEvents%2A>|Retorna uma lista de extensões de evento conforme eles aparecem no arquivo de configuração do servidor de relatório.|  
|<xref:ReportService2010.ReportingService2010.ListJobs%2A>|Retorna uma lista de trabalhos em execução no servidor de relatório.|  
|<xref:ReportService2010.ReportingService2010.ListExtensions%2A>|Retorna uma lista de extensões configuradas para um determinado tipo de extensão.|  
|<xref:ReportService2010.ReportingService2010.ListExtensionTypes%2A>|Retorna uma lista de tipos de extensão com suporte.|  
|<xref:ReportService2010.ReportingService2010.ListItemTypes%2A>|Retorna uma lista de itens de catálogo com suporte.|  
|<xref:ReportService2010.ReportingService2010.ListJobActions%2A>|Retorna uma lista de ações de trabalho com suporte.|  
|<xref:ReportService2010.ReportingService2010.ListJobStates%2A>|Retorna uma lista de estados de trabalho com suporte.|  
|<xref:ReportService2010.ReportingService2010.ListJobTypes%2A>|Retorna uma lista de tipos de trabalho com suporte.|  
|<xref:ReportService2010.ReportingService2010.ListParents%2A>|Recupera itens pai para o item determinado.|  
|<xref:ReportService2010.ReportingService2010.ListSecurityScopes%2A>|Retorna uma lista de escopos de segurança com suporte.|  
|<xref:ReportService2010.ReportingService2010.Logoff%2A>|Faz logoff do usuário atual que está fazendo solicitações de serviço Web. Esse método aplica-se apenas ao modo nativo.|  
|<xref:ReportService2010.ReportingService2010.LogonUser%2A>|Faz logon de um usuário e autentica uma solicitação de usuário no serviço Web do Servidor de Relatório. Esse método aplica-se apenas ao modo nativo.|  
|<xref:ReportService2010.ReportingService2010.SetItemReferences%2A>|Define os itens de catálogo associados a um item.|  
|<xref:ReportService2010.ReportingService2010.MoveItem%2A>|Move e/ou renomeia um item.|  
|<xref:ReportService2010.ReportingService2010.SetProperties%2A>|Define uma ou mais propriedades de um item.|  
|<xref:ReportService2010.ReportingService2010.SetItemDefinition%2A>|Configura a definição ou o conteúdo de um item especificado. Esse método aplica-se aos tipos de item `Report`, `Model`, `Dataset`, `Component`, `Resource` e `DataSource`.|  
|<xref:ReportService2010.ReportingService2010.SetSystemProperties%2A>|Define uma ou mais propriedades do sistema no servidor de relatório ou no farm do SharePoint.|  
|<xref:ReportService2010.ReportingService2010.ValidateExtensionSettings%2A>|Valida configurações de extensão do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
  
## <a name="see-also"></a>Consulte Também  
 [Criando aplicativos usando o serviço Web e o .NET Framework](../net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Serviço Web Servidor de Relatórios](../report-server-web-service.md)   
 [Métodos do serviço Web Servidor de Relatórios](report-server-web-service-methods.md)   
 [Referência técnica &#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  
