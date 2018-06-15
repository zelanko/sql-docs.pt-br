---
title: Contadores de desempenho para os objetos de desempenho do serviço Web do MSRS 2011 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- performance counters [Reporting Services]
- Report Server Web service, performance counters
- Reporting Services performance object
- RS Web Service performance object
- counters [Reporting Services]
- performance [Reporting Services]
ms.assetid: c642fc4f-8734-4626-a194-42ac9cd8e2ef
caps.latest.revision: 50
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 8851d1c5deac3b759452ec23115cb70dd3cf31f4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33028163"
---
# <a name="performance-counters-msrs-2011-web-service-performance-objects"></a>Contadores de desempenho para os objetos de desempenho do serviço Web do MSRS 2011
  Este tópico descreve contadores de desempenho para os objetos de desempenho do **Serviço Web MSRS 2011** e do **Serviço do Windows MSRS 2011** . Esses objetos fazem parte de uma implantação do Modo Nativo do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] .  
  
> [!NOTE]  
>  Esses objetos de desempenho monitoram eventos no servidor de relatório local. Se você estiver executando um servidor de relatório em uma implantação em expansão, as contagens aplicam-se ao servidor atual e não à implantação em expansão.  
  
 Os objetos de desempenho estão disponíveis no Monitor de Desempenho do Windows (**Perfmon.exe**). Para saber mais, veja a documentação do Windows, [Criação de perfil em tempo de execução](http://msdn.microsoft.com/library/w4bz2147.aspx) (http://msdn.microsoft.com/library/w4bz2147.aspx).  
  
 Para obter mais informações relacionadas aos contadores de desempenho de modo do SharePoint, consulte [Contadores de desempenho do modo do SharePoint do serviço Web MSRS 2011 e objetos de desempenho do modo do SharePoint do serviço Windows MSRS 2011 &#40;modo do SharePoint&#41;](../../reporting-services/report-server/performance-counters-msrs-2011-sharepoint-mode-performance-objects.md).  
  
 Neste tópico:  
  
-   [Contadores de desempenho do Serviço Web MSRS 2011](#bkmk_webservice)  
  
-   [Contadores de Desempenho do Serviço Windows MSRS 2011](#bkmk_windowsservice)  
  
-   [Use cmdlets do PowerShell para retornar listas](#bkmk_powershell)  
  
##  <a name="bkmk_webservice"></a> Contadores de desempenho do Serviço Web MSRS 2011  
 O objeto de desempenho do **Serviço Web MSRS 2011** monitora o desempenho do servidor de relatório. Esse objeto de desempenho inclui uma coleção de contadores usados para controlar o processamento do servidor de relatório iniciado normalmente por operações interativas de exibição de relatórios. Quando você configura este contador, pode aplicá-lo a todas as instâncias de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou selecionar instâncias específicas. Esses contadores são redefinidos sempre que o [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] interrompe o serviço Web servidor de relatórios.  
  
 A tabela a seguir lista os contadores que são incluídos com o objeto de desempenho do **Serviço Web MSRS 2011** .  
  
|Contador|Description|  
|-------------|-----------------|  
|**Sessões ativas**|Número de sessões ativas. Este contador fornece uma contagem cumulativa de todas as sessões de navegador geradas a partir de execuções de relatórios, independentemente de estarem ativas ou não.<br /><br /> O contador é reduzido à medida que os registros de sessão são removidos. Por padrão, as sessões são removidas após dez minutos de inatividade.|  
|**Acertos de cache/s**|Número de solicitações por segundo para relatórios armazenados em cache. As solicitações são para relatórios re-renderizados e não solicitações para relatórios processados diretamente do cache. (Consulte **Total de acertos de cache** mais adiante neste tópico.)|  
|**Acertos do cache/s (modelos semânticos)**|Número de solicitações por segundo para modelos armazenados em cache. As solicitações para relatórios re-renderizados e não solicitações para relatórios processados diretamente do cache.|  
|**Erros de cache/s**|Número de solicitações por segundo que não retornaram um relatório de cache. Use este contador para descobrir se os recursos usados para armazenamento em cache (disco ou memória) são suficientes.|  
|**Erros do cache/s (modelos semânticos)**|Número de solicitações por segundo que não retornaram um modelo de cache. Use este contador para descobrir se os recursos usados para armazenamento em cache (disco ou memória) são suficientes.|  
|**Solicitações/s da primeira sessão**|Número de sessões de usuário novas que são iniciadas no cache de servidor de relatório a cada segundo.|  
|**Acertos de cache de memória/s**|Número de vezes por segundo que os relatórios são recuperados do cache na memória. *Cache na memória* é uma parte do cache que armazena relatórios na memória da CPU. Quando o cache na memória é usado, o servidor de relatório não consulta o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para obter o conteúdo armazenado em cache.|  
|**Erros de cache de memória/s**|Número de vezes por segundo que os relatórios não puderam ser recuperados do cache na memória.|  
|**Solicitações/s da próxima sessão**|Número de solicitações por segundo para relatórios que estão abertos em uma sessão já existente (por exemplo, relatórios que são renderizados de um instantâneo de sessão).|  
|**Solicitações de relatório**|Número de relatórios que estão ativos no momento e gerenciados pelo servidor de relatório.|  
|**Relatórios executados/s**|Número de execuções de relatório bem-sucedidas por segundo. Este contador fornece estatísticas sobre volume de relatório. Use este contador com **Solicitações/s** para comparar a execução de relatórios com solicitações de relatórios que podem ser retornadas do cache.|  
|**Solicitações/s**|Número de solicitações por segundo feitas ao servidor de relatório. Este contador controla todos os tipos de solicitações que são gerenciadas pelo servidor de relatório.|  
|**Total de acertos de cache**|Número total de solicitações de relatórios do cache depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios.|  
|**Total de acertos do cache (modelos semânticos)**|Número total de solicitações de modelos do cache depois que o serviço foi iniciado. Este contador é zerado sempre que ASP.NET para o serviço Web Servidor de Relatórios.|  
|**Total de erros do cache**|Número total de vezes que um relatório não pôde ser retornado do cache depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios. Use este contador para determinar se espaço em disco e memória são suficientes.|  
|**Total de erros do cache (modelos semânticos)**|Número total de vezes que um modelo não pôde ser retornado do cache depois que o serviço foi iniciado. Este contador é zerado sempre que ASP.NET para o serviço Web Servidor de Relatórios. Use este contador para determinar se espaço em disco e memória são suficientes.|  
|**Total de acertos do cache de memória**|Número total de relatórios armazenados em cache retornados do cache na memória depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios. *Cache na memória* é uma parte do cache que armazena relatórios na memória da CPU. Quando o cache na memória é usado, o servidor de relatório não consulta o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para obter o conteúdo armazenado em cache.|  
|**Total de erros do cache de memória**|Número total de erros de cache na memória depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios.|  
|**Total de falhas de processamento**|O número de erros de processamento de solicitação para o serviço Web Servidor de Relatórios.|  
|**Total de threads rejeitados**|Número total de threads rejeitados para processamento assíncrono e, posteriormente, tratados como processos síncronos no mesmo thread. Cada fonte de dados é processada em um thread. Se o volume de threads excede à capacidade, os threads serão rejeitados para processamento assíncrono e processados de maneira serial.|  
|**Total de relatórios executados**|Número total de relatórios que foram executados com êxito depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios.|  
|**Total de solicitações**|Número total de todas as solicitações feitas ao servidor de relatório depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios.|  
  
##  <a name="bkmk_windowsservice"></a> Contadores de Desempenho do Serviço Windows MSRS 2011  
 O objeto de desempenho do **MSRS 2011 Windows Service** monitora o serviço Windows do servidor de relatório. Este objeto de desempenho inclui uma coleção de contadores usados para controlar o processamento de relatórios que é iniciado por operações agendadas. As operações agendadas podem incluir assinatura e entrega, instantâneos de execução de relatório e histórico de relatórios. Quando você configura este contador, pode aplicá-lo a todas as instâncias de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou selecionar instâncias específicas.  
  
 A tabela a seguir lista os contadores incluídos no objeto de desempenho do **Serviço do Windows MSRS 2011** .  
  
|Contador|Description|  
|-------------|-----------------|  
|**Sessões ativas**|Número de sessões ativas armazenadas no banco de dados do servidor de relatório. Esse contador fornece uma contagem cumulativa de todas as sessões de navegador utilizáveis geradas a partir de assinaturas de relatórios, independentemente de estarem ativas ou não.|  
|**Liberações do cache/s**|Número de liberações de cache por segundo.|  
|**Acertos de cache/s**|Número de solicitações por segundo para relatórios armazenados em cache. As solicitações são para relatórios re-renderizados e não solicitações para relatórios processados diretamente do cache. (Consulte **Total de acertos de cache** mais adiante neste tópico.)|  
|**Acertos do cache/s (modelos semânticos)**|Número de solicitações por segundo para modelos armazenados em cache.|  
|**Erros de cache/s**|Número de solicitações por segundo que não retornaram um relatório de cache. Use este contador para descobrir se os recursos usados para armazenamento em cache (disco ou memória) são suficientes.|  
|**Erros do cache/s (modelos semânticos)**|Número de solicitações por segundo que não retornaram um modelo de cache. Use este contador para descobrir se os recursos usados para armazenamento em cache (disco ou memória) são suficientes.|  
|**Entregas/s**|Número de entregas de relatório por segundo, em qualquer extensão de entrega.|  
|**Eventos/s**|Número de eventos processados por segundo. Os eventos monitorados incluem o **SnapshotUpdated** e o **TimedSubscription**.|  
|**Solicitações/s da primeira sessão**|Número de novas sessões de execução de relatório criadas por segundo.|  
|**Acertos de cache de memória/s**|Número de vezes por segundo que os relatórios são recuperados do cache na memória. *Cache na memória* é uma parte do cache que armazena relatórios na memória da CPU. Quando o cache na memória é usado, o servidor de relatório não consulta o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para obter o conteúdo armazenado em cache.|  
|**Erros de cache de memória/s**|O número de vezes por segundo que os relatórios não podem ser recuperados a partir do cache na memória.|  
|**Solicitações/s da próxima sessão**|Número de solicitações por segundo para relatórios que estão abertos em uma sessão já existente (por exemplo, relatórios que são renderizados de um instantâneo de sessão).|  
|**Solicitações de relatório**|Número de relatórios que estão ativos no momento e gerenciados pelo servidor de relatório. Use esse contador para avaliar estratégia de armazenamento em cache. Pode haver mais solicitações que relatórios gerados.|  
|**Relatórios executados/s**|Número de relatórios gerados com êxito por segundo.|  
|**Solicitações/s**|Número total de solicitações bem-sucedidas do serviço do servidor de relatório processadas por segundo.|  
|**Atualizações de instantâneo/s**|Número total de atualizações de instantâneo de execução de relatório por segundo.|  
|**Total de reciclagens de domínio de aplicativo**|Número total de ciclos do domínio de aplicativo depois do início do serviço Windows do Servidor de Relatório.|  
|**Total de liberações do cache**|Número total de atualizações do cache do servidor de relatórios depois que o serviço é iniciado. Esse contador é zerado quando o domínio de aplicativo é reciclado. Consulte **Liberações do cache/s**.|  
|**Total de acertos de cache**|Número total de solicitações de relatórios processadas diretamente do cache depois do início do serviço Windows do Servidor de Relatórios. Esse contador é zerado quando o domínio de aplicativo é reciclado. Consulte **Acertos do cache/s**.|  
|**Total de acertos do cache (modelos semânticos)**|Número total de solicitações de modelos processadas diretamente do cache depois do início do serviço Windows do Servidor de Relatórios. Esse contador é zerado quando o domínio de aplicativo é reciclado. Consulte **Acertos do cache/s**.|  
|**Total de erros do cache**|Número total de vezes em que não foi possível retornar um relatório do cache depois do início do serviço Windows do Servidor de Relatório. Esse contador é zerado quando o domínio de aplicativo é reciclado. Consulte **Erros do cache/s**.|  
|**Total de erros do cache (modelos semânticos)**|Número total de vezes em que não foi possível retornar um modelo do cache depois do início do serviço Windows do Servidor de Relatório. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|**Total de entregas**|Número total de relatórios entregues pelo Processador de Agendamento e Entrega, para todas as extensões de entrega. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|**Total de eventos**|Número total de eventos depois do início do serviço Windows do servidor de relatório. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|**Total de acertos do cache de memória**|Número total de relatórios armazenados em cache retornados do cache na memória depois do início do serviço Windows do servidor de relatório. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|**Total de erros do cache de memória**|Número total de erros de cache na memória depois que o serviço foi iniciado. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|**Total de falhas de processamento**|O número de erros de processamento de solicitação no servidor de relatório serviço de Windows.|  
|**Total de threads rejeitados**|Número total de threads rejeitados para processamento assíncrono e, posteriormente, tratados como processo síncrono no mesmo thread. Com carga moderada ou pesada, esse contador é incrementado continuamente.|  
|**Total de relatórios executados**|Número total de relatórios executados.|  
|**Total de solicitações**|Número total de relatórios que foram executados com êxito depois que o serviço foi iniciado. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|**Total de atualizações de instantâneos**|Número total de atualizações para instantâneos de execução de relatório.|  
  
##  <a name="bkmk_powershell"></a> Use cmdlets do PowerShell para retornar listas  
 ![Conteúdo relacionado ao PowerShell](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell")O seguinte script do Windows PowerShell retorna os conjuntos de contadores cujo CounterSetName começa com "msr":  
  
```  
get-counter -listset msr*  
```  
  
 O script do Windows PowerShell a seguir retorna a lista de contadores de desempenho para o CounterSetName.  
  
```  
(get-counter -listset "MSRS 2011 Windows Service").paths  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorando o desempenho do servidor de relatório](../../reporting-services/report-server/monitoring-report-server-performance.md)   
 [Contadores de desempenho do modo do SharePoint do serviço Web do MSRS 2011 e objetos de desempenho do modo do SharePoint do serviço Windows do MSRS 2011 &#40;modo do SharePoint&#41;](../../reporting-services/report-server/performance-counters-msrs-2011-sharepoint-mode-performance-objects.md)   
 [Contadores de desempenho para os objetos de desempenho ReportServer:Service e ReportServerSharePoint:Service](../../reporting-services/report-server/performance-counters-reportserver-service-performance-objects.md)  
  
  
