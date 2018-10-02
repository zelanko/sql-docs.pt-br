---
title: Planejar o design e a implantação de relatório | Reporting Services | Microsoft Docs
ms.date: 09/12/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 1c1e265e-52a2-4de3-96fd-ca4abae01c02
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8b5e541af99ac03562347a893d67de8ad0390940
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47832324"
---
# <a name="plan-for-report-design-and-report-deployment--reporting-services"></a>Planejar a criação e implantação de relatórios | Reporting Services
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] fornece várias abordagens para criar e implantar relatórios paginados. Saiba como planejar ambientes de criação de relatório e de servidor de relatório que funcionam juntos.

Este tópico apresenta uma visão geral do suporte para definição de relatório pelos componentes do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Uma definição de relatório é um arquivo XML escrito em RDL ou RDLC. Cada definição de relatório segue uma versão específica de esquema listado no início do arquivo.  
  
 Arquivos RDL são criados no Designer de Relatórios em projetos do [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] e no Construtor de Relatórios. Os arquivos RDLC são criados com o uso de controles ReportViewer incluídos no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].
  
##  <a name="bkmk_rdl_schema_versions"></a> Versões de esquema RDL  
 A tabela a seguir lista cada versão de esquema disponível e a abreviação usada no restante deste tópico:  
  
|Abreviação|Versão do esquema|  
|------------------|--------------------|  
|2016 RDL|`http://schemas.microsoft.com/sqlserver/reporting/2016/01/reportdefinition`|
|2010 RDL|`http://schemas.microsoft.com/sqlserver/reporting/2010/01/reportdefinition`|  
|2008 RDL|`http://schemas.microsoft.com/sqlserver/reporting/2008/01/reportdefinition`|  
|2005 RDL<br /><br /> 2005 RDLC|`http://schemas.microsoft.com/sqlserver/reporting/2005/01/reportdefinition`|  
|2000 RDL|`http://schemas.microsoft.com/sqlserver/reporting/2003/10/reportdefinition`|  
  
 Para obter mais informações sobre RDL e esquemas RDL, consulte o seguinte:  
  
-   [Esquemas XML do Microsoft SQL Server](http://go.microsoft.com/fwlink/?LinkId=31850)  
  
-   [Especificações da linguagem RDL](http://go.microsoft.com/fwlink/?linkid=116865)  
  
-   [Linguagem RDL &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
 Para obter mais informações sobre os controles ReportViewer, consulte [Controles ReportViewer (Visual Studio)](http://msdn.microsoft.com/library/ms251671.aspx).  
  
##  <a name="bkmk_report_server_rdl_schema_support"></a> Suporte para servidor de relatório e esquema RDL  
 Um arquivo de definição de relatório pode ser implantado em um servidor de relatório do [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] das seguintes maneiras:  
  
-   **Designer de Relatórios:** implante um relatório do Designer de Relatórios no [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)].  
  
-   **Construtor de Relatórios:** salve um relatório no servidor de relatório do Construtor de Relatórios.  
  
-   **Portal da Web:** carregue um relatório em um servidor de relatório de modo nativo do [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)].  
  
-   **SharePoint:** carregue um relatório em um site do SharePoint configurado com um servidor de relatório do modo do SharePoint.  
  
-   **Programaticamente:** publique programaticamente um relatório usando as interfaces API SOAP em um servidor de relatório. Para obter mais informações, consulte [Report Server Web Service](../reporting-services/report-server-web-service/report-server-web-service.md).  
  
 A tabela a seguir lista a versão de esquema com suporte da versão do servidor de relatório.  
  
|Versão do servidor de relatório|Versão do esquema RDL|  
|---------------------------|------------------------|  
|SQL Server 2016|2016 RDL<br /><br />2010 RDL<br /><br /> 2008 RDL<br /><br /> 2005 RDL<br /><br /> 2000 RDL
|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]<br /><br /> Ou<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]<br /><br /> Ou<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|2010 RDL<br /><br /> 2008 RDL<br /><br /> 2005 RDL<br /><br /> 2000 RDL|  
|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|2008 RDL<br /><br /> 2005 RDL<br /><br /> 2000 RDL|  
  
 Quando você carrega ou publica uma definição de relatório ou atualiza um servidor de relatório que contém os relatórios existentes, o servidor de relatório preserva a definição de relatório no formato original. **No primeiro uso**, o servidor de relatório atualiza o relatório no banco de dados do servidor de relatório para um formato binário preservado para exibições subsequentes. A própria definição de relatório (.rdl) não é atualizada.  
  
 Você pode extrair do servidor de relatório uma cópia somente leitura do arquivo de definição de relatório (.rdl). Em um servidor de relatório de modo nativo, procure o [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)], selecione o relatório e clique em **Baixar**. Em uma implantação do modo do SharePoint, vá para a biblioteca de documentos, selecione o relatório e clique em **Baixar uma Cópia**.  
  
 Para atualizar a definição de relatório, é necessário abrir o relatório em um ambiente de criação de relatório, como SQL Server Data Tools ou Construtor de Relatórios, e salvá-lo.  
  
 Para obter mais informações sobre atualizações de relatório e versões de esquema com suporte, consulte [Atualizar relatórios](../reporting-services/install-windows/upgrade-reports.md).  
  
