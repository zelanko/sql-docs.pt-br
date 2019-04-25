---
title: Definindo a propriedade Url do serviço Web | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Url property
- Report Server Web service, proxies
- proxies [Reporting Services]
- XML Web service [Reporting Services], proxies
- Web service [Reporting Services], proxies
- Web references [Reporting Services]
ms.assetid: 4eac4e40-dafb-4403-acde-13df317c8ec8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4036e38a0d0eb5e76934fa119b3bcc37342062a7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62520282"
---
# <a name="setting-the-url-property-of-the-web-service"></a>Definindo a propriedade Url do serviço Web
  A qualquer momento em seus aplicativos do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], você pode modificar a URL base do serviço Web Servidor de Relatórios para a qual o aplicativo foi direcionado no momento. Para fazer isso, basta definir a propriedade **Url** do objeto de serviço. Por exemplo:  
  
```vb  
Dim rs As New ReportingService2010()  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
rs.Url = "http://<Server Name>/reportserver/ReportService2010.asmx"  
```  
  
```csharp  
ReportingService2010 service = new ReportingService2010();  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
rs.Url = "http://<Server Name>/reportserver/ReportService2010.asmx";  
```  
  
 O exemplo a seguir recupera uma definição de relatório de um servidor de relatório e usa essa definição para criar um relatório idêntico em um servidor de relatório diferente:  
  
```vb  
Imports System  
Imports System.Web.Services.Protocols  
  
Class Sample  
   Public Shared Sub Main()  
      Dim rs As New ReportingService2010()  
      rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
      ' Set the base Web service URL of the source server  
      rs.Url = "http://<Server Name>/reportserver/ReportService2010.asmx"  
  
      Dim reportName As String = "/SampleReports/Company Sales"  
      Dim reportDefinition As Byte() = Nothing  
  
      Try  
         ' Get the report definition of a report on a source server  
         reportDefinition = rs.GetItemDefinition(reportName)  
         ' Set the base Web service URL of the destination server  
         rs.Url = "http://<Server Name>/reportserver/ReportService2010.asmx"  
         ' Create a copy of the report on the destination server  
         Dim warnings As Warning() = {}  
         rs.CreateCatalogItem("Report", "Company Sales Copy", "/", False, reportDefinition, Nothing, warnings)        
      Catch e As SoapException  
         Console.WriteLine(e.Detail.InnerXml.ToString())  
      End Try  
   End Sub 'Main  
End Class 'Sample  
```  
  
```csharp  
using System;  
using System.Web.Services.Protocols;  
  
class Sample  
{  
   public static void Main()  
   {  
      ReportingService2010 rs = new ReportingService2010();  
      rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
      // Set the base Web service URL of the source server  
      rs.Url = "http://<Server Name>/reportserver/reportservice2010.asmx";  
  
      string reportName = "/SampleReports/Company Sales";  
      byte[] reportDefinition = null;  
  
      try  
      {  
         reportDefinition = rs.GetItemDefinition(reportName);  
         // Set the base Web service URL of the destination server  
         rs.Url = "http://<Server Name>/reportserver/ReportService2010.asmx";  
         // Create a copy of the report on the destination server  
         Warning[] warnings = {};  
         rs.CreateCatalogItem("Report", "Company Sales Copy", "/", false, reportDefinition, null, out warnings);  
      }  
  
      catch (SoapException e)  
      {  
         Console.WriteLine(e.Detail.InnerXml.ToString());   
      }  
   }  
}  
```  
  
 Para obter mais informações sobre como criar o proxy inicial de serviço Web, consulte [Criar o proxy de serviço Web](creating-the-web-service-proxy.md).  
  
## <a name="see-also"></a>Consulte também  
 <xref:ReportService2010.ReportingService2010.CreateCatalogItem%2A>   
 <xref:ReportService2010.ReportingService2010.GetItemDefinition%2A>   
 [Criando aplicativos usando o serviço Web e o .NET Framework](building-applications-using-the-web-service-and-the-net-framework.md)   
 [Serviço Web do Servidor de Relatório](../report-server-web-service.md)  
  
  
