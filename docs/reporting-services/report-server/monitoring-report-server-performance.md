---
title: Monitorando o desempenho do servidor de relatório | Microsoft Docs
ms.date: 06/20/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- performance counters [Reporting Services]
- report servers [Reporting Services], performance
- counters [Reporting Services]
- monitoring performance [Reporting Services]
- SQL Server Reporting Services, performance
- performance [Reporting Services]
- Reporting Services, performance
ms.assetid: c1bc13d4-8297-4daf-bb19-4c1e5ba292a6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5d277089fded73524e55d05bbc21078d5df426e3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67412652"
---
# <a name="monitoring-report-server-performance"></a>Monitorando o desempenho do servidor de relatório
  Use as ferramentas de monitoramento de desempenho para monitorar o desempenho do servidor de relatório e avaliar a atividade do servidor, observar as tendências, diagnosticar gargalos do sistema e reunir dados que podem ajudar a determinar se a configuração atual do sistema é suficiente. Para ajustar o desempenho do servidor, você pode especificar com que frequência o domínio de aplicativo de servidor de relatório deve ser reciclado. Para obter mais informações, consulte [Configurar memória disponível para aplicativos do Servidor de Relatório](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md).  
  
## <a name="sources-of-performance-data"></a>Fontes de dados de desempenho  
 Use uma combinação de tecnologias e ferramentas para obter informações abrangentes sobre como o sistema está funcionando. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Server fornecem informações sobre o desempenho através das seguintes ferramentas:  
  
-   Gerenciador de Tarefas  
  
-   Visualizador de Eventos  
  
-   Console de Desempenho  
  
 O Gerenciador de Tarefas fornece informações sobre programas e processos em execução no computador. Você pode usar o Gerenciador de Tarefas para monitorar os principais indicadores de desempenho do servidor de relatório. Você também pode avaliar a atividade dos processos de execução e exibir gráficos e dados sobre a CPU e o uso de memória. Para obter informações sobre como usar o Gerenciador de Tarefas, consulte a documentação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 Você pode usar o Console de Desempenho e o Visualizador de Eventos para criar logs e alertas sobre processamento de relatórios e consumo de recursos. Para obter informações sobre eventos do Windows que são gerados pelo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [Log de Aplicativos do Windows](../../reporting-services/report-server/windows-application-log.md). Para obter informações sobre o Console de Desempenho, consulte "Contadores de Desempenho do Windows", mais adiante neste artigo.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também fornecem informações sobre o banco de dados de servidor de relatório e bancos de dados temporários usados para cache e gerenciamento de sessão.  
  
## <a name="windows-performance-counters"></a>Contadores de desempenho do Windows  
 O monitoramento de contadores de desempenho específicos permitem:  
  
-   Estimar os requisitos de sistema necessários para dar suporte a uma carga de trabalho prevista.  
  
-   Criar uma linha de base de desempenho para medir o efeito das alterações de configuração ou atualizações de aplicativo.  
  
-   Monitorar o desempenho do aplicativo sob certas cargas, geradas real ou artificialmente.  
  
-   Verificar se as atualizações de hardware têm o efeito desejado em relação ao desempenho.  
  
-   Validar alterações que foram feitas na configuração do sistema para ter o efeito desejado de desempenho.  

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
  
## <a name="reporting-services-performance-objects"></a>Objetos de desempenho do Reporting Services  
SSRS (SQL Server 2016 Reporting Services) ou posterior inclui os seguintes objetos de desempenho:  
  
-   **MSRS 2011 Web Service** e **MSRS 2011 SharePoint Mode Web Service** para monitorar o desempenho do servidor de relatório. Esses objetos de desempenho incluem uma coleção de contadores usados para controlar o processamento do servidor de relatório iniciado normalmente por meio de operações interativas de exibição de relatórios. Esses contadores são redefinidos sempre que o [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] interrompe o serviço Web Servidor de Relatórios.  
  
