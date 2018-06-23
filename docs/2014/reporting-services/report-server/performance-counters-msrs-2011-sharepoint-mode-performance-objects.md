---
title: Contadores de desempenho para o modo do SharePoint do MSRS 2014 Web Service e MSRS 2014 Windows Service SharePoint objetos de desempenho (modo SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- performance counters [Reporting Services]
- counters [Reporting Services]
- Report Server Windows service, performance counters
- RS Windows Service performance object
- Scheduling and Delivery Processor performance object [Reporting Services]
- performance [Reporting Services]
ms.assetid: 70bf6980-7845-4ab5-8b2a-ebf526d811a6
caps.latest.revision: 54
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 05e07f38382c6cdc8892c3ffd90ed63798b6f797
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009926"
---
# <a name="performance-counters-for-the-msrs-2014-web-service-sharepoint-mode-and-msrs-2014-windows-service-sharepoint-mode-performance-objects-sharepoint-mode"></a>Contadores de desempenho para os objetos de desempenho do serviço Windows MSRS 2014 e do serviço Web MSRS 2014 (modo do SharePoint)
  Este tópico descreve os contadores de desempenho dos objetos de desempenho `MSRS 2014 Web Service SharePoint Mode` e `MSRS 2014 Windows Service SharePoint Mode` que fazem parte de uma implantação do modo do SharePoint do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)].  
  
