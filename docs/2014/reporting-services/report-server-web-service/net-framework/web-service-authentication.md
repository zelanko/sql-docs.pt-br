---
title: Autenticação do serviço Web | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], authentication
- XML Web service [Reporting Services], authentication
- Report Server Web service, authentication
ms.assetid: 852b4947-a090-4e54-8555-5a503945ceab
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: aaccc593ea7e4baece132b759ca920018cdbe4b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62518717"
---
# <a name="web-service-authentication"></a>Autenticação de serviço Web
  Você pode usar a Autenticação de Windows ou a autenticação Básica para autenticar as chamadas feitas ao serviço Web Servidor de Relatório. Qualquer cliente que faz solicitações SOAP ao servidor de relatório deve implementar a parte cliente de um dos protocolos de autenticação suportados. Se você estiver usando o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], poderá usar as classes http de código gerenciado para implementar a autenticação. O uso dessas APIs facilita o envio de informações de autenticação junto comas solicitações SOAP.  
  
 Se você não tiver as credenciais apropriados antes de fazer uma chamada ao serviço Web Servidor de Relatório, a chamada falhará. Em tempo de execução, passe as credenciais para o serviço Web definindo a propriedade **Credentials** do objeto do lado do cliente que representa o serviço Web antes de chamar seus métodos.  
  
 As seções a seguir contêm código de exemplo que envia credenciais usando o [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
## <a name="windows-authentication"></a>Autenticação do Windows  
 O código a seguir transmite credenciais do Windows ao serviço Web.  
  
```vb  
Dim rs As New ReportingService()  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
```  
  
```csharp  
ReportingService rs = new ReportingService();  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
```  
  
## <a name="basic-authentication"></a>Autenticação básica  
 O código a seguir transmite credenciais Básicas ao serviço Web.  
  
```vb  
Dim rs As New ReportingService()  
rs.Credentials = New System.Net.NetworkCredential("username", "password", "domain")  
```  
  
```csharp  
ReportingService service = new ReportingService();  
service.Credentials = new System.Net.NetworkCredential("username", "password", "domain");  
```  
  
 As credenciais devem ser definidas antes de você chamar qualquer um dos métodos do serviço Web Servidor de Relatório. Se você não definir as credenciais, receberá o código de erro HTTP 401 Erro: acesso negado. Autentique o serviço antes de usá-lo, mas depois de definir as credenciais; não será preciso defini-las novamente, desde que você continue usando a mesma variável de serviço (como *rs*).  
  
## <a name="custom-authentication"></a>Autenticação personalizada  
 O [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] inclui uma API de programação que oferece aos desenvolvedores a oportunidade de criar e de desenvolver extensões de autenticação personalizadas, conhecido como extensões de segurança. Para obter mais informações, consulte [Implementing a Security Extension](../../extensions/security-extension/implementing-a-security-extension.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criando aplicativos usando o serviço Web e o .NET Framework](building-applications-using-the-web-service-and-the-net-framework.md)   
 [Serviço Web do Servidor de Relatório](../report-server-web-service.md)  
  
  
