---
title: "Implementando a Interface IDeliveryExtension para uma extensão de entrega | Microsoft Docs"
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
- delivery extensions [Reporting Services], attributes
- delivery extensions [Reporting Services], class creation
- IDeliveryExtension interface
ms.assetid: ab0344db-510b-403f-8dbf-b9831553765d
caps.latest.revision: 37
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: ac54345b14ba3ff84a755e0ce4e8b1c4e9acab13
ms.contentlocale: pt-br
ms.lasthandoff: 08/12/2017

---
# <a name="implementing-the-ideliveryextension-interface-for-a-delivery-extension"></a>Implementando a interface IDeliveryExtension para uma extensão de entrega
  A sua classe de extensão de entrega é usada para entregar notificações de relatório a usuários com base no conteúdo das notificações. A classe de extensão de entrega também oferece infraestrutura para validar configurações de usuário passadas à extensão de entrega. Além disso, a sua classe de extensão de entrega deve conter propriedades específicas que os clientes poderão usar para obter informações sobre o nome da extensão, as configurações suportadas pela extensão e os formatos disponíveis para a extensão de entrega.  
  
 ![Processo de interface IDeliveryExtension](../../../reporting-services/extensions/delivery-extension/media/bk-ext-02.gif "processo de interface IDeliveryExtension")  
A interface IDeliveryExtension permite a validação de dados de usuário como também de clientes para aprender sobre as configurações de entrega exigidas  
  
 Para criar uma classe de extensão de entrega, implemente <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> e <xref:Microsoft.ReportingServices.Interfaces.IExtension>. O **IDeliveryExtension** interface permite que a sua extensão de entrega entregar notificações de relatório usando o <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> método e validar as configurações de extensão de entrada usando o <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ValidateUserData%2A> método. O **IExtension** interface permite que a sua extensão de entrega para implementar um nome de extensão localizado e processar informações de configuração específicas da extensão armazenadas no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] arquivo de configuração. Implementando **IExtension**, sua extensão de entrega contém o <xref:Microsoft.ReportingServices.Interfaces.Extension.LocalizedName%2A> propriedade. É altamente recomendável que [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] suporte a extensões de entrega a **LocalizedName** propriedade, para que os usuários encontrem um nome familiar para a extensão em uma interface de usuário, como o Gerenciador de relatórios.  
  
 Sua extensão de entrega também deve implementar o **ExtensionSettings** propriedade o **IDeliveryExtension** interface. O servidor de relatório usa o valor retornado pela propriedade <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ExtensionSettings%2A> para avaliar as configurações exigidas por uma extensão de entrega. Os clientes que interagem com extensões de entrega usam o método <xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A> do serviço Web Servidor de Relatório para retornar uma lista de configurações para a extensão de entrega.  
  
 Você também pode usar a sua classe de extensão de entrega para recuperar e processar dados de configuração personalizados armazenados no arquivo RSReportServer.config. Para obter mais informações sobre como processar dados de configuração personalizados, consulte o método <xref:Microsoft.ReportingServices.Interfaces.IExtension.SetConfiguration%2A>.  
  
 Para obter um exemplo **IDeliveryExtension** implementação da classe, consulte [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Consulte também  
 [Implementando uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
