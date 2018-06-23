---
title: Use o SQL Server Profiler para monitorar o Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Profiler, Analysis Services
- monitoring Analysis Services [SQL Server]
- performance [Analysis Services], SQL Server Profiler
- Profiler [SQL Server Profiler], Analysis Services
ms.assetid: 8b77dafc-4584-4e93-8ad7-299304391bfd
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 90752fda77529ba73cd7059748c1480769e20939
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010118"
---
# <a name="use-sql-server-profiler-to-monitor-analysis-services"></a>Use SQL Server Profiler to Monitor Analysis Services
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] controla eventos do processo de mecanismo, como início de um lote ou de uma transação, e captura dados sobre esses eventos, permitindo que você monitore o servidor e a atividade do banco de dados (por exemplo, consultas do usuário ou atividade de logon). Você pode capturar dados do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou de um arquivo para análise posterior e também pode reproduzir os eventos capturados na mesma ou em outra instância [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para ver o que aconteceu exatamente. Você pode reproduzir os eventos em tempo real ou passo a passo. Também é muito útil para executar os eventos de rastreamento junto com os contadores de Desempenho na mesma máquina. O profiler pode correlacionar esses dois eventos com base na hora e exibi-los ao longo de uma única linha do tempo. Eventos de rastreamento darão a você mais detalhes enquanto os contadores de Desempenho proporcionam uma exibição de agregação. Para obter informações sobre como criar e executar rastreamentos, consulte [Create Profiler Traces for Replay &#40;Analysis Services&#41;](create-profiler-traces-for-replay-analysis-services.md).  
  
 A tabela a seguir descreve os tópicos dessa seção.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Introdução ao monitoramento do Analysis Services com o SQL Server Profiler](introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)|Descreve como usar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para monitorar uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[Criar rastreamentos do Profiler para reprodução &#40;do Analysis Services&#41;](create-profiler-traces-for-replay-analysis-services.md)|Descreve os requisitos para criar um rastreamento para repetição usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].|  
|[Eventos de rastreamento do Analysis Services](../trace-events/analysis-services-trace-events.md)|Descreve as classes de evento do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Essas classes de evento mapeiam as ações geradas pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e são usadas para repetição de rastreamento.|  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar uma instância do Analysis Services](monitor-an-analysis-services-instance.md)  
  
  