> [!NOTE]  
>  Esses objetos de desempenho monitoram eventos no servidor de relatório local. Se você estiver executando um servidor de relatório em uma implantação em expansão, as contagens se aplicarão ao servidor atual e não à implantação em expansão como um todo.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] Modo do SharePoint  
  
 Os objetos de desempenho estão disponíveis no Monitor de Desempenho do Windows (**Perfmon.exe**). Para obter mais informações, consulte a documentação do Windows. [Criação de perfis de tempo de execução](http://msdn.microsoft.com/library/w4bz2147.aspx).  
  
 **Neste tópico:**  
  
-   [Contadores de desempenho do MSRS 2014 Web Service SharePoint modo](#bkmk_webservice)  
  
-   [Contadores de desempenho do MSRS 2014 Windows Service SharePoint modo](#bkmk_windowsservice)  
  
-   [Use cmdlets do PowerShell para retornar listas](#bkmk_powershell)  
  
##  <a name="bkmk_webservice"></a> Contadores de desempenho do MSRS 2014 Web Service SharePoint modo  
 O objeto de desempenho `MSRS 2014 Web Service SharePoint Mode` monitora o desempenho do servidor de relatório. Esse objeto de desempenho inclui uma coleção de contadores usados para controlar o processamento do servidor de relatório iniciado normalmente por operações interativas de exibição de relatórios. Quando você configura esse contador, você pode aplicar o contador para todas as instâncias de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ou você pode selecionar instâncias específicas. Esses contadores são redefinidos sempre que o [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] interrompe o serviço Web Servidor de Relatórios.  
  
 A tabela a seguir lista os contadores que acompanham o `MSRS 2014 Web Service SharePoint Mode` objeto de desempenho.  
  
|Contador|Description|  
|-------------|-----------------|  
|`Active Sessions`|Número de sessões ativas. Este contador fornece uma contagem cumulativa de todas as sessões de navegador geradas a partir de execuções de relatórios, independentemente de estarem ativas ou não.<br /><br /> O contador é reduzido à medida que os registros de sessão são removidos. Por padrão, as sessões são removidas após dez minutos de inatividade.|  
|`Cache Hits/Sec`|Número de solicitações por segundo para relatórios armazenados em cache. Essas são solicitações para relatórios re-renderizados e não solicitações para relatórios processados diretamente do cache. (Consulte `Total Cache Hits` mais adiante neste tópico.)|  
|`Cache Hits/Sec (Semantic Models)`|Número de solicitações por segundo para modelos armazenados em cache. Essas são solicitações para relatórios re-renderizados e não solicitações para relatórios processados diretamente do cache.|  
|`Cache Misses/Sec`|Número de solicitações por segundo que não retornaram um relatório de cache. Use este contador para descobrir se os recursos usados para armazenamento em cache (disco ou memória) são suficientes.|  
|`Cache Misses/Sec (Semantic Models)`|Número de solicitações por segundo que não retornaram um modelo de cache. Use este contador para descobrir se os recursos usados para armazenamento em cache (disco ou memória) são suficientes.|  
|`First Session Requests/Sec`|Número de sessões de usuário novas que são iniciadas no cache de servidor de relatório a cada segundo.|  
|`Memory Cache Hits/Sec`|Número de vezes por segundo que os relatórios são recuperados do cache na memória. *Cache na memória* é uma parte do cache que armazena relatórios na memória da CPU. Quando o cache na memória é usado, o servidor de relatório não consulta o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para obter o conteúdo armazenado em cache.|  
|`Memory Cache Misses/Sec`|Número de vezes por segundo que os relatórios não puderam ser recuperados do cache na memória.|  
|`Next Session Requests/Sec`|Número de solicitações por segundo para relatórios que estão abertos em uma sessão já existente (por exemplo, relatórios que são renderizados de um instantâneo de sessão).|  
|`Report Requests`|Número de relatórios que estão ativos no momento e que estão sendo tratados pelo servidor de relatório.|  
|`Reports Executed/Sec`|Número de execuções de relatório bem-sucedidas por segundo. Este contador fornece estatísticas sobre volume de relatório. Use este contador com `Request/Sec` para comparar a execução do relatório para solicitações de relatório que pode ser retornado do cache.|  
|`Requests/Sec`|Número de solicitações por segundo feitas ao servidor de relatório. Este contador controla todos os tipos de solicitações que são tratadas pelo servidor de relatório.|  
|`Total Cache Hits`|Número total de solicitações de relatórios do cache depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios.|  
|`Total Cache Hits (Semantic Models)`|Número total de solicitações de modelos do cache depois que o serviço foi iniciado. Este contador é zerado sempre que ASP.NET para o serviço Web Servidor de Relatórios.|  
|`Total Cache Misses`|Número total de vezes que um relatório não pôde ser retornado do cache depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios. Use este contador para determinar se espaço em disco e memória são suficientes.|  
|`Total Cache Misses (Semantic Models)`|Número total de vezes que um modelo não pôde ser retornado do cache depois que o serviço foi iniciado. Este contador é zerado sempre que ASP.NET para o serviço Web Servidor de Relatórios. Use este contador para determinar se espaço em disco e memória são suficientes.|  
|`Total Memory Cache Hits`|Número total de relatórios armazenados em cache retornados do cache na memória depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios. *Cache na memória* é uma parte do cache que armazena relatórios na memória da CPU. Quando o cache na memória é usado, o servidor de relatório não consulta o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para obter o conteúdo armazenado em cache.|  
|`Total Memory Cache Misses`|Número total de erros de cache na memória depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios.|  
|`Total Processing Failures`|O número de erros de processamento de solicitação no serviço Web Servidor de Relatórios.|  
|`Total Rejected Threads`|Número total de threads rejeitados para processamento assíncrono e, subsequentemente, tratados como processos síncronos no mesmo thread. Cada fonte de dados é processada em um thread. Se o volume de threads excede à capacidade, os threads serão rejeitados para processamento assíncrono e processados de maneira serial.|  
|`Total Reports Executed`|Número total de relatórios que foram executados com êxito depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios.|  
|`Total Requests`|Número total de todas as solicitações feitas ao servidor de relatório depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios.|  
  
##  <a name="bkmk_windowsservice"></a> Contadores de desempenho do MSRS 2014 Windows Service SharePoint modo  
 O objeto de desempenho do `MSRS 2014 Windows Service SharePoint Mode` é usado para monitorar o serviço Windows do Servidor de Relatório. Este objeto de desempenho inclui uma coleção de contadores usados para controlar o processamento de relatórios que é iniciado por operações agendadas. As operações agendadas podem incluir assinatura e entrega, instantâneos de execução de relatório e histórico de relatórios. Quando você configura esse contador, você pode aplicar o contador para todas as instâncias de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ou você pode selecionar instâncias específicas.  
  
 A tabela a seguir lista os contadores que estão incluídos no `MSRS 2014 Windows Service SharePoint mode` objeto de desempenho.  
  
|Contador|Description|  
|-------------|-----------------|  
|`Active Sessions`|Número de sessões ativas armazenadas no banco de dados do servidor de relatório. Esse contador fornece uma contagem cumulativa de todas as sessões de navegador utilizáveis geradas a partir de assinaturas de relatórios, independentemente de estarem ativas ou não.|  
|`Alerting: event queue length`||  
|`Alerting: events processed - CreateSchedule`||  
|`Alerting: events processed – Delete schedule`||  
|`Alerting: events processed – DeliverAlert`||  
|`Alerting: events processed – FireAlert`||  
|`Alerting: events processed – FireSchedule`||  
|`Alerting: events processed – GenerateAlert`||  
|`Alerting: events processed – UpdateSchedule`||  
|`Cache Flushes/Sec`|Número de liberações de cache por segundo.|  
|`Cache Hits/Sec`|Número de solicitações por segundo para relatórios armazenados em cache. Essas são solicitações para relatórios re-renderizados e não solicitações para relatórios processados diretamente do cache. (Consulte `Total Cache Hits` mais adiante neste tópico.)|  
|`Cache Hits/Sec (Semantic Models)`|Número de solicitações por segundo para modelos armazenados em cache.|  
|`Cache Misses/Sec`|Número de solicitações por segundo que não retornaram um relatório de cache. Use este contador para descobrir se os recursos usados para armazenamento em cache (disco ou memória) são suficientes.|  
|`Cache Misses/Sec (Semantic Models)`|Número de solicitações por segundo que não retornaram um modelo de cache. Use este contador para descobrir se os recursos usados para armazenamento em cache (disco ou memória) são suficientes.|  
|`Delivers/Sec`|Número de entregas de relatório por segundo, em qualquer extensão de entrega.|  
|`Events/Sec`|Número de eventos processados por segundo. Os eventos que são monitorados incluem `SnapshotUpdated` e `TimedSubscription`.|  
|`First Session Requests/Sec`|Número de novas sessões de execução de relatório criadas por segundo.|  
|`Memory Cache Hits/Sec`|Número de vezes por segundo que os relatórios são recuperados do cache na memória. *Cache na memória* é uma parte do cache que armazena relatórios na memória da CPU. Quando o cache na memória é usado, o servidor de relatório não consulta o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para obter o conteúdo armazenado em cache.|  
|`Memory Cache Misses/Sec`|O número de vezes por segundo que os relatórios não podem ser recuperados a partir do cache na memória.|  
|`Next Session Requests/Sec`|Número de solicitações por segundo para relatórios que estão abertos em uma sessão já existente (por exemplo, relatórios que são renderizados de um instantâneo de sessão).|  
|`Report Requests`|Número de relatórios que estão ativos no momento e que estão sendo tratados pelo servidor de relatório. Use esse contador para avaliar estratégia de armazenamento em cache. Pode haver significativamente mais solicitações que relatórios gerados.|  
|`Reports Executed/Sec`|Número de relatórios gerados com êxito por segundo.|  
|`Requests/Sec`|Número total de solicitações bem-sucedidas do serviço do servidor de relatório processadas por segundo.|  
|`Snapshot Updates/Sec`|Número total de atualizações de instantâneo de execução de relatório por segundo.|  
|`Total App Domain Recycles`|Número total de ciclos do domínio de aplicativo depois do início do serviço Windows do Servidor de Relatório.|  
|**Total de liberações do cache**|Número total de atualizações do cache do servidor de relatórios depois que o serviço é iniciado. Esse contador é zerado quando o domínio de aplicativo é reciclado. Consulte `Cache Flushes/Sec`.|  
|`Total Cache Hits`|Número total de solicitações de relatórios processadas diretamente do cache depois do início do serviço Windows do Servidor de Relatórios. Esse contador é zerado quando o domínio de aplicativo é reciclado. Consulte `Cache Hits/Sec`.|  
|`Total Cache Hits (Semantic Models)`|Número total de solicitações de modelos processadas diretamente do cache depois do início do serviço Windows do servidor de relatórios. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|`Total Cache Misses`|Número total de vezes em que não foi possível retornar um relatório do cache depois do início do serviço Windows do Servidor de Relatório. Esse contador é zerado quando o domínio de aplicativo é reciclado. Consulte `Cache Misses/Sec`.|  
|`Total Cache Misses (Semantic Models)`|Número total de vezes em que não foi possível retornar um modelo do cache depois do início do serviço Windows do Servidor de Relatório. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|`Total Deliveries`|Número total de relatórios entregues pelo Processador de Agenda e Entrega, para todas as extensões de entrega. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|`Total Events`|Número total de eventos depois do início do serviço Windows do Servidor de Relatório. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|`Total Memory Cache Hits`|Número total de relatórios armazenados em cache retornados do cache na memória depois do início do serviço Windows do Servidor de Relátório. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|`Total Memory Cache Misses`|Número total de erros de cache na memória depois que o serviço foi iniciado. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|`Total Processing Failures`|O número de erros de processamento de solicitação para o serviço do Windows servidor de relatórios.|  
|`Total Rejected Threads`|Número total de threads rejeitados para processamento assíncrono e, subsequentemente, tratados como um processo síncrono no mesmo thread. Com carga moderada ou pesada, esse contador é incrementado continuamente.|  
|`Total Reports Executed`|Número total de relatórios executados.|  
|`Total Requests`|Número total de relatórios que foram executados com êxito depois que o serviço foi iniciado. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|`Total Snapshot Updates`|Número total de atualizações de instantâneo de execução de relatório.|  
  
##  <a name="bkmk_powershell"></a> Use cmdlets do PowerShell para retornar listas  
 ![Conteúdo relacionado ao PowerShell](../media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell")O script do Windows PowerShell a seguir retornará os conjuntos de contadores cujo CounterSetName começa com “msr”  
  
```  
get-counter -listset msr*  
Returns a list with the following information  
CounterSetName     : MSRS 2014 Windows Service SharePoint Mode  
CounterSetName     : MSRS 2014 Web Service SharePoint Mode  
```  
  
 O script do Windows PowerShell a seguir retorna a lista de contadores de desempenho para o CounterSetName "MSRS 2014 Windows Service modo do SharePoint".  
  
```  
(get-counter -listset "MSRS 2014 Windows Service SharePoint Mode").paths  
```  
  
## <a name="see-also"></a>Consulte também  
 [Monitorando o desempenho do servidor de relatório](monitoring-report-server-performance.md)   
 [Contadores de desempenho para o MSRS 2014 Web Service e objetos de desempenho do MSRS 2014 Windows Service &#40;modo nativo&#41;](../report-server/performance-counters-msrs-2011-web-service-performance-objects.md)  
  
  