---
title: "Implementando uma extensão de entrega | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
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
- delivery [Reporting Services]
- custom delivery extensions [Reporting Services]
- extensions [Reporting Services], delivery
- delivery extensions [Reporting Services]
ms.assetid: 600cd229-efcd-480e-8c95-3c3c39ff4e7a
caps.latest.revision: 32
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 5db9bf52437c018bc1dcb40e7fa8a8ce2824fa12
ms.contentlocale: pt-br
ms.lasthandoff: 08/12/2017

---
# <a name="implementing-a-delivery-extension"></a>Implementando uma extensão de entrega
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] permite que os usuários criem e publiquem relatórios que, uma vez criados e publicados, podem ser entregues em vários locais. Além disso, o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] inclui várias extensões de entrega e uma API de entrega que permite que os desenvolvedores criem extensões de entrega adicionais para estender ainda mais a funcionalidade de entrega do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 Para uma implementação de exemplo de uma extensão de entrega, consulte [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Visão geral de extensões de entrega](../../../reporting-services/extensions/delivery-extension/delivery-extensions-overview.md)  
 Apresenta como escrever uma extensão de entrega para o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 [Preparando para implementar uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/preparing-to-implement-a-delivery-extension.md)  
 Descreve as interfaces e as classes disponíveis durante a implementação de uma extensão de entrega do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], além dos problemas a serem considerados antes da implementação.  
  
 [Criando uma biblioteca de extensões de entrega](../../../reporting-services/extensions/delivery-extension/creating-a-delivery-extension-library.md)  
 Descreve a atribuição de um namespace para a extensão de entrega do seu [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e a compilação da sua extensão de entrega em uma DLL de biblioteca.  
  
 [Implementando a Interface IDeliveryExtension para uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/implementing-the-ideliveryextension-interface-for-a-delivery-extension.md)  
 Descreve os atributos de uma extensão de entrega e como implementar a sua própria classe de extensão de entrega.  
  
 [Usar uma classe de notificação para uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/using-a-notification-class-for-a-delivery-extension.md)  
 Descreve os atributos de uma **notificação** classe e como usá-lo em sua implementação de extensão de entrega.  
  
 [Usando a classe de configuração para uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/using-the-setting-class-for-a-delivery-extension.md)  
 Descreve os atributos de uma **configuração** classe e como usá-lo em sua implementação de extensão de entrega.  
  
 [Usando a Interface IDeliveryReportServerInformation para uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension.md)  
 Descreve os atributos de uma **IDeliveryReportServerInformation** interface e como usá-lo em sua implementação de extensão de entrega.  
  
 [Usando a classe de relatório para uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/using-the-report-class-for-a-delivery-extension.md)  
 Descreve os atributos de uma **relatório** classe e como usá-lo em sua implementação de extensão de entrega.  
  
 [Usando a classe RenderedOutputFile para uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/using-the-renderedoutputfile-class-for-a-delivery-extension.md)  
 Descreve os atributos de uma **RenderedOutputFile** classe e como usá-lo em sua implementação de extensão de entrega.  
  
 [Implementando a Interface ISubscriptionBaseUIUserControl para uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/implementing-the-isubscriptionbaseuiusercontrol-interface.md)  
 Descreve os atributos de um controle de usuário de extensão de entrega e como implementar a sua própria interface do usuário para uma assinatura.  
  
 [Implantando uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)  
 Descreve como implantar a sua extensão de entrega.  
  
 [Depurando código de extensão de entrega](../../../reporting-services/extensions/delivery-extension/debugging-delivery-extension-code.md)  
 Descreve como depurar código em sua extensão de entrega.  
  
 [Removendo uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/removing-a-delivery-extension.md)  
 Descreve como remover uma extensão de entrega de um servidor de relatório.  
  
## <a name="see-also"></a>Consulte também  
 [Extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

