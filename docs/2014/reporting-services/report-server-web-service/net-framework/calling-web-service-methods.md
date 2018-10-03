---
title: Chamando métodos do serviço Web | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
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
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f35fa29bdcaba7a2b6d0af62eebf7e996d41a890
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48167366"
---
# <a name="calling-web-service-methods"></a>Chamando métodos do serviço Web
  Quando você usa uma classe proxy do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] para chamar as operações do serviço Web, você faz isso usando os métodos dessa classe. Esses métodos respondem como qualquer outro método de uma classe da biblioteca de classes [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Todos os métodos do serviço Web têm acesso público e exigem que você forneça o número e tipos de argumentos adequados. Depois de criar uma instância da classe de proxy em seu projeto, você poderá chamar os métodos para realizar operações de relatório por meio do servidor de relatório. O código C# a seguir ilustra o uso do método <xref:ReportService2010.ReportingService2010.ListChildren%2A> da classe proxy <xref:ReportService2010.ReportingService2010>. Esse código é usado para realizar uma chamada recursiva para o serviço Web que retorna uma matriz dos objetos <xref:ReportService2010.CatalogItem> que contém uma lista de todos os itens do banco de dados do servidor de relatório:  
  
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
 [Criando aplicativos usando o serviço Web e o .NET Framework](building-applications-using-the-web-service-and-the-net-framework.md)   
 [Serviço Web do Servidor de Relatório](../report-server-web-service.md)   
 [Referência técnica &#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  
