---
title: Usando a classe Setting para uma extensão de entrega | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], settings
- Setting class
ms.assetid: 50746639-da7c-46a5-ac7b-e87dd6b91880
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: e8e2e218eb702f2606293596206e43373a6b6a8f
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56030707"
---
# <a name="using-the-setting-class-for-a-delivery-extension"></a>Usando a classe Setting para uma extensão de entrega
  A classe <xref:Microsoft.ReportingServices.Interfaces.Setting> está localizada no namespace <xref:Microsoft.ReportingServices.Interfaces> e representa as informações sobre configurações de extensão para uma extensão de entrega. A classe <xref:Microsoft.ReportingServices.Interfaces.Setting> fornece infraestrutura para o armazenamento de informações sobre as configurações obrigatórias para que uma extensão de entrega funcione corretamente. Por exemplo, na entrega de E-Mail do Report Server, é necessário que um usuário forneça configurações específicas de entrega de e-mails, como o endereço do destinatário, o endereço do remetente, a linha de assunto do e-mail e mais. Indubitavelmente, os seus provedores de entrega personalizados exigirão que o usuário forneça configurações específicas para que a extensão de entrega entregue notificações e relatórios.  
  
 A classe de <xref:Microsoft.ReportingServices.Interfaces.Setting> é usada na implementação da propriedade de <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ExtensionSettings%2A> da interface de <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension>. A classe de <xref:Microsoft.ReportingServices.Interfaces.Setting> também é usada para o processamento dos dados de configuração da extensão fornecidos por um usuário quando uma assinatura ou notificação é criada.  
  
 Para obter um exemplo de como usar a classe <xref:Microsoft.ReportingServices.Interfaces.Setting>, consulte [Amostras de produto do SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Consulte também  
 [Implementando uma extensão de entrega](implementing-a-delivery-extension.md)   
 [Biblioteca de extensões do Reporting Services](../reporting-services-extension-library.md)  
  
  
