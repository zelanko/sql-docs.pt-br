---
title: Contadores de desempenho para o MSRS 2014 Web Service e objetos do desempenho de serviço Windows MSRS 2014 (modo nativo) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- performance counters [Reporting Services]
- Report Server Web service, performance counters
- Reporting Services performance object
- RS Web Service performance object
- counters [Reporting Services]
- performance [Reporting Services]
ms.assetid: c642fc4f-8734-4626-a194-42ac9cd8e2ef
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7d28e597d36305b9c4df7c8b4a499dc507b1ed31
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63191208"
---
# <a name="performance-counters-for-the-msrs-2014-web-service-and-msrs-2014-windows-service-performance-objects-native-mode"></a>Contadores de desempenho para o objeto de desempenho do serviço Windows MSRS 2014 e o Serviço Web MSRS 2014 (modo nativo)
  Este tópico descreve os contadores de desempenho dos objetos de desempenho `MSRS 2014 Web Service` e `MSRS 2014 Windows Service`  
  
> [!NOTE]  
>  Esses objetos de desempenho monitoram eventos no servidor de relatório local. Se você estiver executando um servidor de relatório em uma implantação em expansão, as contagens aplicam-se ao servidor atual e não à implantação em expansão.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] Modo nativo  
  
 Os objetos de desempenho estão disponíveis no Monitor de Desempenho do Windows (**Perfmon.exe**). Para saber mais, veja a documentação do Windows, [Criação de perfil em tempo de execução](https://msdn.microsoft.com/library/w4bz2147.aspx) (https://msdn.microsoft.com/library/w4bz2147.aspx).  
  
 Para obter informações relacionadas aos contadores de desempenho do modo do SharePoint, consulte [contadores de desempenho para o modo do SharePoint do MSRS 2014 Web Service e objetos de desempenho do MSRS 2014 Windows Service SharePoint modo &#40;modo do SharePoint&#41; ](../report-server/performance-counters-msrs-2011-web-service-performance-objects.md).  
  
 **Neste tópico:**  
  
-   [Contadores de desempenho do MSRS 2014 Web Service](#bkmk_webservice)  
  
-   [Contadores de desempenho do MSRS 2014 Windows Service](#bkmk_windowsservice)  
  
-   [Use cmdlets do PowerShell para retornar listas](#bkmk_powershell)  
  
##  <a name="bkmk_webservice"></a> Contadores de desempenho do MSRS 2014 Web Service  
 O objeto de desempenho `MSRS 2014 Web Service` monitora o desempenho do servidor de relatório. Esse objeto de desempenho inclui uma coleção de contadores usados para controlar o processamento do servidor de relatório iniciado normalmente por operações interativas de exibição de relatórios. Quando você configura este contador, pode aplicá-lo a todas as instâncias de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ou selecionar instâncias específicas. Esses contadores são redefinidos sempre que o [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] interrompe o serviço Web servidor de relatórios.  
  
 A tabela a seguir lista os contadores que são incluídos com o objeto de desempenho do `MSRS 2014 Web Service`.  
  
|Contador|Descrição|  
|-------------|-----------------|  
|`Active Sessions`|Número de sessões ativas. Este contador fornece uma contagem cumulativa de todas as sessões de navegador geradas a partir de execuções de relatórios, independentemente de estarem ativas ou não.<br /><br /> O contador é reduzido à medida que os registros de sessão são removidos. Por padrão, as sessões são removidas após dez minutos de inatividade.|  
|`Cache Hits/Sec`|Número de solicitações por segundo para relatórios armazenados em cache. As solicitações são para relatórios re-renderizados e não solicitações para relatórios processados diretamente do cache. (Consulte `Total Cache Hits` mais adiante neste tópico.)|  
|`Cache Hits/Sec (Semantic Models)`|Número de solicitações por segundo para modelos armazenados em cache. As solicitações para relatórios re-renderizados e não solicitações para relatórios processados diretamente do cache.|  
|`Cache Misses/Sec`|Número de solicitações por segundo que não retornaram um relatório de cache. Use este contador para descobrir se os recursos usados para armazenamento em cache (disco ou memória) são suficientes.|  
|`Cache Misses/Sec (Semantic Models)`|Número de solicitações por segundo que não retornaram um modelo de cache. Use este contador para descobrir se os recursos usados para armazenamento em cache (disco ou memória) são suficientes.|  
|`First Session Requests/Sec`|Número de sessões de usuário novas que são iniciadas no cache de servidor de relatório a cada segundo.|  
|`Memory Cache Hits/Sec`|Número de vezes por segundo que os relatórios são recuperados do cache na memória. *Cache na memória* é uma parte do cache que armazena relatórios na memória da CPU. Quando o cache na memória é usado, o servidor de relatório não consulta o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para obter o conteúdo armazenado em cache.|  
|`Memory Cache Misses/Sec`|Número de vezes por segundo que os relatórios não puderam ser recuperados do cache na memória.|  
|`Next Session Requests/Sec`|Número de solicitações por segundo para relatórios que estão abertos em uma sessão já existente (por exemplo, relatórios que são renderizados de um instantâneo de sessão).|  
|`Report Requests`|Número de relatórios que estão ativos no momento e gerenciados pelo servidor de relatório.|  
|`Reports Executed/Sec`|Número de execuções de relatório bem-sucedidas por segundo. Este contador fornece estatísticas sobre volume de relatório. Use este contador com `Request/Sec` para comparar execução de relatórios com solicitações de relatórios que podem ser retornadas do cache.|  
|`Requests/Sec`|Número de solicitações por segundo feitas ao servidor de relatório. Este contador controla todos os tipos de solicitações que são gerenciadas pelo servidor de relatório.|  
|`Total Cache Hits`|Número total de solicitações de relatórios do cache depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios.|  
|`Total Cache Hits (Semantic Models)`|Número total de solicitações de modelos do cache depois que o serviço foi iniciado. Este contador é zerado sempre que ASP.NET para o serviço Web Servidor de Relatórios.|  
|`Total Cache Misses`|Número total de vezes que um relatório não pôde ser retornado do cache depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios. Use este contador para determinar se espaço em disco e memória são suficientes.|  
|`Total Cache Misses (Semantic Models)`|Número total de vezes que um modelo não pôde ser retornado do cache depois que o serviço foi iniciado. Este contador é zerado sempre que ASP.NET para o serviço Web Servidor de Relatórios. Use este contador para determinar se espaço em disco e memória são suficientes.|  
|`Total Memory Cache Hits`|Número total de relatórios armazenados em cache retornados do cache na memória depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios. *Cache na memória* é uma parte do cache que armazena relatórios na memória da CPU. Quando o cache na memória é usado, o servidor de relatório não consulta o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para obter o conteúdo armazenado em cache.|  
|`Total Memory Cache Misses`|Número total de erros de cache na memória depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios.|  
|`Total Processing Failures`|O número de erros de processamento de solicitação para o serviço Web Servidor de Relatórios.|  
|`Total Rejected Threads`|Número total de threads rejeitados para processamento assíncrono e, posteriormente, tratados como processos síncronos no mesmo thread. Cada fonte de dados é processada em um thread. Se o volume de threads excede à capacidade, os threads serão rejeitados para processamento assíncrono e processados de maneira serial.|  
|`Total Reports Executed`|Número total de relatórios que foram executados com êxito depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios.|  
|`Total Requests`|Número total de todas as solicitações feitas ao servidor de relatório depois que o serviço foi iniciado. Este contador é zerado sempre que [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] para o serviço Web Servidor de Relatórios.|  
  
##  <a name="bkmk_windowsservice"></a> Contadores de desempenho do MSRS 2014 Windows Service  
 O objeto de desempenho do `MSRS 2014 Windows Service` monitora o serviço Windows do servidor de relatório. Este objeto de desempenho inclui uma coleção de contadores usados para controlar o processamento de relatórios que é iniciado por operações agendadas. As operações agendadas podem incluir assinatura e entrega, instantâneos de execução de relatório e histórico de relatórios. Quando você configura este contador, pode aplicá-lo a todas as instâncias de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ou selecionar instâncias específicas.  
  
 A tabela a seguir lista os contadores incluídos no objeto de desempenho `MSRS 2014 Windows Service`.  
  
|Contador|Descrição|  
|-------------|-----------------|  
|`Active Sessions`|Número de sessões ativas armazenadas no banco de dados do servidor de relatório. Esse contador fornece uma contagem cumulativa de todas as sessões de navegador utilizáveis geradas a partir de assinaturas de relatórios, independentemente de estarem ativas ou não.|  
|`Cache Flushes/Sec`|Número de liberações de cache por segundo.|  
|`Cache Hits/Sec`|Número de solicitações por segundo para relatórios armazenados em cache. As solicitações são para relatórios re-renderizados e não solicitações para relatórios processados diretamente do cache. (Consulte `Total Cache Hits` mais adiante neste tópico.)|  
|`Cache Hits/Sec (Semantic Models)`|Número de solicitações por segundo para modelos armazenados em cache.|  
|`Cache Misses/Sec`|Número de solicitações por segundo que não retornaram um relatório de cache. Use este contador para descobrir se os recursos usados para armazenamento em cache (disco ou memória) são suficientes.|  
|`Cache Misses/Sec (Semantic Models)`|Número de solicitações por segundo que não retornaram um modelo de cache. Use este contador para descobrir se os recursos usados para armazenamento em cache (disco ou memória) são suficientes.|  
|`Delivers/Sec`|Número de entregas de relatório por segundo, em qualquer extensão de entrega.|  
|`Events/Sec`|Número de eventos processados por segundo. Os eventos monitorados incluem `SnapshotUpdated` e `TimedSubscription`.|  
|`First Session Requests/Sec`|Número de novas sessões de execução de relatório criadas por segundo.|  
|`Memory Cache Hits/Sec`|Número de vezes por segundo que os relatórios são recuperados do cache na memória. *Cache na memória* é uma parte do cache que armazena relatórios na memória da CPU. Quando o cache na memória é usado, o servidor de relatório não consulta o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para obter o conteúdo armazenado em cache.|  
|`Memory Cache Misses/Sec`|O número de vezes por segundo que os relatórios não podem ser recuperados a partir do cache na memória.|  
|`Next Session Requests/Sec`|Número de solicitações por segundo para relatórios que estão abertos em uma sessão já existente (por exemplo, relatórios que são renderizados de um instantâneo de sessão).|  
|`Report Requests`|Número de relatórios que estão ativos no momento e gerenciados pelo servidor de relatório. Use esse contador para avaliar estratégia de armazenamento em cache. Pode haver mais solicitações que relatórios gerados.|  
|`Reports Executed/Sec`|Número de relatórios gerados com êxito por segundo.|  
|`Requests/Sec`|Número total de solicitações bem-sucedidas do serviço do servidor de relatório processadas por segundo.|  
|`Snapshot Updates/Sec`|Número total de atualizações de instantâneo de execução de relatório por segundo.|  
|`Total App Domain Recycles`|Número total de ciclos do domínio de aplicativo depois do início do serviço Windows do Servidor de Relatório.|  
|**Total de liberações do cache**|Número total de atualizações do cache do servidor de relatórios depois que o serviço é iniciado. Esse contador é zerado quando o domínio de aplicativo é reciclado. Consulte `Cache Flushes/Sec`.|  
|`Total Cache Hits`|Número total de solicitações de relatórios processadas diretamente do cache depois do início do serviço Windows do Servidor de Relatórios. Esse contador é zerado quando o domínio de aplicativo é reciclado. Consulte `Cache Hits/Sec`.|  
|`Total Cache Hits (Semantic Models)`|Número total de solicitações de modelos processadas diretamente do cache depois do início do serviço Windows do Servidor de Relatórios. Esse contador é zerado quando o domínio de aplicativo é reciclado. Consulte `Cache Hits/Sec`.|  
|`Total Cache Misses`|Número total de vezes em que não foi possível retornar um relatório do cache depois do início do serviço Windows do Servidor de Relatório. Esse contador é zerado quando o domínio de aplicativo é reciclado. Consulte `Cache Misses/Sec`.|  
|`Total Cache Misses (Semantic Models)`|Número total de vezes em que não foi possível retornar um modelo do cache depois do início do serviço Windows do Servidor de Relatório. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|`Total Deliveries`|Número total de relatórios entregues pelo Processador de Agendamento e Entrega, para todas as extensões de entrega. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|`Total Events`|Número total de eventos depois do início do serviço Windows do servidor de relatório. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|`Total Memory Cache Hits`|Número total de relatórios armazenados em cache retornados do cache na memória depois do início do serviço Windows do servidor de relatório. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|`Total Memory Cache Misses`|Número total de erros de cache na memória depois que o serviço foi iniciado. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|`Total Processing Failures`|O número de erros de processamento de solicitação no servidor de relatório serviço de Windows.|  
|`Total Rejected Threads`|Número total de threads rejeitados para processamento assíncrono e, posteriormente, tratados como processo síncrono no mesmo thread. Com carga moderada ou pesada, esse contador é incrementado continuamente.|  
|`Total Reports Executed`|Número total de relatórios executados.|  
|`Total Requests`|Número total de relatórios que foram executados com êxito depois que o serviço foi iniciado. Esse contador é zerado quando o domínio de aplicativo é reciclado.|  
|`Total Snapshot Updates`|Número total de atualizações para instantâneos de execução de relatório.|  
  
##  <a name="bkmk_powershell"></a> Use cmdlets do PowerShell para retornar listas  
 ![Conteúdo relacionado ao PowerShell](../media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell")O seguinte script do Windows PowerShell retorna os conjuntos de contadores cujo CounterSetName começa com "msr":  
  
```  
get-counter -listset msr*  
```  
  
 O script do Windows PowerShell a seguir retorna a lista de contadores de desempenho para o CounterSetName.  
  
```  
(get-counter -listset "MSRS 2014 Windows Service").paths  
```  
  
## <a name="see-also"></a>Consulte também  
 [Monitorando o desempenho do servidor de relatório](monitoring-report-server-performance.md)   
 [Contadores de desempenho para o modo do SharePoint do MSRS 2014 Web Service e objetos de desempenho do MSRS 2014 Windows Service SharePoint modo &#40;modo do SharePoint&#41;](../report-server/performance-counters-msrs-2011-web-service-performance-objects.md)   
 [Contadores de desempenho para os objetos de desempenho ReportServer:Service e ReportServerSharePoint:Service](performance-counters-reportserver-service-performance-objects.md)  
  
  
