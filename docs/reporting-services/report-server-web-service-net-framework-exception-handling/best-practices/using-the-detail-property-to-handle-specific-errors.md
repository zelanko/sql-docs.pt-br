---
title: Usando a propriedade Detail para tratar erros específicos | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service-net-framework-exception-handling
ms.topic: reference
helpviewer_keywords:
- exceptions [Reporting Services], Detail property
- Detail property
- InnerText property
ms.assetid: 4392633d-b46b-41e6-bc12-efb64e166704
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8543ec4cebe940523dad26044ee93f697d62c6bc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62992405"
---
# <a name="using-the-detail-property-to-handle-specific-errors"></a>Usando a propriedade Detail para manipular erros específicos
  Para classificar ainda mais as exceções, o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] retorna informações de erro adicionais na propriedade **InnerText** dos elementos filho da propriedade **Detail** da exceção SOAP. Como a propriedade **Detail** é um objeto **XmlNode**, você pode acessar o texto interno do elemento filho **Message** usando o código a seguir.  
  
 Para obter uma lista de todos os elementos filho disponíveis contidos na propriedade **Detail**, consulte [Propriedade Detail](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md). Para obter mais informações, consulte “Propriedade Detail” na documentação do SDK do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
```vb  
Try  
' Code for accessing the report server  
Catch ex As SoapException  
   ' The exception is a SOAP exception, so use  
   ' the Detail property's Message element.  
   Console.WriteLine(ex.Detail("Message").InnerXml)  
End Try  
```  
  
```csharp  
try  
{  
   // Code for accessing the report server  
}  
catch (SoapException ex)  
{  
   // The exception is a SOAP exception, so use  
   // the Detail property's Message element.  
   Console.WriteLine(ex.Detail["Message"].InnerXml);  
}  
```  
  
```vb  
Try  
' Code for accessing the report server  
Catch ex As SoapException  
   If ex.Detail("ErrorCode").InnerXml = "rsInvalidItemName" Then  
   End If ' Perform an action based on the specific error code  
End Try  
```  
  
```csharp  
try  
{  
   // Code for accessing the report server  
}  
catch (SoapException ex)  
{  
   if (ex.Detail["ErrorCode"].InnerXml == "rsInvalidItemName")  
   {  
      // Perform an action based on the specific error code  
   }  
}  
```  
  
 A linha de código a seguir grava o código de erro específico retornado na Exceção SOAP para o console. Você também pode avaliar o código de erro e executar ações específicas.  
  
```vb  
Console.WriteLine(ex.Detail("ErrorCode").InnerXml)  
```  
  
```csharp  
Console.WriteLine(ex.Detail["ErrorCode"].InnerXml);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Introdução ao tratamento de exceção no Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Classe SoapException do Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)   
 [Tabela de erros de SoapException](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md)  
  
  
