---
title: Usando métodos seguros do serviço Web | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- SOAP [Reporting Services], secure connections
- Web service [Reporting Services], SOAP
- Report Server Web service, SOAP
- XML Web service [Reporting Services], SOAP
ms.assetid: 87329299-c2ea-4517-9148-d855726768a9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 84c0b693df2906d4ab3245df20c3b9a979cf07f6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63128807"
---
# <a name="using-secure-web-service-methods"></a>Usando métodos seguros do serviço Web
  Certos métodos do serviço Web Servidor de Relatório podem exigir uma conexão segura quando chamados. Os métodos que exigem uma conexão segura são determinados pela configuração **SecureConnectionLevel** no arquivo RSReportServer.config. O valor da configuração é um valor inteiro com um intervalo válido 0 e superior. A tabela a seguir descreve esses valores.  
  
|Nível|Descrição|  
|-----------|-----------------|  
|**0**|Não é segura. Chamadas feitas ao API SOAP do Reporting Services não exigem uma conexão segura.|  
|Maior que **0**|Segura. Todas as chamadas feitas ao API SOAP do Reporting Services exigem uma conexão segura.|  
  
 Você pode usar o método <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A> do serviço Web para retornar uma lista de métodos do serviço Web que exigem uma conexão segura de acordo com a configuração atual do servidor de relatório. Em um cenário SSL, avalie a lista de métodos retornados por <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A> e altere o nome do esquema da URI do serviço Web para "https" ou "http", dependendo do método chamado.  
  
## <a name="see-also"></a>Consulte Também  
 [Criando aplicativos usando o serviço Web e o .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Serviço Web do Servidor de Relatório](../../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
