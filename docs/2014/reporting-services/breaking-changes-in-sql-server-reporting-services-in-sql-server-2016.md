---
title: Alterações recentes em SQL Server Reporting Services no SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Me.Value references
- Reporting Services, backward compatibility
- breaking changes [Reporting Services]
ms.assetid: 39c7aafd-dcb9-4317-b8f7-d15828eb4f9a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0d86c9bb07a52aba0cd93b006fc33edf4d1aa885
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109926"
---
# <a name="breaking-changes-in-sql-server-reporting-services-in-sql-server-2014"></a>Alterações recentes no SQL Server Reporting Services do SQL Server 2014
  Este tópico descreve as alterações recentes no [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Essas alterações podem danificar aplicativos, scripts ou funcionalidades baseados em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Você pode encontrar esses problemas durante a atualização ou em scripts ou relatórios personalizados. Para obter mais informações, consulte [Use Upgrade Advisor to Prepare for Upgrades](../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
 **Neste tópico:**  
  
-   [SQL Server 2014 Reporting Services alterações significativas](#bkmk_sql14)  
  
-   [Alterações recentes do SQL Server 2012 Reporting Services](#bkmk_rc0)  
  
-   [Alterações recentes do SQL Server 2008 R2 Reporting Services](#bkmk_kj)  
  
##  <a name="sssql14-reporting-services-breaking-changes"></a><a name="bkmk_sql14"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Reporting Services alterações significativas  
 Não há nenhuma alteração recente do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
##  <a name="sssql11-reporting-services-breaking-changes"></a><a name="bkmk_rc0"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Reporting Services alterações significativas  
  
### <a name="sharepoint-mode-server-references-require-the-sharepoint-site"></a>Referências de servidor de modo do SharePoint exigem o site do SharePoint  
 Você não pode navegar nem referenciar diretamente para o Servidor de relatório usando o nome do diretório virtual no caminho da URL. Por exemplo:  
  
 `http://<Server name>/ReportServer`  
  
 Agora é necessário incluir o site do SharePoint no caminho da URL. Por exemplo, se o nome do seu site`videos`for ' ' e usado`sites`o prefixo ' ', a URL será semelhante ao seguinte:  
  
 `http://<Server Name>/sites/videos/_vti_bin/ReportServer`  
  
### <a name="changes-to-sharepoint-mode-command-line-installation"></a>Alterações na instalação de linha de comando de modo do SharePoint  
 A configuração de entrada **/RSINSTALLMODE** funciona apenas com instalações de modo nativo e não funciona para instalações de modo do SharePoint. Por exemplo, não há suporte para o seguinte [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]em: **/RSINSTALLMODE = "DefaultSharePointMode"**. Em vez desta configuração de entrada, use **/RSSHPINSTALLMODE = "DefaultSharePointMode**."  
  
 A instrução a seguir é um exemplo de um comando de instalação completo e conjunto de parâmetros: **Setup/Action = Install/Features = SQL, RS/InstanceName = Denali_INST1..../RSSHPINSTALLMODE = "DefaultSharePointMode"**  
  
 Para obter mais informações sobre instalações de linha de comando, consulte [instalação de prompt de comando do modo do Reporting Services SharePoint e modo nativo](install-windows/install-reporting-services-at-the-command-prompt.md).  
  
### <a name="the-reporting-services-wmi-provider-no-longer-supports-configuration-of-sharepoint-mode"></a>O provedor WMI do Reporting Services não dá mais suporte à configuração do modo do SharePoint.  
 A configuração do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint agora é concluída usando cmdlets do PowerShell e a Administração Central do SharePoint. A nova arquitetura de modo SharePoint do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] utiliza a arquitetura de serviços SharePoint. O SharePoint não oferece suporte a interfaces WMI.  
  
 Essas alterações afetam a seguinte lista de componentes e fluxos de trabalho:  
  
-   Aplicativos personalizados que usam o provedor WMI [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] em modo do SharePoint.  
  
-   O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Configuration Manager, rskeymgmt.exe e rsconfig.exe. Em vez de usar esses utilitários para configuração de modo do SharePoint [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , use a Administração Central do SharePoint e o PowerShell.  
  
-   SQL Server Management Studio: os clientes não podem fazer referência a um servidor com sintaxe semelhante a <machine_name>/<instance_name>. A partir da versão [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] , o método recomendado era usar uma URL do site do SharePoint. Por exemplo, **http://<sharepoint_server>/<** sharePoint_site>. A partir do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], uma URL do site do SharePoint é a única sintaxe com suporte.  
  
### <a name="report-model-designer-is-not-available-in-sql-server-data-tools"></a>O Designer de Modelo de Relatório não está disponível no SQL Server Data Tools  
 O [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] não dá mais suporte a projetos de modelo de relatório. O designer do Modelo de Relatório não está disponível no [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]. Não é possível criar novos projetos de modelo de relatório nem abrir projetos existentes no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e não é possível criar nem atualizar modelos de relatório. Para atualizar modelos de relatório, você pode usar o [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ou ferramentas anteriores. Você pode continuar a usar modelos de relatório como fontes de dados em relatórios criados em ferramentas do [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] , como o Construtor de Relatórios e o Designer de Relatórios. O designer de consulta que você usa para criar consultas para extrair dados de relatório de modelos de relatório continua disponível no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
##  <a name="sql-server-2008-r2-reporting-services-breaking-changes"></a><a name="bkmk_kj"></a>SQL Server 2008 R2 Reporting Services alterações significativas  
 Esta seção descreve as alterações significativas [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]no.  
  
> [!NOTE]  
>  Como o SQL Server 2008 R2 é uma atualização de versão secundária do SQL Server 2008, recomendamos que você também revise o conteúdo na seção do SQL Server 2008.  
  
### <a name="expanded-csv-data-renderer"></a>Processador de dados CSV expandido  
 No [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], o arquivo CSV inclui dados de gráfico e de medidor. Os aplicativos que dependem de uma estrutura de arquivos CSV prévia não funcionarão mais por causa das inclusões das colunas adicionais para gráficos e medidores.  
  
 Para obter mais informações, consulte [Exportar para um arquivo CSV &#40;Construtor de Relatórios e SSRS&#41;](report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Alterações de comportamento para SQL Server Reporting Services no SQL Server 2014](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [O que há de novo &#40;Reporting Services&#41;](what-s-new-reporting-services.md)   
 [Recursos preteridos do SQL Server Reporting Services no SQL Server 2014](deprecated-features-in-sql-server-reporting-services-ssrs.md)   
 [Funcionalidade descontinuada do SQL Server Reporting Services no SQL Server 2014](discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)  
  
  
