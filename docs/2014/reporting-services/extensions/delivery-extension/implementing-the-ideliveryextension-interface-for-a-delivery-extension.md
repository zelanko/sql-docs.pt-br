---
title: Implementando a interface IDeliveryExtension para uma extensão de entrega | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], attributes
- delivery extensions [Reporting Services], class creation
- IDeliveryExtension interface
ms.assetid: ab0344db-510b-403f-8dbf-b9831553765d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a0f9ab0767a09016d4f4bc1158988965bfc13b27
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181428"
---
# <a name="implementing-the-ideliveryextension-interface-for-a-delivery-extension"></a>Implementando a interface IDeliveryExtension para uma extensão de entrega
  A sua classe de extensão de entrega é usada para entregar notificações de relatório a usuários com base no conteúdo das notificações. A classe de extensão de entrega também oferece infraestrutura para validar configurações de usuário passadas à extensão de entrega. Além disso, a sua classe de extensão de entrega deve conter propriedades específicas que os clientes poderão usar para obter informações sobre o nome da extensão, as configurações suportadas pela extensão e os formatos disponíveis para a extensão de entrega.  
  
 ![Processo da interface IDeliveryExtension](../../media/bk-ext-02.gif "Processo da interface IDeliveryExtension")  
A interface IDeliveryExtension permite a validação de dados de usuário como também de clientes para aprender sobre as configurações de entrega exigidas  
  
 Para criar uma classe de extensão de entrega, implemente <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> e <xref:Microsoft.ReportingServices.Interfaces.IExtension>. A interface **IDeliveryExtension** permite que a extensão de entrega forneça notificações de relatório usando o método <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> e valide as configurações de extensão de entrada usando o método <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ValidateUserData%2A>. A interface **IExtension** permite que você habilite a extensão de entrega para implementar um nome de extensão localizado e processe informações de configuração específicas à extensão armazenadas no arquivo de configuração [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Ao implementar **IExtension**, a extensão de entrega conterá a propriedade <xref:Microsoft.ReportingServices.Interfaces.Extension.LocalizedName%2A>. É altamente recomendável que as extensões de entrega do [!INCLUDE[ssRS](../../../includes/ssrs.md)] deem suporte à propriedade **LocalizedName**, para que os usuários encontrem um nome conhecido para a extensão em uma interface do usuário, como Gerenciador de Relatórios.  
  
 A extensão de entrega também deve implementar a propriedade **ExtensionSettings** da interface **IDeliveryExtension**. O servidor de relatório usa o valor retornado pela propriedade <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ExtensionSettings%2A> para avaliar as configurações exigidas por uma extensão de entrega. Os clientes que interagem com extensões de entrega usam o método <xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A> do serviço Web Servidor de Relatório para retornar uma lista de configurações para a extensão de entrega.  
  
 Você também pode usar a sua classe de extensão de entrega para recuperar e processar dados de configuração personalizados armazenados no arquivo RSReportServer.config. Para obter mais informações sobre como processar dados de configuração personalizados, consulte o método <xref:Microsoft.ReportingServices.Interfaces.IExtension.SetConfiguration%2A>.  
  
 Para obter uma implementação da classe **IDeliveryExtension** de exemplo, consulte [Amostras de produto do SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Consulte também  
 [Implementando uma extensão de entrega](../delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensões do Reporting Services](../reporting-services-extension-library.md)  
  
  
