---
title: Fontes e arquivos de log do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- troubleshooting [Reporting Services], log files
- logs [Reporting Services]
- logs [Reporting Services], about log files
- report servers [Reporting Services], log files
- report server log files
- files [Reporting Services], logs
ms.assetid: 80ef0acc-cbef-49d0-87e7-844e3ce19604
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: c355a6ecdecc5ad17dbdba788e736dfaf701d099
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56021537"
---
# <a name="reporting-services-log-files-and-sources"></a>Fontes e arquivos de log do Reporting Services
  Um servidor de relatório [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e um ambiente de servidor de relatório dão suporte a uma variedade de destinos de log para registrar informações sobre operações e status do servidor. Há duas categorias básicas de registro em log, log de execução e log de rastreamento. O log de execução inclui informações sobre estatística de execução de relatório, auditoria, diagnóstico de desempenho e otimização. O log de rastreamento são informações sobre mensagens de erro e diagnóstico em geral.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] | Modo nativo do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]   
  
 A tabela a seguir fornece links para informações adicionais sobre cada log, incluindo o local e como exibir seu conteúdo.  
  
|Log|Descrição|  
|---------|-----------------|  
|[Log de execução do servidor de relatório e a exibição ExecutionLog3](report-server-executionlog-and-the-executionlog3-view.md)|O log de execução é um modo de exibição do SQL Server armazenado no banco de dados do servidor de relatório.<br /><br /> O log de execução do servidor de relatório contém dados sobre relatórios específicos, incluindo quando o relatório foi executado, quem o executou, quando foi entregue e qual formato de renderização foi usado.|  
|Log de rastreamento do SharePoint|Para servidores de relatório executados no SharePoint, os logs de rastreamento do SharePoint contêm informações do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] . Você também pode configurar as informações específicas do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] para o serviço de log unificado do SharePoint. Para obter mais informações, consulte [Ativar eventos do Reporting Services para o log de rastreamento do SharePoint &#40;ULS&#41;](turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md)|  
|[Log de rastreamento do serviço Servidor de Relatório](report-server-service-trace-log.md)|O log de rastreamento de serviço contém informações bem detalhadas que são úteis se você estiver depurando um aplicativo ou investigando um problema ou evento.<br /><br /> `C:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\LogFiles`|  
|[Log HTTP do Servidor de Relatório](report-server-http-log.md)|O arquivo de log HTTP contém um registro de todas as solicitações e respostas HTTP manipuladas pelo serviço Web do servidor de relatório e pelo Gerenciador de Relatórios.|  
|[Log de aplicativo do Windows](windows-application-log.md)|O log de aplicativos de Microsoft Windows contém informações sobre eventos de servidor de relatório.|  
|Logs de desempenho do Windows|Os logs de desempenho do Windows contêm dados de desempenho do servidor de relatório. Você pode criar logs de desempenho e escolher contadores que determinam quais dados devem ser coletados. Para obter mais informações, consulte [Monitoring Report Server Performance](monitoring-report-server-performance.md).|  
|Arquivos de log de instalação|Arquivos de log também são criados durante a instalação. Se a instalação falhar ou for bem-sucedida com avisos ou outras mensagens, você poderá examinar os arquivos de log para solucionar o problema. Para obter mais informações, consulte [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).|  
|Logs de IIS|Arquivos de log criados por Serviços de Informações da Internet da Microsoft (IIS). Para obter mais informações, consulte [Como habilitar o log em Serviços de Informações da Internet (IIS)](https://support.microsoft.com/kb/313437).|  
|Vídeo|Exibir um breve vídeo que demonstra o uso do Microsoft Power Query para exibir arquivos de log [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] .<br /><br /> ![Exibir um vídeo sobre logs de SSRS e Power Query](../media/generic-video-thumbnail.png "exibir um vídeo sobre logs de SSRS e Power Query")|  
  
## <a name="see-also"></a>Consulte também  
 [Servidor de relatório do Reporting Services &#40;Modo Nativo&#41;](reporting-services-report-server-native-mode.md)   
 [Referência de erros e eventos &#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
