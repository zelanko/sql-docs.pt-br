---
title: Implementando a Interface ISubscriptionBaseUIUserControl | Microsoft Docs
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
- user controls [Reporting Services]
- ISubscriptionBaseUIUserControl interface
- delivery extensions [Reporting Services], user controls
ms.assetid: a1e9122c-aa0b-45de-b536-4f1202875ab1
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 4e76edaa727df1694a5903e1cc9870c20581c9a0
ms.contentlocale: pt-br
ms.lasthandoff: 08/12/2017

---
# <a name="implementing-the-isubscriptionbaseuiusercontrol-interface"></a>Implementando a Interface ISubscriptionBaseUIUserControl
  As extensões de entrega do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] podem conter uma implementação de uma interface do usuário de assinatura para a obtenção de informações específicas da extensão no Gerenciador de Relatórios. A interface do usuário é invocada quando um usuário cria uma assinatura nova ou modifica uma existente. Quando uma assinatura nova é criada, a interface do usuário exibe valores padrão adequados e permite que os usuários interajam com o provedor de entrega. Quando uma assinatura é modificada, a interface do usuário é preenchida previamente com as informações da assinatura atual.  
  
 As extensões de entrega oferecem a interface do usuário de assinatura como um controle de usuário do ASP.NET. O servidor de relatório incorpora o controle de usuário definido pela extensão de entrega ao exibir a interface do usuário de assinatura. A interface base que oferece métodos abstratos habilitando esta funcionalidade é a interface <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl>. Esta interface garante que as operações comuns, como a validação de valores de entrada, sejam executadas corretamente. Adicionalmente, o controle de usuário base oferece um conjunto de propriedades padrão usadas pelo servidor de relatório para consistência entre assinaturas. Essas propriedades são obrigatórias para extensões de entrega integradas ao Gerenciador de Relatórios.  
  
 Você pode implementar a interface <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> em um provedor de entrega para criar uma interface do usuário de assinatura para o Gerenciador de Relatórios. A interface <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> oferece infraestrutura para permitir que os usuários insiram valores para configurações de assinatura, para o processamento das configurações necessárias à extensão de entrega e para a validação das configurações.  
  
> [!NOTE]  
>  Você não é obrigado a implementar a interface <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> como parte de sua extensão de entrega. As assinaturas que usam sua extensão de entrega podem sempre ser criadas pelos métodos da API SOAP <xref:ReportService2010.ReportingService2010.CreateSubscription%2A> e <xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A>. Para obter mais informações sobre os recursos da API SOAP para o gerenciamento de assinatura e entrega, consulte [Subscription and Delivery Methods](../../../reporting-services/report-server-web-service/methods/subscription-and-delivery-methods.md).  
  
 A interface <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> estende <xref:Microsoft.ReportingServices.Interfaces.IExtension>. O controle de usuário implementa <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> também deve herdar de **WebControl**. Para obter mais informações sobre o **WebControl** de classe, consulte o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] guia do desenvolvedor.  
  
 Para obter um exemplo de como usar o <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> interface, consulte [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Consulte também  
 [Implementando uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
