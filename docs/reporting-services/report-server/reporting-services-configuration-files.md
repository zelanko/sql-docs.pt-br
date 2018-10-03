---
title: Arquivos de configuração do Reporting Services | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], configuration files
- configuration options [Reporting Services]
- modifying configuration files
- configuration files [Reporting Services]
ms.assetid: 21e5c32f-ad67-4917-b55a-8e21bd64f5a6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 89adc4f3087a0684ba10089931bd703bd49d28a3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47595584"
---
# <a name="reporting-services-configuration-files"></a>Arquivos de configuração do Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] armazena informações de componente no registro e em arquivos de configuração que são copiados no sistema de arquivos durante a instalação. Os arquivos de configuração contêm uma combinação de valores somente para uso interno e de valores definidos pelo usuário. Os valores definidos pelo usuário são especificados na instalação, com as ferramentas de configuração, os utilitários de linha de comando e a edição manual de arquivos de configuração.  
  
 A modificação dos arquivos de configuração só é necessária se você estiver adicionando ou definindo configurações avançadas. As configurações são especificadas como elementos ou atributos XML. Se você entender de XML e arquivos de configuração, use um editor de texto ou de código para modificar configurações definidas pelo usuário. Para obter mais informações sobre como modificar um arquivo de configuração ou para saber mais sobre como o servidor de relatório lê configurações novas e atualizadas, consulte [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
> [!NOTE]  
>  Em versões anteriores, o Gerenciador de Relatórios tinha seu próprio arquivo de configuração chamado RSWebApplication.config. Esse arquivo está agora obsoleto. Se você tiver atualizado a partir de uma instalação anterior, o arquivo não será excluído, mas o servidor de relatório não lerá nenhuma configuração contida nele. Se o arquivo existir em seu computador, exclua-o. No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores, todas as configurações do Gerenciador de Relatórios são armazenadas e lidas no arquivo RSReportServer.config. Para ver uma lista de quais configurações foram excluídas ou movidas, consulte [Alterações significativas no SQL Server Reporting Services do SQL Server 2016](../../reporting-services/breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md).  
  
 Neste tópico:  
  
-   [Resumo de arquivos de configuração (modo nativo)](#bkmk_config_file_Summary_native_mode)  
  
-   [Resumo de arquivos de configuração (modo do SharePoint)](#bkmk_config_file_Summary_sharepoint_mode)  
  
##  <a name="bkmk_config_file_Summary_native_mode"></a> Resumo de arquivos de configuração (modo nativo)  
 A tabela a seguir descreve onde são armazenadas as configurações. A maioria das configurações é armazenada em arquivos de configuração incluídos no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Por padrão, o diretório de instalação é o seguinte:  
  
```  
C:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER  
```  
  
|Armazenado em:|Descrição|Local|  
|----------------|-----------------|--------------|  
|RSReportServer.config|Armazena configurações para áreas de recurso do serviço Servidor de Relatório: o Gerenciador de Relatórios, o serviço Web do servidor de relatório e o processamento em segundo plano. Para obter mais informações sobre cada configuração, consulte [Arquivo de Configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).|\<Installation directory> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|Armazena as políticas de segurança de acesso a códigos para as extensões de servidor. Para obter mais informações sobre esse arquivo, consulte [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Installation directory> \Reporting Services \ReportServer|  
|RSMgrPolicy.config|Armazena as políticas de segurança de acesso a códigos para o Gerenciador de Relatórios. Para obter mais informações sobre esse arquivo, consulte [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Installation directory> \Reporting Services \ReportManager|  
|Web.config para o serviço Web do servidor de relatório|Inclui somente as configurações obrigatórias para ASP.NET.|\<Installation directory> \Reporting Services \ReportServer|  
|Web.config para o Gerenciador de Relatórios|Inclui somente as configurações obrigatórias para ASP.NET.|\<Installation directory> \Reporting Services \ReportManager|  
|ReportingServicesService.exe.config|Armazena configurações que especificam os níveis de rastreamento e as opções de log para o serviço Servidor de Relatório. Para obter mais informações sobre os elementos desse arquivo, consulte [ReportingServicesService Configuration File](../../reporting-services/report-server/reportingservicesservice-configuration-file.md).|\<Installation directory> \Reporting Services \ReportServer \Bin|  
|Configurações de registro|Armazena o estado de configuração e outras configurações usadas para desinstalar o Reporting Services. Se estiver solucionando um problema de instalação ou configuração, consulte essas configurações para obter informações sobre como o servidor de relatório é configurado.<br /><br /> Não modifique essas configurações diretamente, pois isso pode invalidar sua instalação.|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<InstanceID\> \Setup<br /><br /> **- E -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Services\ReportServer|  
|RSReportDesigner.config|Armazena configurações para o Designer de Relatórios. Para obter mais informações, consulte [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md).|\<drive>:\Program Files \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies.|  
|RSPreviewPolicy.config|Armazena as políticas de segurança de acesso a códigos para as extensões de servidor usadas durante a visualização do relatório. Para obter mais informações sobre esse arquivo, consulte [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|C:\Arquivos de Programas\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssembliesr|  
  
##  <a name="bkmk_config_file_Summary_sharepoint_mode"></a> Resumo de arquivos de configuração (modo do SharePoint)  
 A tabela a seguir fornece uma descrição dos arquivos de configuração usados para um servidor de relatório no modo do SharePoint. A maioria dos parâmetros de configuração é armazenado nos bancos de dados de aplicativo de serviço do SharePoint. Para obter mais informações, consulte [Serviço SharePoint do Reporting Services e aplicativos de serviço](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md).  
  
 Por padrão, o diretório de instalação do modo do SharePoint é o seguinte:  
  
```  
C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting  
```  
  
|Armazenado em:|Descrição|Local|  
|----------------|-----------------|--------------|  
|RSReportServer.config|Armazena configurações para áreas de recurso do serviço Servidor de Relatório: o Gerenciador de Relatórios, o serviço Web do servidor de relatório e o processamento em segundo plano. Para obter mais informações sobre cada configuração, consulte [Arquivo de Configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).|\<Installation directory> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|Armazena as políticas de segurança de acesso a códigos para as extensões de servidor. Para obter mais informações sobre esse arquivo, consulte [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Installation directory> \Reporting Services \ReportServer|  
|Web.config para o serviço Web do servidor de relatório|Inclui somente as configurações obrigatórias para ASP.NET.|\<Installation directory> \Reporting Services \ReportServer|  
|Configurações de registro|Armazena o estado de configuração e outras configurações usadas para desinstalar o Reporting Services. Além disso, armazena informações sobre cada aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .<br /><br /> Não modifique essas configurações diretamente, pois isso pode invalidar sua instalação.|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<InstanceID\> \Setup<br /><br /> ID da instância de exemplo: MSSQL13.MSSQLSERVER<br /><br /> **- E -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Reporting Services\Service Applications|  
|RSReportDesigner.config|Armazena configurações para o Designer de Relatórios. Para obter mais informações, consulte [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md).|\<drive>:\Program Files \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies.|  
  
## <a name="see-also"></a>Consulte Também  
 [Servidor de relatório do Reporting Services &#40;Modo Nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Extensões do Reporting Services](../../reporting-services/extensions/reporting-services-extensions.md)   
 [Utilitário rsconfig &#40;SSRS&#41;](../../reporting-services/tools/rsconfig-utility-ssrs.md)   
 [Iniciar e parar o serviço Servidor de Relatório](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)  
  
  
