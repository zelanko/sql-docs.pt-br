---
title: Os recursos no SQL Server Reporting Services no SQL Server 2014 preteridos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Reporting Services, backward compatibility
- deprecated features [Reporting Services]
- HTML OWC rendering extension [Reporting Services]
- Report Server Web service, endpoints
ms.assetid: 3876c01e-f81d-4cce-9104-5106a8c369e6
caps.latest.revision: 49
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: a52d82f4a2126c12dad3ec19cde3cc93ff22368d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118605"
---
# <a name="deprecated-features-in-sql-server-reporting-services-in-sql-server-2014"></a>Recursos preteridos no SQL Server Reporting Services do SQL Server 2014
  Este tópico descreve os recursos preteridos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Os recursos ainda estão disponíveis na versão em que foram preteridos; porém, os recursos estão agendados para ser removidos em uma versão futura do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Recursos preteridos não devem ser usados em aplicativos novos.  
  
 Neste tópico:  
  
-   [Recursos preteridos SQL Server 2014 Reporting Services](#bkmk_2014)  
  
-   [Recursos preteridos SQL Server 2012 SP1 Reporting Services](#bkmk_2012sp1)  
  
-   [Recursos preteridos SQL Server 2012 Reporting Services](#bkmk_2012)  
  
-   [Recursos preteridos SQL Server 2008 R2 Reporting Services](#bkmk_kj)  
  
##  <a name="bkmk_2014"></a> Recursos preteridos SQL Server 2014 Reporting Services  
  
### <a name="features-not-supported-in-the-next-version-of-sql-server"></a>Recursos sem suporte na próxima versão do SQL Server  
 O seguinte [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] recursos não terão suporte no **próximo** versão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Não use esses recursos em novo trabalho de desenvolvimento e, assim que possível, modifique os aplicativos que os utilizam atualmente.  
  
#### <a name="html-rendering-extension-device-information-settings"></a>Configurações de informações de dispositivos para extensões de renderização HTML  
 As configurações de informações de dispositivos da extensão de renderização HTML a seguir foram preteridas.  
  
-   ActionScript  
  
-   ActiveXControls  
  
-   GetImage  
  
-   OnlyVisibleStyles  
  
-   ReplacementRoot  
  
-   ResourceStreamRoot  
  
-   StreamRoot  
  
-   UsePx  
  
-   Zoom  
  
 Para obter mais informações sobre a extensão de renderização HTML, consulte [HTML Device Information Settings](html-device-information-settings.md)  
  
#### <a name="microsoft-word-and-microsoft-excel-1997-2003-rendering"></a>Renderização do Microsoft Word e do Microsoft Excel 1997-2003  
 O[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] extensões de renderização BIFF8 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] relatórios para o [!INCLUDE[msCoName](../includes/msconame-md.md)] Word e [!INCLUDE[msCoName](../includes/msconame-md.md)] formato de arquivo de intercâmbio binário do Excel 1997-2003. [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Inclui extensões de renderização no [!INCLUDE[msCoName](../includes/msconame-md.md)] formato do Office 2007-2010 Open XML.  
  
#### <a name="report-definition-language-rdl-2005-and-earlier"></a>Linguagem RDL 2005 e versões anteriores  
 A linguagem RDL 2005 e as versões anteriores foram preteridos. Para obter mais informações sobre RDL, consulte [linguagem de definição de relatório &#40;SSRS&#41;](reports/report-definition-language-ssrs.md).  
  
 Para obter mais informações sobre como atualizar relatórios, consulte [atualizar relatórios](install-windows/upgrade-reports.md).  
  
#### <a name="sql-server-2005-and-earlier-custom-report-items"></a>Itens de relatório personalizados do SQL Server 2005 e versões anteriores  
 Itens de relatório personalizado (CRI) compilados para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005 e versões anteriores foram preteridos.  
  
#### <a name="reporting-services-snapshots-2005-and-earlier"></a>Instantâneos do Reporting Services 2005 e versões anteriores  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] renderizados com [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005 e versões anteriores foram preteridos.  
  
#### <a name="report-models"></a>Modelos de relatório  
 Os modelos de relatório SMDL (linguagem de modelagem semântica) foram preteridos. Embora você possa continuar a usar modelos de relatório existentes como fontes de dados em [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] relata Considere atualizar seus relatórios para remover a dependência de modelos de relatório.  
  
 O [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não contém ferramentas para criar ou atualizar modelos de relatório. Para obter mais informações, consulte [alterações recentes no SQL Server Reporting Services no SQL Server 2014](breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md).  
  
#### <a name="deprecated-methods-in-the-web-service-endpoint"></a>Métodos preteridos no ponto de extremidade de serviço Web  
 As operações a seguir estão obsoletas no <xref:ReportService2010.ReportingService2010> ponto de extremidade de serviço Web:  
  
-   <xref:ReportService2010.ReportingService2010.GetProperties%2A>  
  
-   <xref:ReportService2010.ReportingService2010.IsSSLRequired%2A>  
  
#### <a name="sharepoint-web-parts"></a>Web Parts do SharePoint  
 O arquivo de gabinete de instalação **RSWebParts.cab** e as Web Parts do SharePoint que podem ser extraídos do arquivo cab são preteridos. As web parts preteridas são o navegador de relatórios (**SPExplorer.dwp**) e o Visualizador de relatórios (**SPViewer.dwp**).  
  
 Para obter mais informações sobre as web parts preteridas, consulte [exibir e explorar modo nativo relatórios usando SharePoint Web Parts (SSRS)](http://msdn.microsoft.com/library/ms159772.aspx)  
  
### <a name="features-not-supported-in-a-future-version-of-sql-server"></a>Recursos sem suporte em uma versão futura do SQL Server  
 Os recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] a seguir terão suporte na próxima versão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], mas serão removidos em uma versão posterior. A versão específica do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não foi determinada.  
  
 Não [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] recursos foram preteridos no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
##  <a name="bkmk_2012sp1"></a> Recursos preteridos SQL Server 2012 SP1 Reporting Services  
 Esta seção descreve [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] recursos preteridos no [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]. Os recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] a seguir terão suporte na próxima versão do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], mas serão removidos em uma versão posterior. A versão específica do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não foi determinada.  
  
### <a name="sharepoint-web-parts"></a>Web Parts do SharePoint  
 O arquivo de gabinete de instalação **RSWebParts.cab** e as Web Parts do SharePoint que podem ser extraídos do arquivo cab são preteridos. As web parts preteridas são o navegador de relatórios (**SPExplorer.dwp**) e o Visualizador de relatórios (**SPViewer.dwp**).  
  
 Para obter mais informações sobre as web parts preteridas, consulte [exibir e explorar modo nativo relatórios usando SharePoint Web Parts (SSRS)](http://msdn.microsoft.com/library/ms159772.aspx)  
  
##  <a name="bkmk_2012"></a> Recursos preteridos SQL Server 2012 Reporting Services  
 Esta seção descreve [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] recursos preteridos no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
### <a name="html-rendering-extension-device-information-settings"></a>Configurações de informações de dispositivos para extensões de renderização HTML  
 As configurações de informações de dispositivos da extensão de renderização HTML a seguir foram preteridas.  
  
-   ActionScript  
  
-   ActiveXControls  
  
-   GetImage  
  
-   OnlyVisibleStyles  
  
-   ReplacementRoot  
  
-   ResourceStreamRoot  
  
-   StreamRoot  
  
-   UsePx  
  
-   Zoom  
  
 Para obter mais informações sobre a extensão de renderização HTML, consulte [HTML Device Information Settings](html-device-information-settings.md)  
  
### <a name="microsoft-word-and-microsoft-excel-1997-2003-rendering"></a>Renderização do Microsoft Word e do Microsoft Excel 1997-2003  
 O[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] extensões de renderização BIFF8 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] relatórios para o [!INCLUDE[msCoName](../includes/msconame-md.md)] Word e [!INCLUDE[msCoName](../includes/msconame-md.md)] formato de arquivo de intercâmbio binário do Excel 1997-2003. [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Inclui extensões de renderização no [!INCLUDE[msCoName](../includes/msconame-md.md)] formato do Office 2007-2010 Open XML.  
  
### <a name="report-definition-language-rdl-2005-and-earlier"></a>Linguagem RDL 2005 e versões anteriores  
 A linguagem RDL 2005 e as versões anteriores foram preteridos. Para obter mais informações sobre RDL, consulte [linguagem de definição de relatório &#40;SSRS&#41;](reports/report-definition-language-ssrs.md).  
  
 Para obter mais informações sobre como atualizar relatórios, consulte [atualizar relatórios](install-windows/upgrade-reports.md).  
  
### <a name="sql-server-2005-and-earlier-custom-report-items"></a>Itens de relatório personalizados do SQL Server 2005 e versões anteriores  
 Itens de relatório personalizado (CRI) compilados para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005 e versões anteriores foram preteridos.  
  
### <a name="reporting-services-snapshots-2005-and-earlier"></a>Instantâneos do Reporting Services 2005 e versões anteriores  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] renderizados com [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005 e versões anteriores foram preteridos.  
  
### <a name="report-models"></a>Modelos de relatório  
 Os modelos de relatório SMDL (linguagem de modelagem semântica) foram preteridos. Embora você possa continuar a usar modelos de relatório existentes como fontes de dados em [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] relata Considere atualizar seus relatórios para remover a dependência de modelos de relatório.  
  
 O [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não contém ferramentas para criar ou atualizar modelos de relatório. Para obter mais informações, consulte [alterações recentes no SQL Server Reporting Services no SQL Server 2014](breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md).  
  
### <a name="deprecated-methods-in-the-web-service-endpoint"></a>Métodos preteridos no ponto de extremidade de serviço Web  
 As operações a seguir estão obsoletas no <xref:ReportService2010.ReportingService2010> ponto de extremidade de serviço Web:  
  
-   <xref:ReportService2010.ReportingService2010.GetProperties%2A>  
  
-   <xref:ReportService2010.ReportingService2010.IsSSLRequired%2A>  
  
##  <a name="bkmk_kj"></a> Recursos preteridos SQL Server 2008 R2 Reporting Services  
  
> [!NOTE]  
>  Como o SQL Server 2008 R2 é uma atualização de versão secundária do SQL Server 2008, recomendamos que você também revise o conteúdo na seção do SQL Server 2008.  
  
### <a name="report-server-web-service-endpoints"></a>Pontos de extremidade do serviço Web Servidor de Relatórios  
 Os serviços Web <xref:ReportService2005.ReportingService2005> e <xref:ReportService2006.ReportingService2006> foram substituídos nesta versão. Esses pontos de extremidade foram substituídos por um novo ponto de extremidade: <xref:ReportService2010.ReportingService2010>.  
  
 O novo ponto de extremidade inclui toda a funcionalidade disponível nos pontos de extremidade preteridos e os novos recursos introduzidos no SQL Server 2008 R2.  
  
## <a name="see-also"></a>Consulte também  
 [O que há de novo &#40;Reporting Services&#41;](what-s-new-reporting-services.md)   
 [Compatibilidade com versões anteriores](../getting-started/backward-compatibility.md)   
 [Alterações de comportamento no SQL Server Reporting Services no SQL Server 2014](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [Funcionalidade descontinuada do SQL Server Reporting Services no SQL Server 2014](discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)  
  
  