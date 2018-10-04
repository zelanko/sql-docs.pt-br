---
title: Monitorando o desempenho do servidor de relatório | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
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
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 0379e0105522caf643d2295070da395df51a41a3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48112846"
---
# <a name="monitoring-report-server-performance"></a>Monitorando o desempenho do servidor de relatório
  Use as ferramentas de monitoramento de desempenho para monitorar o desempenho do servidor de relatório e avaliar a atividade do servidor, observar as tendências, diagnosticar gargalos do sistema e reunir dados que podem ajudar a determinar se a configuração atual do sistema é suficiente. Para ajustar o desempenho do servidor, você pode especificar com que frequência o domínio de aplicativo de servidor de relatório deve ser reciclado. Para obter mais informações, consulte [Configurar memória disponível para aplicativos do Servidor de Relatório](../report-server/configure-available-memory-for-report-server-applications.md).  
  
## <a name="sources-of-performance-data"></a>Fontes de dados de desempenho  
 Use uma combinação de tecnologias e ferramentas para obter informações abrangentes sobre como o sistema está funcionando. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Server fornecem informações sobre o desempenho através das seguintes ferramentas:  
  
-   Gerenciador de Tarefas  
  
-   Visualizador de Eventos  
  
-   Console de Desempenho  
  
 O Gerenciador de Tarefas fornece informações sobre programas e processos em execução no computador. Você pode usar o Gerenciador de Tarefas para monitorar os principais indicadores de desempenho do servidor de relatório. Você também pode avaliar a atividade dos processos de execução e exibir gráficos e dados sobre a CPU e o uso de memória. Para obter informações sobre como usar o Gerenciador de Tarefas, consulte a documentação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 Você pode usar o Console de Desempenho e o Visualizador de Eventos para criar logs e alertas sobre processamento de relatórios e consumo de recursos. Para obter informações sobre eventos do Windows que são gerados pelo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [Log de aplicativo do Windows](windows-application-log.md). Para obter informações sobre o Console de Desempenho, consulte “Contadores de Desempenho do Windows”, mais adiante neste tópico.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também fornecem informações sobre o banco de dados de servidor de relatório e bancos de dados temporários usados para cache e gerenciamento de sessão.  
  
## <a name="windows-performance-counters"></a>Contadores de desempenho do Windows  
 O monitoramento de contadores de desempenho específicos permitem:  
  
-   Estimar os requisitos de sistema necessários para dar suporte a uma carga de trabalho prevista.  
  
-   Criar uma linha de base de desempenho para medir o efeito das alterações de configuração ou atualizações de aplicativo.  
  
-   Monitorar o desempenho do aplicativo sob certas cargas, geradas real ou artificialmente.  
  
-   Verificar se as atualizações de hardware têm o efeito desejado em relação ao desempenho.  
  
-   Validar alterações que foram feitas na configuração do sistema para ter o efeito desejado de desempenho.  
  
## <a name="reporting-services-performance-objects"></a>Objetos de Desempenho do Reporting Services  
 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] contém os seguintes objetos de desempenho:  
  
-   **Serviço Web MSRS 2011** e `MSRS 2011 SharePoint Mode Web Service` para monitorar o desempenho do servidor de relatório. Esses objetos de desempenho incluem uma coleção de contadores usados para controlar o processamento do servidor de relatório iniciado normalmente por meio de operações interativas de exibição de relatórios. Esses contadores são redefinidos sempre que o [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] interrompe o serviço Web Servidor de Relatórios.  
  
-   `MSRS 2011 Windows Service` e `MSRS 2011 Windows Service SharePoint Mode` para monitorar as operações agendadas e a entrega do relatório. Esses objetos de desempenho incluem uma coleção de contadores usados para controlar o processamento de relatórios que é iniciado por meio de operações agendadas. As operações agendadas incluem assinatura e entrega, instantâneos de execução de relatório e histórico de relatório.  
  
-   `ReportServer:Service` e `ReportServerSharePoint:Service` para monitorar eventos relacionados ao HTTP e gerenciamento de memória. Esses contadores são específicos ao [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]e controlam eventos relacionados ao HTTP para o servidor de relatório, como solicitações, conexões e tentativas de logon. Esse objeto de desempenho também inclui contadores relacionados a gerenciamento de memória.  
  
 Se você tiver várias instâncias de servidor de relatório em um único computador, poderá monitorar as instâncias juntas ou separadamente. Escolha quais instâncias devem ser incluídas ao adicionar um contador. Para obter mais informações sobre como usar o Console de Desempenho (perfmon.msc) e adicionar contadores, consulte a documentação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
## <a name="other-performance-counters"></a>Outros Contadores de Desempenho  
 Contadores de desempenho personalizados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] são fornecidos somente para `MSRS 2008 Web Service`, `MSRS 2008 Windows Service` e `ReportServer:Service`. Os objetos de desempenho a seguir fornecem monitoramento de desempenho adicional para o servidor de relatório.  
  
|Objeto de desempenho|Observações|  
|------------------------|-----------|  
|`.NET CLR Data` e `.NET CLR Memory`|O Gerenciador de Relatórios usa contadores de desempenho [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] . Para obter mais informações, consulte “Melhorando o desempenho e a escalabilidade do aplicativo .NET” no MSDN.|  
|`Process`|Adicione os contadores de desempenho  `Elapsed Time` e `ID Process` para uma instância de ReportingServicesService a fim de controlar o tempo de atividade de processo por ID de processo.|  
  
## <a name="sharepoint-events"></a>Eventos do SharePoint  
 Além dos objetos de desempenho do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , você também poderá configurar eventos do SharePoint se estiver executando um servidor de relatório no modo integrado do SharePoint e tiver configurado o ambiente de relatórios para usar um produto do SharePoint. Nesta seção, use os Eventos de um servidor de relatório no modo integrado do SharePoint para revisar eventos de diagnóstico que podem fornecer informações úteis, se seu ambiente de relatórios estiver integrado com o SharePoint.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Contadores de desempenho para o MSRS 2014 Web Service e objetos de desempenho do MSRS 2014 Windows Service &#40;modo nativo&#41;](performance-counters-msrs-2011-web-service-performance-objects.md)  
 Descreve os contadores de desempenho usados pelo serviço Web Servidor de Relatórios.  
  
 [Contadores de desempenho para o modo do SharePoint do MSRS 2014 Web Service e objetos de desempenho do MSRS 2014 Windows Service SharePoint modo &#40;modo do SharePoint&#41;](performance-counters-msrs-2011-sharepoint-mode-performance-objects.md)  
 Descreve os contadores de desempenho usados pelo serviço do Windows Servidor de Relatório.  
  
 [Contadores de desempenho para os objetos de desempenho ReportServer:Service e ReportServerSharePoint:Service](performance-counters-reportserver-service-performance-objects.md)  
 Descreve os contadores de desempenho relacionados a memória e ao HTTP no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Eventos de um servidor de relatório no modo integrado do SharePoint  
 Descreve os eventos de diagnóstico úteis a serem registrados quando você executar um ambiente de relatórios com um produto do SharePoint.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar memória disponível para aplicativos do Servidor de Relatório](../report-server/configure-available-memory-for-report-server-applications.md)   
 [Servidor de relatório do Reporting Services &#40;Modo Nativo&#41;](reporting-services-report-server-native-mode.md)   
 [Ferramentas do Reporting Services](../tools/reporting-services-tools.md)  
  
  
