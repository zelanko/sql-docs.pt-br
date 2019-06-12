---
title: Arquivos de configuração do Reporting Services | Microsoft Docs
ms.date: 05/30/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], configuration files
- configuration options [Reporting Services]
- modifying configuration files
- configuration files [Reporting Services]
ms.assetid: 21e5c32f-ad67-4917-b55a-8e21bd64f5a6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 25b695456bbac34e2c6ce8bf8c312c4108dd852e
ms.sourcegitcommit: 561cee96844b82ade6cf543a228028ad5c310768
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66506650"
---
# <a name="reporting-services-configuration-files"></a>Arquivos de configuração do Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] armazena informações de componente no registro e em arquivos de configuração que são copiados no sistema de arquivos durante a instalação. Os arquivos de configuração contêm uma combinação de valores somente para uso interno e de valores definidos pelo usuário. Os valores definidos pelo usuário são especificados na instalação, com as ferramentas de configuração, os utilitários de linha de comando e a edição manual de arquivos de configuração.  
  
 A modificação dos arquivos de configuração só é necessária se você estiver adicionando ou definindo configurações avançadas. As configurações são especificadas como elementos ou atributos XML. Se você entender de XML e arquivos de configuração, use um editor de texto ou de código para modificar configurações definidas pelo usuário. Para obter mais informações sobre como modificar um arquivo de configuração ou para saber mais sobre como o servidor de relatório lê configurações novas e atualizadas, consulte [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
> [!NOTE]  
> Em versões anteriores, o Gerenciador de Relatórios tinha seu próprio arquivo de configuração chamado RSWebApplication.config. Esse arquivo está agora obsoleto. Se você tiver atualizado a partir de uma instalação anterior, o arquivo não será excluído, mas o servidor de relatório não lerá nenhuma configuração contida nele. Se o arquivo existir em seu computador, exclua-o. No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores, todas as configurações do Gerenciador de Relatórios são armazenadas e lidas no arquivo RSReportServer.config. Para ver uma lista de quais configurações foram excluídas ou movidas, consulte [Alterações significativas no SQL Server Reporting Services do SQL Server 2016](../../reporting-services/breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md).  
  
 Neste artigo  
  
-   [Resumo de arquivos de configuração (modo nativo)](#bkmk_config_file_Summary_native_mode)  
  
-   [Resumo de arquivos de configuração (modo do SharePoint)](#bkmk_config_file_Summary_sharepoint_mode)  
  
##  <a name="bkmk_config_file_Summary_native_mode"></a> Resumo de arquivos de configuração (modo nativo)  
 A tabela a seguir descreve onde são armazenadas as configurações. A maioria das configurações é armazenada em arquivos de configuração incluídos no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Por padrão, o diretório de instalação é o seguinte:  
  
' ' Instalar caminhos  
C:\Program Files\Microsoft SQL Server\MSRSxx.MSSQLSERVER (onde xx é o número de versão do MS SQL) ou  
C:\Arquivos de Programas\Microsoft SQL Server Reporting Services  
  Dependendo da versão do SSRS
```  
  
|Stored in:|Description|Location|  
|----------------|-----------------|--------------|  
|RSReportServer.config|Stores configuration settings for feature areas of the Report Server service: Report Manager or the web portal, the Report Server Web service, and background processing. For more information about each setting, see [RsReportServer.config Configuration File](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).|\<Installation directory> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|Stores the code access security policies for the server extensions. For more information about this file, see [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Installation directory> \Reporting Services \ReportServer|  
|RSMgrPolicy.config|Stores the code access security policies for the web portal. For more information about this file, see [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Installation directory> \Reporting Services \ReportManager|  
|Web.config for the Report Server Web service|Includes only those settings that are required for ASP.NET.|\<Installation directory> \Reporting Services \ReportServer|  
|Web.config for Report Manager|Includes only those settings that are required for ASP.NET if applicable for the SSRS version.|\<Installation directory> \Reporting Services \ReportManager|  
|ReportingServicesService.exe.config|Stores configuration settings that specify the trace levels and logging options for the Report Server service. For more information about the elements in this file, see [ReportingServicesService Configuration File](../../reporting-services/report-server/reportingservicesservice-configuration-file.md).|\<Installation directory> \Reporting Services \ReportServer \Bin|  
|Registry settings|Stores configuration state and other settings used to uninstall Reporting Services. If you are troubleshooting an installation or configuration problem, you can view these settings to get information about how the report server is configured.<br /><br /> Do not modify these settings directly as this can invalidate your installation.|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<InstanceID\> \Setup<br /><br /> **- And -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Services\ReportServer|  
|RSReportDesigner.config|Stores configuration settings for Report Designer. For more information, see [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md).|\<drive>:\Program Files \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies.|  
|RSPreviewPolicy.config|Stores the code access security policies for the server extensions used during report preview. For more information about this file, see [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|C:\Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssembliesr|  
  
##  <a name="bkmk_config_file_Summary_sharepoint_mode"></a> Summary of configuration Files (SharePoint mode)  
 The following table provides a description of configuration files used for a SharePoint mode report server. Most configuration settings are stored in SharePoint service application databases. For more information, see [Reporting Services SharePoint Service and Service Applications](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md).  
  
 By default, the installation directory for SharePoint mode is the following:  
  
```Install path
C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting  
```  
  
|Armazenado em:|Descrição|Local|  
|----------------|-----------------|--------------|  
|RSReportServer.config|Armazena configurações para áreas de recurso do serviço Servidor de Relatório: o Gerenciador de Relatórios, o serviço Web do servidor de relatório e o processamento em segundo plano. Para obter mais informações sobre cada configuração, consulte [Arquivo de Configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).|\<Installation directory> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|Armazena as políticas de segurança de acesso a códigos para as extensões de servidor. Para obter mais informações sobre esse arquivo, consulte [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Installation directory> \Reporting Services \ReportServer|  
|Web.config para o serviço Web do servidor de relatório|Inclui somente as configurações que são necessárias para o ASP.NET, se aplicável para a versão do SSRS.|\<Installation directory> \Reporting Services \ReportServer|  
|Configurações de registro|Armazena o estado de configuração e outras configurações usadas para desinstalar o Reporting Services. Além disso, armazena informações sobre cada aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .<br /><br /> Não modifique essas configurações diretamente, pois isso pode invalidar sua instalação.|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<InstanceID\> \Setup<br /><br /> ID da instância de exemplo: MSSQL13.MSSQLSERVER<br /><br /> **- E -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Reporting Services\Service Applications|  
|RSReportDesigner.config|Armazena configurações para o Designer de Relatórios. Para obter mais informações, consulte [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md).|\<drive>:\Program Files \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies.|  
  
## <a name="see-also"></a>Confira também  
 [Servidor de relatório do Reporting Services &#40;Modo Nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Extensões do Reporting Services](../../reporting-services/extensions/reporting-services-extensions.md)   
 [Utilitário rsconfig &#40;SSRS&#41;](../../reporting-services/tools/rsconfig-utility-ssrs.md)   
 [Iniciar e parar o serviço Servidor de Relatório](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)  
  
  
