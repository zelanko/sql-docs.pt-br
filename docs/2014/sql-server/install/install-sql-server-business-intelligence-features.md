---
title: Install SQL Server 2014 BI Features
ms.custom: ''
ms.prod: sql-server-2014
ms.reviewer: ''
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.date: 10/24/2018
ms.technology: install
ms.openlocfilehash: 93f362adfbc85500854943a479dac01988eb3a01
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952559"
---
# <a name="install-sql-server-2014-bi-features"></a>Install SQL Server 2014 BI Features

  Recursos do SQL Server que são parte da plataforma Microsoft Business Intelligence e que incluem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]e vários aplicativos cliente usados para criação ou funcionamento com dados analíticos. Esta seção da documentação da Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explica como instalar esses recursos.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] podem ser instalados como servidores autônomos, em configurações em expansão, ou como aplicativos de serviço compartilhado em um farm do SharePoint. A instalação dos serviços em um farm habilita os recursos de BI que estão disponíveis apenas no SharePoint, incluindo o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint e o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], o designer de relatórios interativos ad hoc do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que é executado nos bancos de dados de modelo de tabela do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ou do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Se você já estiver familiarizado com as etapas de instalação de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]ou PowerPivot para SharePoint, poderá pular para as listas de verificação para obter orientação sobre como habilitar cenários específicos. Para obter mais informações, consulte [listas de verificação para instalar recursos de BI com o SharePoint](checklists-for-installing-bi-features-with-sharepoint.md).  
  
## <a name="contents"></a>Sumário

Nesta seção:
  
|Link|Tarefa|  
|----------|----------|  
|[Listas de verificação para instalar recursos com SharePoint](checklists-for-installing-bi-features-with-sharepoint.md)|Se você já souber o que deseja instalar e estiver familiarizado com as etapas de instalação para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]ou [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, poderá usar as listas de verificação nesta seção para orientação em ordem de instalação, conta e requisitos de permissão e etapas que implantam topologias avançadas, inclusive multisservidor e implantações de multirrecurso.|  
|[Instalar SQL Server recursos do BI com &#40;o SharePoint PowerPivot e Reporting Services&#41;](install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md)|Esta seção explica como instalar recursos de SQL Server em um ambiente do SharePoint. Ela identifica quais recursos de SQL Server estão disponíveis para uma versão e uma edição específicas do SharePoint. Ela também inclui procedimentos de instalação de PowerPivot para SharePoint e de Reporting Services no modo do SharePoint.|  
|[Instalar o Analysis Services em modo multidimensional e de mineração de dados](install-analysis-services-in-multidimensional-and-data-mining-mode.md)<br /><br /> [Instalar o Analysis Services em modo Tabular](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services)<br /><br /> [Instalar o Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)<br /><br /> [Instalar o Integration Services](../../integration-services/install-windows/install-integration-services.md)<br /><br /> [Instalar o Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)<br /><br /> [Instalar o servidor de relatórios de modo nativo do Reporting Services](../../reporting-services/install-windows/install-reporting-services-native-mode-report-server.md)|Esta seção fornece instruções sobre como instalar o Analysis Services, o Integration Services, o Master Data Services e o Reporting Services, quando o Analysis Services e o Reporting Services estão instalados sem o SharePoint. Isso às vezes é referenciado como *modo nativo*, sendo o cenário de instalação mais comum do Reporting Services e do Analysis Services. Nesta seção, você saberá sobre opções de instalação que determinam diretamente o contexto operacional de seu servidor. Para o Reporting Services, este poderia ser um servidor que é pré-configurado ou um que requer várias etapas de configuração antes de você poder usá-lo. Para o Analysis Services, as opções de instalação que você seleciona determinarão o tipo de projeto que a ser implantado para o servidor.|  
|[Verificar ou solucionar problemas de instalação do recurso de BI SQL Server](../../../2014/sql-server/install/verify-or-troubleshoot-sql-server-bi-feature-installation-problems.md)|Esta seção inclui etapas para verificar uma instalação. Ela também fornece links para informações de resolução de problema na Web.|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
|Link|Tarefa|  
|----------|----------|  
|[Atualizar para o SQL Server 2014](../../database-engine/install-windows/upgrade-sql-server.md)<br /><br /> [Atualizar o Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)<br /><br /> [Atualizar o PowerPivot para SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)<br /><br /> [Atualizar e migrar o Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)|Use as instruções nesta seção para atualizar servidores e conteúdo de uma versão anterior para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|[Desinstalar o SQL Server 2014](uninstall-sql-server.md)<br /><br /> [Desinstalar o PowerPivot para SharePoint](../../../2014/sql-server/install/uninstall-power-pivot-for-sharepoint.md)<br /><br /> [Desinstalar o Reporting Services](../../../2014/sql-server/install/uninstall-reporting-services.md)|Use as instruções nesta seção para desinstalar recursos do BI.|  
  
## <a name="see-also"></a>Consulte também

* [Novidades &#40;Reporting Services&#41;](../../../2014/reporting-services/what-s-new-reporting-services.md)

* [O que há de novo no Analysis Services e Business Intelligence](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services)

* [Instalar o SQL Server 2014](../../database-engine/install-windows/install-sql-server.md)

* [Atualizar para o SQL Server 2014](../../database-engine/install-windows/upgrade-sql-server.md)
