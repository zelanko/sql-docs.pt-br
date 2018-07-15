---
title: Usando uma classe de notificação para uma extensão de entrega | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], notifications
- notifications [Reporting Services]
- retry queues
- Nofication class
ms.assetid: 549c40c4-d33d-46c2-9d6a-7bbb671ac67a
caps.latest.revision: 32
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: cf6f9e23cfd4168c2b2b15a6011caf7f7e431b5f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37272412"
---
# <a name="using-a-notification-class-for-a-delivery-extension"></a>Usando uma classe de notificação classe para uma extensão de entrega
  A classe <xref:Microsoft.ReportingServices.Interfaces.Notification> classe está localizada no namespace <xref:Microsoft.ReportingServices.Interfaces> e representa informações de assinatura que extensões de entrega usam para entregar relatórios. A classe <xref:Microsoft.ReportingServices.Interfaces.Notification> oferece algumas propriedades que podem ser usadas para renderizar os relatórios para entrega, determinar o status da notificação e definir dados de usuário.  
  
 ![Processo de notificação de relatório](../../media/bk-ext-03.gif "Processo de notificação de relatório")  
A notificação é o objeto central de qualquer entrega  
  
 Quando um evento dispara que está associado a uma assinatura que usa a sua extensão de entrega personalizada, uma notificação com um objeto <xref:Microsoft.ReportingServices.Interfaces.Report> será criada. O objeto <xref:Microsoft.ReportingServices.Interfaces.Report> encapsula a funcionalidade necessária para a renderização de um determinado relatório para um formato de renderização suportado e contém propriedades específicas do relatório, como a URL para o relatório no servidor e o nome do relatório. Para obter mais informações sobre a classe <xref:Microsoft.ReportingServices.Interfaces.Report>, consulte [Usando a classe Report para uma extensão de entrega](../delivery-extension/using-the-report-class-for-a-delivery-extension.md).  
  
 Você passa o objeto <xref:Microsoft.ReportingServices.Interfaces.Notification> ao método <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> de sua extensão de entrega. Seu método <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> deve conter código específico para processar a notificação e entregar o relatório.  
  
 Para obter um exemplo de como usar a classe <xref:Microsoft.ReportingServices.Interfaces.Notification>, consulte [Amostras de produto do SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="retry-functionality"></a>Funcionalidade de repetição  
 O [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] permite a você criar uma fila de repetição para notificações que não podem ser entregues imediatamente. Depois que o servidor de relatório invoca o método <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> de uma extensão de entrega, a extensão de entrega poderá solicitar que o servidor de relatório tente entregar novamente em um momento determinado. Se isso acontecer, o servidor de relatório coloca a notificação em uma fila interna e tenta entregar novamente após um período de tempo específico. Os administradores podem configurar o número máximo de novas tentativas executadas pelo servidor de relatório e o período entre as novas tentativas na seção da extensão de entrega do arquivo RSReportServer.config usando o elemento XML **MaxNumberOfRetries** e o elemento XML **PeriodBetweenRetries**. As notificações são removidas da fila de repetição se a entrega for bem-sucedida mais tarde ou se o número máximo de novas tentativas for alcançado. Se a entrega falhar depois do número de máximo de novas tentativas, a notificação será descartada.  
  
## <a name="see-also"></a>Consulte também  
 [Implementando uma extensão de entrega](../delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensões do Reporting Services](../reporting-services-extension-library.md)  
  
  
