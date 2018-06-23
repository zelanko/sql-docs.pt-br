---
title: Alterações recentes no SQL Server Reporting Services no SQL Server 2014 | Microsoft Docs
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
- Me.Value references
- Reporting Services, backward compatibility
- breaking changes [Reporting Services]
ms.assetid: 39c7aafd-dcb9-4317-b8f7-d15828eb4f9a
caps.latest.revision: 111
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: b6aef4ad0256779c355a98467df5f6425b69444a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009296"
---
# <a name="breaking-changes-in-sql-server-reporting-services-in-sql-server-2014"></a>Alterações recentes no SQL Server Reporting Services do SQL Server 2014
  Este tópico descreve as alterações recentes no [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Essas alterações podem danificar aplicativos, scripts ou funcionalidades baseados em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Você pode encontrar esses problemas durante a atualização ou em scripts ou relatórios personalizados. Para obter mais informações, consulte [Use Upgrade Advisor to Prepare for Upgrades](../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
 **Neste tópico:**  
  
-   [Alterações recentes SQL Server 2014 Reporting Services](#bkmk_sql14)  
  
-   [Alterações recentes SQL Server 2012 Reporting Services](#bkmk_rc0)  
  
-   [Alterações recentes SQL Server 2008 R2 Reporting Services](#bkmk_kj)  
  
##  <a name="bkmk_sql14"></a> [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] O Reporting Services, alterações recentes  
 Não há nenhum [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] alterações recentes no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
##  <a name="bkmk_rc0"></a> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] O Reporting Services, alterações recentes  
  
### <a name="sharepoint-mode-server-references-require-the-sharepoint-site"></a>Referências de servidor de modo do SharePoint exigem o site do SharePoint  
 Você não pode navegar nem referenciar diretamente para o Servidor de relatório usando o nome do diretório virtual no caminho da URL. Por exemplo:  
  
 `http://<Server name>/ReportServer`  
  
 Agora é necessário incluir o site do SharePoint no caminho da URL. Por exemplo, se seu nome de site for '`videos`' e você tiver usado o prefixo '`sites`', a URL seria semelhante ao seguinte:  
  
 `http://<Server Name>/sites/videos/_vti_bin/ReportServer`  
  
### <a name="changes-to-sharepoint-mode-command-line-installation"></a>Alterações na instalação de linha de comando de modo do SharePoint  
 A configuração de entrada **/RSINSTALLMODE** funciona apenas com instalações de modo nativo e não funciona para instalações de modo do SharePoint. Por exemplo, o seguinte não é suportado em [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]: **/RSINSTALLMODE = "DefaultSharePointMode"**. Em vez desta configuração de entrada, use **/RSSHPINSTALLMODE = "DefaultSharePointMode**."  
  
 A instrução a seguir é um exemplo de um comando de instalação completo e do conjunto de parâmetros: **setup /ACTION=install /FEATURES=SQL,RS /InstanceName=Denali_INST1 …. /RSSHPINSTALLMODE="DefaultSharePointMode"**  
  
 Para obter mais informações sobre instalações de linha de comando, consulte [Prompt de comando instalação do Reporting Services modo do SharePoint e modo nativo](install-windows/install-reporting-services-at-the-command-prompt.md).  
  
### <a name="the-reporting-services-wmi-provider-no-longer-supports-configuration-of-sharepoint-mode"></a>O provedor WMI do Reporting Services não dá mais suporte à configuração do modo do SharePoint.  
 A configuração do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint agora é concluída usando cmdlets do PowerShell e a Administração Central do SharePoint. A nova arquitetura de modo SharePoint do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] utiliza a arquitetura de serviços SharePoint. O SharePoint não oferece suporte a interfaces WMI.  
  
 Essas alterações afetam a seguinte lista de componentes e fluxos de trabalho:  
  
-   Aplicativos personalizados que usam o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] provedor WMI para [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no modo do SharePoint.  
  
-   O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Configuration Manager, rskeymgmt.exe e rsconfig.exe. Em vez de usar esses utilitários para configuração de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] modo do SharePoint, use a Administração Central do SharePoint e do PowerShell.  
  
-   SQL Server Management Studio: Clientes não podem referenciar um servidor com sintaxe semelhante a <machine_name>/<instance_name>. A partir da versão [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], o método recomendado era usar uma URL do site do SharePoint. Por exemplo, **http://<SHAREPOINT_SERVER>/<sharePoint_site&gt**. Começando com [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], uma URL do site do SharePoint é a única sintaxe com suporte.  
  
### <a name="report-model-designer-is-not-available-in-sql-server-data-tools"></a>O Designer de Modelo de Relatório não está disponível no SQL Server Data Tools  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] não dá suporte a projetos de modelo de relatório. O designer do Modelo de Relatório não está disponível no [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]. Você não pode criar novos projetos de modelo de relatório ou abrir projetos existentes no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e você não pode criar ou atualizar modelos de relatório. Para atualizar modelos de relatório, você pode usar [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ou ferramentas anteriores. Você pode continuar a usar modelos de relatório como fontes de dados em relatórios criados em ferramentas do [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)], como o Construtor de Relatórios e o Designer de Relatórios. O designer de consulta que você usa para criar consultas para extrair dados de relatório de modelos de relatório continua disponível no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
##  <a name="bkmk_kj"></a> Alterações recentes SQL Server 2008 R2 Reporting Services  
 Esta seção descreve as alterações recentes no [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
> [!NOTE]  
>  Como o SQL Server 2008 R2 é uma atualização de versão secundária do SQL Server 2008, recomendamos que você também revise o conteúdo na seção do SQL Server 2008.  
  
### <a name="expanded-csv-data-renderer"></a>Processador de dados CSV expandido  
 Em [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], o arquivo CSV inclui dados de gráfico e medidor. Os aplicativos que dependem de uma estrutura de arquivos CSV prévia não funcionarão mais por causa das inclusões das colunas adicionais para gráficos e medidores.  
  
 Para obter mais informações, consulte [Exporting to a CSV File &#40;Report Builder and SSRS&#41;](report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Alterações de comportamento no SQL Server Reporting Services no SQL Server 2014](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [O que há de novo &#40;Reporting Services&#41;](what-s-new-reporting-services.md)   
 [Recursos preteridos no SQL Server Reporting Services no SQL Server 2014](deprecated-features-in-sql-server-reporting-services-ssrs.md)   
 [Funcionalidade descontinuada do SQL Server Reporting Services no SQL Server 2014](discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)  
  
  