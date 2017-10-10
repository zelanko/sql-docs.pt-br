---
title: Instalar o SharePoint do Reporting Services no modo | Microsoft Docs
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
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 4bba09c0ec60a810faf3d7ef8e75a7a43661dfba
ms.contentlocale: pt-br
ms.lasthandoff: 10/06/2017

---
# <a name="install-reporting-services-sharepoint-mode"></a>Instalar o modo do SharePoint do Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)][!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

SQL Server Reporting Services no SharePoint, ativa a criação de relatórios e exibição em bibliotecas de documentos, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] entrega de assinatura de relatórios por email, [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], alertas de dados e recursos de gerenciamento de relatórios, tudo em uma implantação com base no [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint. Para obter mais informações sobre recursos no modo do SharePoint, consulte a seção "Recurso de suporte e comportamento diferenças pelo modo de servidor" em [servidor de relatório do Reporting Services](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md).

> [!NOTE]
> Integração do Reporting Services com o SharePoint não está mais disponível após o SQL Server 2016.

Há dois componentes principais do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a serem instalados para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint:  

|Instalação|Descrição|  
|------------------|-----------------|  
|**Servidor de Relatório:** o servidor de relatório do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é instalado no Modo do SharePoint|O servidor de relatório controla o processamento e a renderização de dados e de relatórios, bem como a assinatura e o processamento de Alerta de Dados O servidor de relatório no modo do SharePoint é projetado e instalado como um Serviço Compartilhado do SharePoint.<br /><br /> **Como:** usar as mídia de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instalar o servidor de relatório.|  
|**Suplemento:** o servidor de relatório do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos SharePoint, **rssharepoint.msi**.|O suplemento instala páginas e recursos de interface do usuário [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em um servidor front-end de Web do SharePoint. Os recursos de interface do usuário incluem o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], páginas de administração na Administração Central do SharePoint, páginas de recursos usadas em bibliotecas de documentos do SharePoint e páginas de alertas de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .<br /><br /> **Como:**  o suplemento pode ser instalado por meio de um download da Web ou pela mídia de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, veja [Onde encontrar o suplemento Reporting Services para produtos do SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).|  
  
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

## <a name="next-steps"></a>Próximas etapas

 [Arquitetura de alertas de dados e fluxo de trabalho](../../reporting-services/reporting-services-data-alerts.md#AlertingWF)   
 [Gerenciador de alertas de dados para os administradores de alerta](../../reporting-services/data-alert-manager-for-alerting-administrators.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
