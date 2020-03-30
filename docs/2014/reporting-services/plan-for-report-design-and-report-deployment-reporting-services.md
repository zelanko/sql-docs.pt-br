---
title: Plano de elaboração de relatórios e implantação de relatórios (Reporting Services 2014) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 1c1e265e-52a2-4de3-96fd-ca4abae01c02
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d3047dba3e54d384f2f52733e8cf49308b793190
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2020
ms.locfileid: "80380817"
---
# <a name="plan-for-report-design-and-report-deployment-reporting-services-2014"></a>Planejar a criação e a implantação de relatórios (Reporting Services 2014)
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] fornece várias abordagens para a autoria e implantação de relatórios. Use este tópico para aprender a planejar um ambiente de criação de relatórios e servidor de relatório que funcionam em conjunto. Este tópico apresenta uma visão geral do suporte para definição de relatório pelos componentes do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Uma definição de relatório é um arquivo XML escrito em RDL ou RDLC. Cada definição de relatório segue uma versão específica de esquema listado no início do arquivo.  
  
 Arquivos RDL são criados no Designer de Relatórios em projetos do [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] e no Construtor de Relatórios 3.0. Os arquivos RDLC são criados com o uso de controles ReportViewer incluídos no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
 Neste tópico:  
  
-   [Versões de Esquema RDL](#bkmk_rdl_schema_versions)  
  
-   [Suporte ao servidor de relatórios e ao esquema RDL](#bkmk_report_server_rdl_schema_support)  
  
-   [Suporte à autoria e implantação de relatórios](#bkmk_report_authoring_and_deployment)  
  
-   [Controles do ReportViewer](#bkmk_reportviewer)  
  
##  <a name="rdl-schema-versions"></a><a name="bkmk_rdl_schema_versions"></a> Versões de esquema RDL  
 A tabela a seguir lista cada versão de esquema disponível e a abreviação usada no restante deste tópico:  
  
|Abreviação|Versão do esquema|  
|------------------|--------------------|  
|2010 RDL|`https://schemas.microsoft.com/sqlserver/reporting/2010/01/reportdefinition`|  
|2008 RDL|`https://schemas.microsoft.com/sqlserver/reporting/2008/01/reportdefinition`|  
|2005 RDL<br /><br /> 2005 RDLC|`https://schemas.microsoft.com/sqlserver/reporting/2005/01/reportdefinition`|  
|2000 RDL|`https://schemas.microsoft.com/sqlserver/reporting/2003/10/reportdefinition`|  
  
 Para obter mais informações sobre RDL e esquemas RDL, consulte o seguinte:  
  
-   [Esquemas XML do Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkId=31850)  
  
-   [Especificações da linguagem RDL](https://go.microsoft.com/fwlink/?linkid=116865)  
  
-   [Linguagem RDL &#40;SSRS&#41;](reports/report-definition-language-ssrs.md)  
  
 Para obter mais informações sobre os controles ReportViewer, consulte [Controles ReportViewer (Visual Studio)](https://msdn.microsoft.com/library/ms251671.aspx).  
  
##  <a name="report-server-and-rdl-schema-support"></a><a name="bkmk_report_server_rdl_schema_support"></a> Suporte para servidor de relatório e esquema RDL  
 Um arquivo de definição de relatório pode ser implantado em um servidor de relatório do [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] das seguintes maneiras:  
  
-   **Designer de Relatórios:** implante um relatório do Designer de Relatórios no [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)].  
  
-   **Construtor de Relatórios:** salve um relatório no servidor de relatório do Construtor de Relatórios.  
  
-   **Gerenciador de Relatórios:** carregue um relatório para um servidor de relatório de modo nativo do Gerenciador de Relatórios.  
  
-   **SharePoint:** carregue um relatório em um site do SharePoint configurado com um servidor de relatório do modo do SharePoint.  
  
-   **Programaticamente:** publique programaticamente um relatório usando as interfaces API SOAP em um servidor de relatório. Para obter mais informações, consulte [Report Server Web Service](report-server-web-service/report-server-web-service.md).  
  
 A tabela a seguir lista a versão de esquema com suporte da versão do servidor de relatório.  
  
|Versão do servidor de relatório|Versão do esquema RDL|  
|---------------------------|------------------------|  
|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]<br /><br /> Ou<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]<br /><br /> Ou<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|2010 RDL<br /><br /> 2008 RDL<br /><br /> 2005 RDL<br /><br /> 2000 RDL|  
|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|2008 RDL<br /><br /> 2005 RDL<br /><br /> 2000 RDL|  
|[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]|2005 RDL<br /><br /> 2000 RDL|  
  
 Quando você carrega ou publica uma definição de relatório ou atualiza um servidor de relatório que contém os relatórios existentes, o servidor de relatório preserva a definição de relatório no formato original. **No primeiro uso**, o servidor de relatório atualiza o relatório no banco de dados do servidor de relatório para um formato binário preservado para exibições subsequentes. A própria definição de relatório (.rdl) não é atualizada.  
  
 Você pode extrair do servidor de relatório uma cópia somente leitura do arquivo de definição de relatório (.rdl). Em um servidor de relatório de modo nativo, navegue para o gerenciador de relatório, selecione o relatório e clique em **Baixar**. Em uma implantação do modo do SharePoint, vá para a biblioteca de documentos, selecione o relatório e clique em **Baixar uma Cópia**.  
  
 Para atualizar a definição de relatório, abra o relatório em um ambiente de criação de relatório e salve-o.  
  
 Para obter mais informações sobre atualizações de relatório e versões de esquema com suporte, consulte [Atualizar relatórios](install-windows/upgrade-reports.md).  
  
##  <a name="report-authoring-and-deployment-support"></a><a name="bkmk_report_authoring_and_deployment"></a> Suporte para a criação e a implantação de relatório  
 O ambiente de criação de relatórios é o Designer de Relatórios em projetos do [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] e o Construtor de Relatório. Os ambientes de criação de relatórios fornecem vários recursos de suporte para atualização de relatório, design de relatório, visualização de relatório no modo local, visualização de relatório no servidor de relatório e implantação de relatório.  
  
 A tabela a seguir resume o suporte para criar e implantar definições de relatório para versões de esquema diferentes:  
  
|Ambiente de criação|Versão de RDL criada|Implantar versão de RDL|Implantar em versões de servidor de relatório|  
|---------------------------|--------------------------|------------------------|--------------------------------------|  
|Designer de Relatórios no SQL Server 2014 Data Tools - Business Intelligence para Microsoft Visual Studio 2012, no centro de download da Microsoft.<br /><br /> Ou<br /><br /> Designer de Relatórios no SQL Server 2012 Data Tools - Business Intelligence para Microsoft Visual Studio 2012, no centro de download da Microsoft.<br /><br /> Ou<br /><br /> O Designer de Relatórios no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Data Tools, incluído no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].|Autores 2010 RDL. No código-fonte do RDL existente:<br /><br /> 2000 RDL, atualiza para 2010 RDL<br /><br /> 2005 RDL, atualiza para 2010 RDL<br /><br /> 2008 RDL, atualiza para 2010 RDL|2008 RDL<br /><br /> 2010 RDL|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|Designer de Relatórios no [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] Business Intelligence Development Studio|Autores 2010 RDL. No código-fonte do RDL existente:<br /><br /> 2000 RDL, atualiza para 2010 RDL<br /><br /> 2005 RDL, atualiza para 2010 RDL<br /><br /> 2008 RDL, atualiza para 2010 RDL|2008 RDL<br /><br /> 2010 RDL|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|Designer de Relatórios no [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Business Intelligence Development Studio|Autores 2008 RDL. No código-fonte do RDL existente:<br /><br /> 2000 RDL, atualiza para 2008 RDL<br /><br /> 2005 RDL, atualiza para 2008 RDL|2008 RDL|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|  
|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Construtor de Relatórios|Autores 2010 RDL. No código-fonte do RDL existente:<br /><br /> 2000 RDL, atualiza para 2010 RDL<br /><br /> 2005 RDL, atualiza para 2010 RDL<br /><br /> 2008 RDL, atualiza para 2010 RDL|2010 RDL|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|  
|Designer de Relatórios RDLC do Visual Studio Designer de Relatórios|2005 RDLC|N/D|N/D|  
  
 Para obter mais informações sobre [!INCLUDE[ss_dtbi_vs2013](../includes/ss-dtbi-vs2013-md.md)], consulte o seguinte:  
  
-   [Implantação e suporte de versão no SQL Server Data Tools &#40;SSRS&#41;](tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)  
  
-   [Ferramentas de dados do Microsoft SQL Server - Business Intelligence para Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843).  
  
##  <a name="reportviewer-controls"></a><a name="bkmk_reportviewer"></a>Controles do ReportViewer  
 Um controle [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ReportViewer pode exibir um relatório .rdlc no modo de visualização local ou no modo remoto, o controle pode exibir um arquivo .rdl hospedado em um servidor de relatório [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . A tabela a seguir fornece a lista de versões de RDL com suporte dos controles ReportViewer para processamento local (.rdlc). O suporte para RDL no lado do servidor é resumido na seção [Suporte para servidor de relatório e esquema RDL](#bkmk_report_server_rdl_schema_support).  
  
|Controle ReportViewer no produto|Versão do RDL para a visualização local|  
|-------------------------------------|--------------------------------------|  
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 2013<br /><br /> Ou<br /><br /> [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 2012<br /><br /> Ou<br /><br /> [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]|2008 RDL|  
|[!INCLUDE[vsprvslong](../includes/vsprvslong-md.md)]<br /><br /> Ou<br /><br /> [!INCLUDE[vsOrcas](../includes/vsorcas-md.md)]|2005 RDL|  
  
 Para saber mais, consulte o seguinte:   
  
-   [Convertendo arquivos RDLC em arquivos RDL](https://msdn.microsoft.com/library/ms252109.aspx)  
  
-   [Controles ReportViewer (Visual Studio)](https://msdn.microsoft.com/library/ms251671.aspx)  
  
-   [Adicionando e configurando controles ReportViewer](https://msdn.microsoft.com/library/ms252104.aspx)  
  
## <a name="see-also"></a>Consulte também  
 [Relatórios, relatórios de peças e definições de relatórios &#40;o construtor de relatórios e o SSRS&#41;](report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [Ferramentas de serviços de relatórios](tools/reporting-services-tools.md)   
 [Linguagem RDL &#40;SSRS&#41;](reports/report-definition-language-ssrs.md)  
  
  
