---
title: Implementando uma extensão de entrega | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- delivery [Reporting Services]
- custom delivery extensions [Reporting Services]
- extensions [Reporting Services], delivery
- delivery extensions [Reporting Services]
ms.assetid: 600cd229-efcd-480e-8c95-3c3c39ff4e7a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cae33496e4dddcaf2d14ba2d87f0d4013795e58f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63165135"
---
# <a name="implementing-a-delivery-extension"></a>Implementando uma extensão de entrega
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] permite que os usuários criem e publiquem relatórios que, depois de criados e publicados, possam ser entregues a vários locais. Além disso, o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] inclui várias extensões de entrega e uma API de entrega que permite que os desenvolvedores criem extensões de entrega adicionais para estender ainda mais a funcionalidade de entrega do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 Para obter uma implementação de exemplo de uma extensão de entrega, consulte [Amostras de produto do SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Visão geral das extensões de entrega] entrega-extensões-overview.md)  
 Apresenta como escrever uma extensão de entrega para o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 [Preparando para implementar uma entrega de extensão](preparing-to-implement-a-delivery-extension.md)  
 Descreve as interfaces e as classes disponíveis durante a implementação de uma extensão de entrega do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], além dos problemas a serem considerados antes da implementação.  
  
 [Criando uma biblioteca de extensões de entrega](creating-a-delivery-extension-library.md)  
 Descreve a atribuição de um namespace para a extensão de entrega do seu [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e a compilação da sua extensão de entrega em uma DLL de biblioteca.  
  
 [Implementando a interface IDeliveryExtension para uma extensão de entrega](implementing-the-ideliveryextension-interface-for-a-delivery-extension.md)  
 Descreve os atributos de uma extensão de entrega e como implementar a sua própria classe de extensão de entrega.  
  
 [Usando uma classe de notificação classe para uma extensão de entrega](using-a-notification-class-for-a-delivery-extension.md)  
 Descreve os atributos de uma classe **Notification** e como usá-la na implementação de extensão de entrega.  
  
 [Usando a classe Setting para uma extensão de entrega](using-the-setting-class-for-a-delivery-extension.md)  
 Descreve os atributos de uma classe **Setting** e como usá-la na implementação de extensão de entrega.  
  
 [Usando a interface IDeliveryReportServerInformation para uma extensão de entrega](using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension.md)  
 Descreve os atributos de uma interface **IDeliveryReportServerInformation** e como usá-la na implementação de extensão de entrega.  
  
 [Usando a classe Report para uma extensão de entrega](using-the-report-class-for-a-delivery-extension.md)  
 Descreve os atributos de uma classe **Report** e como usá-la na implementação de extensão de entrega.  
  
 [Usar a classe RenderedOutputFile para uma extensão de entrega](using-the-renderedoutputfile-class-for-a-delivery-extension.md)  
 Descreve os atributos de uma classe **RenderedOutputFile** e como usá-la na implementação de extensão de entrega.  
  
 [Implementando a interface ISubscriptionBaseUIUserControl para uma extensão de entrega](implementing-the-isubscriptionbaseuiusercontrol-interface.md)  
 Descreve os atributos de um controle de usuário de extensão de entrega e como implementar a sua própria interface do usuário para uma assinatura.  
  
 [Implantando uma extensão de entrega](deploying-a-delivery-extension.md)  
 Descreve como implantar a sua extensão de entrega.  
  
 [Depurando o código de extensão de entrega](debugging-delivery-extension-code.md)  
 Descreve como depurar código em sua extensão de entrega.  
  
 [Removendo uma extensão de entrega](removing-a-delivery-extension.md)  
 Descreve como remover uma extensão de entrega de um servidor de relatório.  
  
## <a name="see-also"></a>Consulte Também  
 [Extensões do Reporting Services](../reporting-services-extensions.md)   
 [Biblioteca de extensões do Reporting Services](../reporting-services-extension-library.md)  
  
  
