---
title: Implementando a Interface ISubscriptionBaseUIUserControl para uma extensão de entrega | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- user controls [Reporting Services]
- ISubscriptionBaseUIUserControl interface
- delivery extensions [Reporting Services], user controls
ms.assetid: a1e9122c-aa0b-45de-b536-4f1202875ab1
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 7d138662d8b72a99d84d9a224b97bed6be58c675
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56029887"
---
# <a name="implementing-the-isubscriptionbaseuiusercontrol-interface-for-a-delivery-extension"></a>Implementando a interface ISubscriptionBaseUIUserControl para uma extensão de entrega
  As extensões de entrega do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] podem conter uma implementação de uma interface do usuário de assinatura para a obtenção de informações específicas da extensão no Gerenciador de Relatórios. A interface do usuário é invocada quando um usuário cria uma assinatura nova ou modifica uma existente. Quando uma assinatura nova é criada, a interface do usuário exibe valores padrão adequados e permite que os usuários interajam com o provedor de entrega. Quando uma assinatura é modificada, a interface do usuário é preenchida previamente com as informações da assinatura atual.  
  
 As extensões de entrega oferecem a interface do usuário de assinatura como um controle de usuário do ASP.NET. O servidor de relatório incorpora o controle de usuário definido pela extensão de entrega ao exibir a interface do usuário de assinatura. A interface base que oferece métodos abstratos habilitando esta funcionalidade é a interface <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl>. Esta interface garante que as operações comuns, como a validação de valores de entrada, sejam executadas corretamente. Adicionalmente, o controle de usuário base oferece um conjunto de propriedades padrão usadas pelo servidor de relatório para consistência entre assinaturas. Essas propriedades são obrigatórias para extensões de entrega integradas ao Gerenciador de Relatórios.  
  
 Você pode implementar a interface <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> em um provedor de entrega para criar uma interface do usuário de assinatura para o Gerenciador de Relatórios. A interface <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> oferece infraestrutura para permitir que os usuários insiram valores para configurações de assinatura, para o processamento das configurações necessárias à extensão de entrega e para a validação das configurações.  
  
> [!NOTE]  
>  Você não é obrigado a implementar a interface <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> como parte de sua extensão de entrega. As assinaturas que usam sua extensão de entrega podem sempre ser criadas pelos métodos da API SOAP <xref:ReportService2010.ReportingService2010.CreateSubscription%2A> e <xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A>. Para obter mais informações sobre os recursos da API SOAP para o gerenciamento de assinaturas e para entrega, consulte [Métodos de assinatura e de entrega](../../report-server-web-service/methods/subscription-and-delivery-methods.md).  
  
 A interface <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> estende <xref:Microsoft.ReportingServices.Interfaces.IExtension>. O controle de usuário que implementa <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> também deve herdar de **System.Web.UI.WebControls.WebControl**. Para obter mais informações sobre a classe **WebControl**, consulte o Guia do Desenvolvedor do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
 Para obter um exemplo de como usar a interface <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl>, consulte [Amostras de produto do SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Consulte também  
 [Implementando uma extensão de entrega](implementing-a-delivery-extension.md)   
 [Biblioteca de extensões do Reporting Services](../reporting-services-extension-library.md)  
  
  