-   **MSRS 2011 Windows Service** e **MSRS 2011 Windows Service SharePoint Mode** para monitorar as operações agendadas e a entrega do relatório. Esses objetos de desempenho incluem uma coleção de contadores usados para controlar o processamento de relatórios que é iniciado por meio de operações agendadas. As operações agendadas incluem assinatura e entrega, instantâneos de execução de relatório e histórico de relatório.  
  
-   **ReportServer Service** e **ReportServerSharePoint Service** monitoram eventos relacionados ao HTTP e gerenciamento de memória. Esses contadores são específicos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e controlam eventos relacionados ao HTTP para o servidor de relatório, como solicitações, conexões e tentativas de entrada. Esse objeto de desempenho também inclui contadores relacionados a gerenciamento de memória.  
  
 Se você tiver várias instâncias de servidor de relatório em um único computador, poderá monitorar as instâncias juntas ou separadamente. Escolha quais instâncias devem ser incluídas ao adicionar um contador. Para obter mais informações sobre como usar o Console de Desempenho (perfmon.msc) e adicionar contadores, consulte a documentação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
## <a name="other-performance-counters"></a>Outros contadores de desempenho  
 Contadores de desempenho personalizados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] são fornecidos apenas para **Serviço Web do MSRS 2008**, **Serviço Windows do MSRS 2008** e **ReportServer Service**. Os objetos de desempenho a seguir fornecem monitoramento de desempenho adicional para o servidor de relatório.  
  
|Objeto de desempenho|Observações|  
|------------------------|-----------|  
|**.NET CLR Data** e **.NET CLR Memory**|O portal da Web usa contadores de desempenho [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]. Para obter mais informações, consulte “Melhorando o desempenho e a escalabilidade do aplicativo .NET” no MSDN.|  
|**Processo**|Adicione os contadores de desempenho **Elapsed Time** e **ID Process** para uma instância de ReportingServicesService a fim de controlar o tempo de atividade de processo por ID de processo.|  
  
## <a name="sharepoint-events"></a>Eventos do SharePoint  
 Além dos objetos de desempenho do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , você também poderá configurar eventos do SharePoint se estiver executando um servidor de relatório no modo integrado do SharePoint e tiver configurado o ambiente de relatórios para usar um produto do SharePoint. Nesta seção, use os Eventos de um servidor de relatório no modo integrado do SharePoint para revisar eventos de diagnóstico que podem fornecer informações úteis, se seu ambiente de relatórios estiver integrado com o SharePoint.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Contadores de desempenho do serviço Web MSRS 2011 e objetos de desempenho do serviço Windows MSRS 2011 &#40;modo nativo&#41;](../../reporting-services/report-server/performance-counters-msrs-2011-web-service-performance-objects.md)  
 Descreve os contadores de desempenho usados pelo serviço Web Servidor de Relatórios.  
  
 [Contadores de desempenho do modo do SharePoint do serviço Web MSRS 2011 e objetos de desempenho do modo do SharePoint do serviço Windows MSRS 2011 &#40;modo do SharePoint&#41;](../../reporting-services/report-server/performance-counters-msrs-2011-sharepoint-mode-performance-objects.md)  
 Descreve os contadores de desempenho usados pelo serviço do Windows Servidor de Relatório.  
  
 [Contadores de desempenho para os objetos de desempenho ReportServer:Service e ReportServerSharePoint:Service](../../reporting-services/report-server/performance-counters-reportserver-service-performance-objects.md)  
 Descreve os contadores de desempenho relacionados a memória e ao HTTP no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  

::: moniker-end
  
## <a name="see-also"></a>Confira também  
 [Configurar memória disponível para aplicativos do Servidor de Relatório](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)   
 [Servidor de relatório do Reporting Services &#40;Modo Nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Ferramentas do Reporting Services](../../reporting-services/tools/reporting-services-tools.md)  
  