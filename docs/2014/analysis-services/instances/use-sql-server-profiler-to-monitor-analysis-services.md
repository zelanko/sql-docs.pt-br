---
title: Usar SQL Server Profiler para monitorar Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Profiler, Analysis Services
- monitoring Analysis Services [SQL Server]
- performance [Analysis Services], SQL Server Profiler
- Profiler [SQL Server Profiler], Analysis Services
ms.assetid: 8b77dafc-4584-4e93-8ad7-299304391bfd
author: minewiskan
ms.author: owend
ms.openlocfilehash: e144c1d858670f8a46b164ffc9885e6e082c4b0a
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543723"
---
# <a name="use-sql-server-profiler-to-monitor-analysis-services"></a>Use SQL Server Profiler to Monitor Analysis Services
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] controla eventos do processo de mecanismo, como início de um lote ou de uma transação, e captura dados sobre esses eventos, permitindo que você monitore o servidor e a atividade do banco de dados (por exemplo, consultas do usuário ou atividade de logon). Você pode capturar dados do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou de um arquivo para análise posterior e também pode reproduzir os eventos capturados na mesma ou em outra instância [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para ver o que aconteceu exatamente. Você pode reproduzir os eventos em tempo real ou passo a passo. Também é muito útil para executar os eventos de rastreamento junto com os contadores de Desempenho na mesma máquina. O profiler pode correlacionar esses dois eventos com base na hora e exibi-los ao longo de uma única linha do tempo. Eventos de rastreamento darão a você mais detalhes enquanto os contadores de Desempenho proporcionam uma exibição de agregação. Para obter informações sobre como criar e executar rastreamentos, consulte [Criar rastreamentos do Profiler para reprodução &#40;Analysis Services&#41;](create-profiler-traces-for-replay-analysis-services.md).  
  
 A tabela a seguir descreve os tópicos dessa seção.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Introdução ao monitoramento do Analysis Services com o SQL Server Profiler](introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)|Descreve como usar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para monitorar uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[Criar rastreamentos do Profiler para reprodução &#40;Analysis Services&#41;](create-profiler-traces-for-replay-analysis-services.md)|Descreve os requisitos para criar um rastreamento para repetição usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].|  
|[Eventos de rastreamento do Analysis Services](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events)|Descreve as classes de evento do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Essas classes de evento mapeiam as ações geradas pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e são usadas para repetição de rastreamento.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar uma instância do Analysis Services](monitor-an-analysis-services-instance.md)  
  
  
