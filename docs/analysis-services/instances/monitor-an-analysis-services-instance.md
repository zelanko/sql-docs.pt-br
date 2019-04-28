---
title: Monitorar uma visão geral de instância do Analysis Services | Microsoft Docs
ms.date: 11/16/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 39cc5a22165d07aafce29e4216548c4e8d226892
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62709468"
---
# <a name="monitoring-overview"></a>Visão geral de monitoramento
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

Analysis Services tem várias ferramentas diferentes para ajudá-lo a monitorar e ajustar o desempenho dos seus servidores. A escolha da ferramenta depende do tipo de monitoramento ou de ajuste a ser feito e dos eventos em particular a monitorar.

Para obter mais informações sobre como monitorar o SQL Server Analysis Services, consulte o [guia de operações do SQL Server 2008 R2](http://go.microsoft.com/fwlink/?LinkID=225539).  
  
## <a name="monitoring-tools"></a>Ferramentas de monitoramento  

|Ferramenta  |Descrição  |
|---------|---------|
|[SQL Server Profiler](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)      |   Rastreia eventos de processo do mecanismo. Ele também captura dados sobre esses eventos, permitindo que você monitore a atividade de servidor e banco de dados.      |
| [Eventos estendidos](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)     |   Um sistema que usa pouquíssimos recursos do sistema de monitoramento, torna uma ferramenta ideal para diagnosticar problemas em servidores de produção e teste de desempenho e rastreamento de leve.       |
| [Exibições de gerenciamento dinâmico &#40;DMVs&#41;](../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)      |   Consultas que retornam informações sobre objetos de modelo, as operações do servidor e a integridade do servidor. A consulta, com base em SQL, é uma interface para conjuntos de linhas de esquema.      |
| [Eventos de rastreamento](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events)     |  Siga a atividade de uma instância capturando e analisando os eventos de rastreamento gerados pela instância. Os eventos de rastreamento são agrupados de forma que você possa localizar facilmente eventos de rastreamento relacionados.        |
|   [Contadores de desempenho](../../analysis-services/instances/performance-counters-ssas.md)\*    |    Usando o Monitor de Desempenho, você pode monitorar o desempenho de uma instância do Microsoft SQL Server Analysis Services (SSAS) usando contadores de desempenho.     |
|[Operações de log](../../analysis-services/instances/performance-counters-ssas.md)\*|Uma instância do SQL Server Analysis Services registrará notificações do servidor, erros e avisos no arquivo msmdsrv exe-um para cada instância instalada. |

\* Aplica-se ao SQL Server Analysis Services só.

## <a name="see-also"></a>Confira também

[Monitorar métricas do servidor do Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-monitor)   
[Configurar o log de diagnóstico do Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-logging)
