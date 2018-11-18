---
title: Definindo o namespace de item para o método GetProperties | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service-net-framework-soap-headers
ms.topic: reference
helpviewer_keywords:
- item properties [Reporting Services]
- ItemNamespaceHeader SOAP header
- GetProperties method
ms.assetid: b0a08639-3101-40a2-abe2-3a41753826d1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 86d01110e1d1e0146e34a3d2f5c3afe2434f48bd
ms.sourcegitcommit: 9ece10c2970a4f0812647149d3de2c6b75713e14
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51812839"
---
# <a name="setting-the-item-namespace-for-the-getproperties-method"></a>Definindo o namespace Item para o método GetProperties
  Você pode usar o cabeçalho SOAP <xref:ReportService2010.ItemNamespaceHeader> no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para recuperar propriedades de item baseadas em dois identificadores de item diferentes: o caminho completo do item ou a ID do item.  
  
 Quando você faz uma chamada ao método <xref:ReportService2010.ReportingService2010.GetProperties%2A> normalmente passa como argumento o caminho completo do item para o qual deseja recuperar propriedades. Ao usar <xref:ReportService2010.ItemNamespaceHeader>, você pode definir o cabeçalho SOAP para a sua chamada de método para permitir o uso de <xref:ReportService2010.ReportingService2010.GetProperties%2A> ao passar a ID do item como um identificador.  
  
 O exemplo de código a seguir recupera os valores para propriedades de item baseadas na ID do item.  
  
> [!NOTE]  
>  Por padrão, você não precisará definir um valor para <xref:ReportService2010.ItemNamespaceHeader> se passar para o método <xref:ReportService2010.ReportingService2010.GetProperties%2A> o caminho completo como o identificador de item.  
  
```vb  
Imports System  
Imports System.Collections  
  
Class Sample  
   Sub Main()  
      Dim rs As New ReportingService2010()  
      rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
      rs.Url = "https://<Server Name>/reportserver/ReportService2010.asmx"  
  
      Dim items() As CatalogItem  
  
      Try  
         ' Need the ID property of items. Normally, you would already have   
         ' this stored somewhere.  
         items = rs.ListChildren("/AdventureWorks Sample Reports", False)  
  
         ' Set the item namespace header to be GUID-based  
         rs.ItemNamespaceHeaderValue = New ItemNamespaceHeader()  
         rs.ItemNamespaceHeaderValue.ItemNamespace = ItemNamespaceEnum.GUIDBased  
  
         ' Call GetProperties with item ID.  
         If Not (items Is Nothing) Then  
            Dim item As CatalogItem  
            For Each item In  items  
               Dim properties As [Property]() = rs.GetProperties(item.ID, Nothing)  
               Dim property As [Property]  
               For Each property In  properties  
                  Console.WriteLine(([property].Name + ": " + [property].Value))  
               Next property  
               Console.WriteLine()  
            Next item  
         End If  
  
      Catch e As Exception  
         Console.WriteLine((e.Message + ": " + e.StackTrace))  
      End Try  
   End Sub 'Main  
End Class 'Sample  
```  
  
```csharp  
using System;  
using System.Collections;  
  
class Sample  
{  
   static void Main()  
   {  
   ReportingService2010 rs = new ReportingService2010();  
      rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
      rs.Url = "https://<Server Name>/reportserver/ReportService2010.asmx";  
  
      CatalogItem[] items;  
  
      try  
      {  
         // Need the ID property of items. Normally, you would already have   
         // this stored somewhere.  
         items = rs.ListChildren("/AdventureWorks Sample Reports", false);  
  
         // Set the item namespace header to be GUID-based  
         rs.ItemNamespaceHeaderValue = new ItemNamespaceHeader();  
         rs.ItemNamespaceHeaderValue.ItemNamespace = ItemNamespaceEnum.GUIDBased;  
  
         // Call GetProperties with item ID.  
         if (items != null)  
         {  
            foreach( CatalogItem item in items)  
            {  
               Property[] properties = rs.GetProperties(item.ID, null);  
               foreach (Property property in properties)  
               {  
                  Console.WriteLine(property.Name + ": " + property.Value);  
               }  
               Console.WriteLine();  
            }  
         }  
      }  
  
      catch (Exception e)  
      {  
         Console.WriteLine(e.Message);  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência técnica &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)   
 [Usar cabeçalhos SOAP do Reporting Services](../../reporting-services/report-server-web-service-net-framework-soap-headers/using-reporting-services-soap-headers.md)  
  
  