##  <a name="bkmk_report_authoring_and_deployment"></a> Suporte para a criação e a implantação de relatório  
 O ambiente de criação de relatórios é o Designer de Relatórios em projetos do [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] e o Construtor de Relatório. Os ambientes de criação de relatórios fornecem vários recursos de suporte para atualização de relatório, design de relatório, visualização de relatório no modo local, visualização de relatório no servidor de relatório e implantação de relatório.  
  
 A tabela a seguir resume o suporte para criar e implantar definições de relatório para versões de esquema diferentes:  
  
|Ambiente de criação|Versão de RDL criada|Implantar versão de RDL|Implantar em versões de servidor de relatório|  
|---------------------------|--------------------------|------------------------|--------------------------------------|  
|Construtor de Relatórios do SQL Server 2016|Cria o 2016 RDL<br /><br /> Atualizará versões mais antigas do RDL para o 2016 RDL|2016 RDL|SQL Server 2016|
|Designer de Relatórios no SQL Server 2016 Data Tools – Business Intelligence para Microsoft Visual Studio 2015|Cria o 2016 RDL<br /><br /> Atualizará versões mais antigas do RDL para o 2016 RDL|2016 RDL|SQL Server 2016|
|Designer de Relatórios no SQL Server 2014 Data Tools – Business Intelligence para Microsoft Visual Studio 2012<br /><br /> Ou<br /><br /> Designer de Relatórios no SQL Server 2012 Data Tools – Business Intelligence para Microsoft Visual Studio 2012<br /><br /> Ou<br /><br /> O Designer de Relatórios no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Data Tools, incluído no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].|Cria 2010 RDL<br /><br /> Atualizará versões mais antigas do RDL para o 2010 RDL|2010 RDL|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|Designer de Relatórios no [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] Business Intelligence Development Studio|Cria 2010 RDL<br /><br /> Atualizará versões mais antigas do RDL para o 2010 RDL|2010 RDL|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|Designer de Relatórios no [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Business Intelligence Development Studio|Cria 2008 RDL<br /><br /> Atualizará versões mais antigas do RDL para o 2008 RDL|2008 RDL|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|
  
 Para obter mais informações sobre o SSDT (SQL Server Data Tools), consulte:  
  
-   [Implantação e suporte de versão no SQL Server Data Tools &#40;SSRS&#41;](../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)  
  
-   [SQL Server Data Tools para Visual Studio 2015](../ssdt/download-sql-server-data-tools-ssdt.md).  
  
##  <a name="bkmk_reportviewer"></a> Controles ReportViewer  
 Um controle [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ReportViewer pode exibir um relatório .rdlc no modo de visualização local ou no modo remoto, o controle pode exibir um arquivo .rdl hospedado em um servidor de relatório [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . A tabela a seguir fornece a lista de versões de RDL com suporte dos controles ReportViewer para processamento local (.rdlc). O suporte para RDL no lado do servidor é resumido na seção [Suporte para servidor de relatório e esquema RDL](#bkmk_report_server_rdl_schema_support).  
  
|Controle ReportViewer no produto|Versão do RDL para a visualização local|  
|-------------------------------------|--------------------------------------|  
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 2015 <br/><br/>Ou<br/><br/>[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 2013<br /><br /> Ou<br /><br /> [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 2012<br /><br /> Ou<br /><br /> [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]|2008 RDL|  
|[!INCLUDE[vsprvslong](../includes/vsprvslong-md.md)]<br /><br /> Ou<br /><br /> [!INCLUDE[vsOrcas](../includes/vsorcas-md.md)]|2005 RDL|  
  
 Para obter mais informações, consulte o seguinte:  
  
-   [Convertendo arquivos RDLC em arquivos RDL](http://msdn.microsoft.com/library/ms252109.aspx)  
  
-   [Controles ReportViewer (Visual Studio)](http://msdn.microsoft.com/library/ms251671.aspx)  
  
-   [Adicionando e configurando controles ReportViewer](http://msdn.microsoft.com/library/ms252104.aspx)  
  
## <a name="see-also"></a>Consulte Também  
 [Relatórios, partes de relatório e definições de relatório &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [Ferramentas do Reporting Services](../reporting-services/tools/reporting-services-tools.md)   
 [Linguagem RDL &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
