---
title: "Usando métodos do serviço Web segura | Microsoft Docs"
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
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- SOAP [Reporting Services], secure connections
- Web service [Reporting Services], SOAP
- Report Server Web service, SOAP
- XML Web service [Reporting Services], SOAP
ms.assetid: 87329299-c2ea-4517-9148-d855726768a9
caps.latest.revision: 36
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 802070f070222fba573b52bf1f53b2c6eb8ba8b6
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="using-secure-web-service-methods"></a>Usando métodos seguros do serviço Web
  Certos métodos do serviço Web Servidor de Relatório podem exigir uma conexão segura quando chamados. Os métodos que exigem uma conexão segura são determinados pelo **SecureConnectionLevel** no arquivo rsreportserver. config. O valor da configuração é um valor inteiro com um intervalo válido 0 e superior. A tabela a seguir descreve esses valores.  
  
|Nível|Description|  
|-----------|-----------------|  
|**0**|Não é segura. Chamadas feitas ao API SOAP do Reporting Services não exigem uma conexão segura.|  
|Maior **0**|Segura. Todas as chamadas feitas ao API SOAP do Reporting Services exigem uma conexão segura.|  
  
 Você pode usar o método <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A> do serviço Web para retornar uma lista de métodos do serviço Web que exigem uma conexão segura de acordo com a configuração atual do servidor de relatório. Em um cenário SSL, avalie a lista de métodos retornados por <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A> e altere o nome do esquema da URI do serviço Web para "https" ou "http", dependendo do método chamado.  
  
## <a name="see-also"></a>Consulte também  
 [Criando aplicativos que usam o serviço Web e o .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Serviço Web servidor de relatório](../../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
