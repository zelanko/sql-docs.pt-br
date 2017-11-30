---
title: "Visão geral das extensões de entrega | Microsoft Docs"
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
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- subscriptions [Reporting Services], delivery extensions
- delivery extensions [Reporting Services], about extensions
ms.assetid: a30600a9-bbed-4519-9426-3470ff2982e7
caps.latest.revision: "37"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 07f9b2fcb366ecf1b433917852462766d6cd0951
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="delivery-extensions-overview"></a>Visão geral de extensões de entrega
  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] permite que os usuários criem e publiquem relatórios que, uma vez criados e publicados, podem ser entregues em vários locais. Além disso, o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] inclui várias extensões de entrega e uma API de entrega que permite que os desenvolvedores criem extensões de entrega adicionais para estender ainda mais a funcionalidade de entrega do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 A tabela a seguir lista as extensões de entrega incluídas no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
|Extensão da entrega|Description|  
|------------------------|-----------------|  
|Email do servidor de relatório|Usa um servidor SMTP para enviar relatórios de email a usuários individuais ou a grupos.|  
|Compartilhamento de arquivos do servidor de relatórios|Usado para distribuir relatórios em sua organização para o compartilhamentos de arquivos de rede. Oferece a capacidade de copiar um relatório automaticamente para um compartilhamento de arquivo em uma agenda designada.|  
  
 ![Arquitetura de extensão de entrega do Reporting Services](../../../reporting-services/extensions/delivery-extension/media/bk-reportservicedelivery.gif "Arquitetura de extensão de entrega do Reporting Services")  
Arquitetura da extensão de entrega do Reporting Services  
  
 As extensões de entrega são emparelhadas com as assinaturas. Durante a criação de uma assinatura, um usuário pode escolher uma das extensões de entrega disponíveis para determinar como o relatório será entregue. No [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], as assinaturas estão localizadas no banco de dados do servidor de relatório. Quando ocorre um evento, o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] corresponde o evento às assinaturas contidas no banco de dados do servidor de relatório. Para cada assinatura ligada ao evento, o servidor de relatório criará uma notificação. Para assinaturas controladas por dados, uma notificação será criada para cada destinatário. Depois que a notificação for criada, o servidor de relatório invocará uma determinada extensão de entrega e passará valores para as configurações de extensão especificadas na notificação. A extensão de entrega envia a notificação ao usuário como especificado pela extensão de entrega selecionada.  
  
 As extensões de entrega implementam API de extensão de entrega do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Ao dar suporte à API de extensão de entrega do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], as extensões de entrega poderão receber notificações do servidor de relatório e fornecer o status da notificação.  
  
 O servidor de relatório não gerencia destinos de entrega para notificações e relatórios. A coleta de informações de destino é realizada pelo código escrito em sua extensão de entrega.  
  
## <a name="subscriptions-and-delivery-extensions"></a>Assinaturas e extensões de entrega  
 Os aplicativos cliente criam assinaturas que usam extensões de entrega usando dois métodos do serviço Web Servidor de Relatório: <xref:ReportService2010.ReportingService2010.CreateSubscription%2A> e <xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A>. Para modificar assinaturas que já existem, serão usados os métodos <xref:ReportService2010.ReportingService2010.SetSubscriptionProperties%2A> e <xref:ReportService2010.ReportingService2010.SetDataDrivenSubscriptionProperties%2A>. Durante a criação de uma assinatura, o usuário também seleciona uma extensão de entrega para a assinatura e digita valores para as configurações de extensão exigidas. Quando um usuário salvar uma assinatura, ela será armazenada no banco de dados do servidor de relatório. As assinatura criam notificações baseadas em uma agenda ou em um evento. Quando uma entrega é iniciada, primeiro a extensão de entrega selecionada carrega quaisquer dados de configuração a partir do arquivo de configuração. Em seguida, são recuperadas as configurações de extensão da assinatura e são definidos valores. Por fim, o método <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> é chamado e a notificação é enviada.  
  
## <a name="developer-requirements"></a>Requisitos de desenvolvedor  
 Desenvolver uma extensão de entrega do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] exige que você tenha:  
  
-   Um computador de implantação com um servidor de relatório instalado.  
  
-   Um computador de desenvolvimento com o [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)] ou o SDK (Software Development Kit) do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] instalado.  
  
-   Uma compreensão detalhada dos recursos e das capacidades do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], especificamente de assinatura e de entrega.  
  
-   Uma compreensão detalhada do [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] e de controles da Web se estiver planejando implementar a sua própria interface do usuário de assinatura para o Gerenciador de Relatórios.  
  
-   Experiência de desenvolvimento em uma linguagem do [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], como [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# ou [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] .NET.  
  
## <a name="see-also"></a>Consulte também  
 [Implementando uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
