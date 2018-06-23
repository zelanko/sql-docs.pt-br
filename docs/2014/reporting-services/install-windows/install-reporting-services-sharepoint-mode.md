---
title: Instalação do modo do SharePoint (SharePoint 2010 e SharePoint 2013) do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- default configuration [Reporting Services]
- installing Reporting Services, SharePoint integrated mode
- installation options [Reporting Services]
ms.assetid: ac6cba68-2665-4a39-8fa3-cb7d7e6723c0
caps.latest.revision: 30
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: f0e75a75ffb14f720f2b421d659fa6142b579019
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36005846"
---
# <a name="reporting-services-sharepoint-mode-installation-sharepoint-2010-and-sharepoint-2013"></a>Instalação do modo do SharePoint do Reporting Services (SharePoint 2010 e SharePoint 2013)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no SharePoint modo é uma coleção de componentes de servidor que fornecem geração de relatórios e entrega, com base em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[msCoName](../../includes/msconame-md.md)] produtos do SharePoint.  
  
 A execução do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em modo do SharePoint fornece o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] e recursos de alerta de dados. Para obter mais informações sobre recursos no modo do SharePoint, veja a seção “Suporte a recursos e diferenças de comportamento por modo de servidor” em [Servidor de Relatório do Reporting Services](../reporting-services-report-server.md)  
  
 Há duas instalações fundamentais necessárias ao [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint:  
  
|Instalação|Description|  
|------------------|-----------------|  
|O [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] suplemento para produtos do SharePoint.|O suplemento instala páginas e recursos de interface do usuário [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em um servidor front-end de Web do SharePoint. Os recursos de interface do usuário incluem o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], páginas de administração na Administração Central do SharePoint, páginas de recursos usadas em bibliotecas de documentos do SharePoint e páginas de alertas de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|O [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servidor de relatório instalado no modo do SharePoint|O servidor de relatório controla o processamento e a renderização de dados e de relatórios, bem como a assinatura e o processamento de Alerta de Dados O servidor de relatório no modo do SharePoint é projetado e instalado como um Serviço Compartilhado do SharePoint.|  
  
 Para instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], use a mídia de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Para obter instruções sobre cenários de implantação avançada, consulte [lista de verificação de implantação: Reporting Services, Power View e PowerPivot para SharePoint](../../sql-server/install/deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md) e [lista de verificação de implantação: instalar o Reporting Services em um existente Farm do SharePoint](../../sql-server/install/deployment-checklist-install-reporting-services-existing-sharepoint-farm.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Combinações do SharePoint e Reporting Services Server e o suplemento com suporte &#40;do SQL Server 2014&#41;](supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
 [Instalar o Reporting Services SharePoint Mode para SharePoint 2013](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)  
  
 [Instalar o Reporting Services no modo do SharePoint para SharePoint 2010](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
 [Instalar ou desinstalar o Reporting Services suplemento para SharePoint &#40;do SharePoint 2010 e SharePoint 2013&#41;](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
 [Onde encontrar o suplemento Reporting Services para produtos do SharePoint](where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
 [Adicionar um servidor de relatório a um Farm &#40;expansão do SSRS&#41;](add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
 [Adicionar um front-end da Web do Reporting Services a um farm](add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 [Configure o email para o do aplicativo de serviço Reporting Services &#40;do SharePoint 2010 e SharePoint 2013&#41;](configure-e-mail-for-a-reporting-services-service-application.md)  
  
 [Provisionar assinaturas e alertas para aplicativos de serviço SSRS](provision-subscriptions-and-alerts-for-ssrs-service-applications.md)  
  
 [Claims to Windows Token Service &#40;C2WTS&#41; e o Reporting Services](../../sql-server/install/claims-to-windows-token-service-c2wts-and-reporting-services.md)  
  
## <a name="see-also"></a>Consulte também  
 [Arquitetura e fluxo de trabalho de alertas de dados](../reporting-services-data-alerts.md#AlertingWF)   
 [Gerenciador de alertas de dados para os administradores de alerta](../data-alert-manager-for-alerting-administrators.md)  
  
  