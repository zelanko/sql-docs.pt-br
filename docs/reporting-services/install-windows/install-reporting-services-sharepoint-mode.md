---
title: Instalar o Reporting Services no modo do SharePoint | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 06/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- default configuration [Reporting Services]
- installing Reporting Services, SharePoint integrated mode
- installation options [Reporting Services]
ms.assetid: ac6cba68-2665-4a39-8fa3-cb7d7e6723c0
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b2c77f21304b04b5349691b6c464026fe944a4eb
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="install-reporting-services-sharepoint-mode"></a>Instalar o Reporting Services no modo do SharePoint
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no SharePoint permite a criação de relatórios e a exibição em bibliotecas de documentos, entrega da assinatura do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de relatórios por email,  [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], alertas de dados e recursos de gerenciamento de relatórios, tudo em uma implantação com base no [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint. Para obter mais informações sobre recursos no modo do SharePoint, veja a seção “Suporte a recursos e diferenças de comportamento por modo de servidor” em [Servidor de Relatório do Reporting Services](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md)  
  
 Há dois componentes principais do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a serem instalados para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint:  
  
|Instalação|Descrição|  
|------------------|-----------------|  
|**Servidor de Relatório:** o servidor de relatório do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é instalado no Modo do SharePoint|O servidor de relatório controla o processamento e a renderização de dados e de relatórios, bem como a assinatura e o processamento de Alerta de Dados O servidor de relatório no modo do SharePoint é projetado e instalado como um Serviço Compartilhado do SharePoint.<br /><br /> **Como:** usar as mídia de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instalar o servidor de relatório.|  
|**Add-in:** The [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] add-in for SharePoint products, **rssharepoint.msi**.|O suplemento instala páginas e recursos de interface do usuário [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em um servidor front-end de Web do SharePoint. Os recursos de interface do usuário incluem o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], páginas de administração na Administração Central do SharePoint, páginas de recursos usadas em bibliotecas de documentos do SharePoint e páginas de alertas de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .<br /><br /> **Como:**  o suplemento pode ser instalado por meio de um download da Web ou pela mídia de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, veja [Onde encontrar o suplemento Reporting Services para produtos do SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).|  
  
## <a name="in-this-section"></a>Nesta seção  
 [Combinações do SharePoint e do servidor e suplemento Reporting Services com suporte &#40;SQL Server 2016&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
 [Onde encontrar o suplemento Reporting Services para produtos do SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
 [Instalar o Primeiro Servidor de Relatório no Modo do SharePoint](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md)  
  
 [Instalar ou desinstalar o suplemento Reporting Services para SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
 [Adicionar um servidor de relatório a um farm &#40;Expansão do SSRS&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
 [Adicionar um front-end da Web do Reporting Services a um farm](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 [Configurar o email para um serviço de aplicativo do Reporting Services &#40;SharePoint 2013 e SharePoint 2016&#41;](http://msdn.microsoft.com/en-us/38fc34a6-aae7-4dde-9ad2-f1eee0c42a9f)  
  
 [Provisionar Assinaturas e Alertas para aplicativos de serviço SSRS](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)  
  
 [C2WTS &#40;Declarações para Serviço de Token do Windows&#41; e Reporting Services](../../reporting-services/install-windows/claims-to-windows-token-service-c2wts-and-reporting-services.md)  
  
## <a name="see-also"></a>Consulte também  
 [Arquitetura de alertas de dados e fluxo de trabalho](../../reporting-services/reporting-services-data-alerts.md#AlertingWF)   
 [Gerenciador de Alertas de dados para administradores de alertas](../../reporting-services/data-alert-manager-for-alerting-administrators.md)  
  
  

