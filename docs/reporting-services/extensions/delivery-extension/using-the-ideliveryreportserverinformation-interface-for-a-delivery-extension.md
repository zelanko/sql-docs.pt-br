---
title: "Usando a Interface IDeliveryReportServerInformation para uma extensão de entrega | Microsoft Docs"
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
- IDeliveryReportServerInformation interface
- delivery extensions [Reporting Services], retrieving report server information
ms.assetid: adbce647-18f3-470c-8114-42f8bcc95dc2
caps.latest.revision: 34
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: caebc70ede4475cef103d0d76598ea3125231252
ms.contentlocale: pt-br
ms.lasthandoff: 08/12/2017

---
# <a name="using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension"></a>Usando a interface IDeliveryReportServerInformation para uma extensão de entrega
  A interface de <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation> exibe várias propriedades que você poderá usar para recuperar informações sobre um servidor de relatório. Você pode usar essas informações para entregar notificações e relatórios. Ao implementar a sua classe de extensão de entrega, você implementa a propriedade <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ReportServerInformation%2A> como exigido pela interface de <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension>. A propriedade de <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ReportServerInformation%2A> retorna um objeto que implementa a interface de <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation>. A partir desse objeto é possível obter uma lista de extensões de renderização atualmente suportadas pelo servidor de relatório.  
  
 O seguinte **para** loop pode ser usado para armazenar uma lista de extensões de renderização disponíveis atualmente no servidor de relatório em um **ArrayList** objeto.  
  
```vb  
Dim renderFormats As New ArrayList()  
Dim e As Microsoft.ReportingServices.Interfaces.Extension  
For Each e In  ReportServerInformation.RenderingExtension  
   If e.Visible Then  
      renderFormats.Add(e.Name)  
   End If  
Next e  
```  
  
```csharp  
ArrayList renderFormats = new ArrayList();  
foreach (Microsoft.ReportingServices.Interfaces.Extension e in ReportServerInformation.RenderingExtension)  
{   
   if (e.Visible)  
   {  
      renderFormats.Add(e.Name);  
   }  
}  
```  
  
 Para obter mais informações sobre o <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation> interface, consulte [usando a IDeliveryReportServerInformation Interface para uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension.md).  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.ReportingServices.Interfaces>   
 [Implementando uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

