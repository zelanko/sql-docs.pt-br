---
title: "Chamando métodos do serviço Web | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- Web service [Reporting Services], SOAP
- Web service [Reporting Services], calls
- calling Web service
- Report Server Web service, SOAP
- XML Web service [Reporting Services], calls
- Report Server Web service, calls
- XML Web service [Reporting Services], SOAP
- SOAP [Reporting Services], calls
ms.assetid: f6f0c6e3-8bb5-4c44-9d19-1872edc72746
caps.latest.revision: 38
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6e55323aade7a87123817b4a53c3ee03d5e336d5
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="calling-web-service-methods"></a>Chamando métodos do serviço Web
  Quando você usa um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] classe de proxy para chamar operações de serviço da Web, você pode fazer isso usando os métodos dessa classe. Esses métodos respondem como qualquer outro método de uma classe da biblioteca de classes [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Todos os métodos do serviço Web têm acesso público e exigem que você forneça o número e tipos de argumentos adequados. Depois de criar uma instância da classe de proxy em seu projeto, você poderá chamar os métodos para realizar operações de relatório por meio do servidor de relatório. O código c# a seguir ilustra o uso do <xref:ReportService2010.ReportingService2010.ListChildren%2A> método o <xref:ReportService2010.ReportingService2010> classe proxy. Esse código é usado para realizar uma chamada recursiva para o serviço Web que retorna uma matriz dos objetos <xref:ReportService2010.CatalogItem> que contém uma lista de todos os itens do banco de dados do servidor de relatório:  
  
```vb  
Dim rs As New ReportingService2010()  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
Dim items As CatalogItem() = rs.ListChildren("/", True)  
```  
  
```csharp  
ReportingService2010 rs = new ReportingService2010();  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
CatalogItem[] items = rs.ListChildren("/", true);  
```  
  
## <a name="see-also"></a>Consulte também  
 [Criando aplicativos que usam o serviço Web e o .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Serviço Web servidor de relatório](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Referência técnica &#40; SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
