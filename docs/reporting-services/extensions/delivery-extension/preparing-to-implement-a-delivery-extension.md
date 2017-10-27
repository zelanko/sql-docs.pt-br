---
title: "Preparando para implementar uma extensão de entrega | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
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
- interfaces [Reporting Services]
- delivery extensions [Reporting Services], implementing
ms.assetid: aee1608d-374f-4ad3-bc23-fe07fdaa52b7
caps.latest.revision: 34
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 7bbaf0976e9b145df33e04eea93a5d2ae0408c11
ms.contentlocale: pt-br
ms.lasthandoff: 08/12/2017

---
# <a name="preparing-to-implement-a-delivery-extension"></a>Preparando para implementar uma entrega de extensão
  Antes de implementar a sua extensão de entrega do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], você deve definir as interfaces a serem implementadas. Primeiro você precisa decidir como a sua extensão de entrega será usada, que configurações a sua extensão de entrega exigirá e a funcionalidade específica de que você precisará implementar para entregar notificações de relatório.  
  
 Cada extensão de entrega do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] deve fornecer a seguinte funcionalidade:  
  
-   Uma implementação de interface <xref:Microsoft.ReportingServices.Interfaces.IExtension> que representa a extensão e um nome de extensão localizado.  
  
-   Uma implementação <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> que cria uma extensão de entrega que pode ser usada para entregar notificações de relatório a usuários finais.  
  
-   A habilidade para processar dados de usuário específicos para uma assinatura.  
  
 Cada extensão de entrega pode ser aprimorada para incluir a seguinte funcionalidade:  
  
-   Uma implementação de controle de usuário do [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] que permite que usuários finais usem o Gerenciador de Relatórios para criar assinaturas de relatório que usam a extensão de entrega.  
  
 A tabela a seguir descreve as interfaces e as classes disponíveis para extensões de entrega.  
  
|Interface ou classe|Description|  
|------------------------|-----------------|  
|<xref:Microsoft.ReportingServices.Interfaces.IExtension> Interface|Representa uma extensão no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
|<xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> Interface|Representa uma extensão de entrega no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
|<xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation> Interface|Contém informações sobre o servidor de relatório exigido por extensões de entrega (por exemplo, uma lista das extensões de renderização disponíveis).|  
|<xref:Microsoft.ReportingServices.Interfaces.Setting>Classe|Representa uma configuração para uma extensão.|  
|<xref:Microsoft.ReportingServices.Interfaces.Notification>Classe|Contém informações de assinatura que extensões de entrega usam para entregar relatórios.|  
|<xref:Microsoft.ReportingServices.Interfaces.Report>Classe|Representa informações e métodos específicos do relatório métodos que permitem que extensões de entrega enviem relatórios a usuários.|  
|<xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>Classe|Representa a saída de uma extensão de renderização. Um objeto <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> contém o nome de arquivo associado e as informações de tipo exigidos pela extensão de entrega para o processamento do fluxo retornado pela extensão de renderização.|  
|<xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> Interface|Um controle de usuário que representa o meio de recuperação de informações de assinatura específicas da extensão de entrega do usuário no Gerenciador de Relatórios (por exemplo, um endereço de email ou o caminho para um compartilhamento de arquivo).|  
  
## <a name="see-also"></a>Consulte também  
 [Extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementando uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

