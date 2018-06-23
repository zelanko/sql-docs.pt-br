---
title: Definindo o namespace de item para o método GetProperties | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- item properties [Reporting Services]
- ItemNamespaceHeader SOAP header
- GetProperties method
ms.assetid: b0a08639-3101-40a2-abe2-3a41753826d1
caps.latest.revision: 37
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9cfe424d0cc39cb72c5d08215131a4cf540f2ed2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121639"
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
      rs.Url = "http://<Server Name>/reportserver/ReportService2010.asmx"  
  
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
      rs.Url = "http://<Server Name>/reportserver/ReportService2010.asmx";  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência técnica &#40;SSRS&#41;](../technical-reference-ssrs.md)   
 [Usar cabeçalhos SOAP do Reporting Services](using-reporting-services-soap-headers.md)  
  
  