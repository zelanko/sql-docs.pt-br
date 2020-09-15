---
description: Definindo o namespace Item para o método GetProperties
title: Definindo o namespace de item para o método GetProperties | Microsoft Docs
Description: Saiba como recuperar propriedades com base no caminho ou na ID de um item usando o método GetProperties e o cabeçalho SOAP ItemNamespaceHeader.
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
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: fc0d61726a885b6a2422a4fe048121e65b8642f8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423240"
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
 [Usando cabeçalhos SOAP do Reporting Services](../../reporting-services/report-server-web-service-net-framework-soap-headers/using-reporting-services-soap-headers.md)  
  
  
