---
title: Otimizar o rastreamento do SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- time [SQL Server], traces
- SQL Trace, performance
- traces [SQL Server], performance
- performance [SQL Server], trace
ms.assetid: 50944218-925f-4576-aec8-4379846d7681
caps.latest.revision: 24
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fee234855ca643b46bcea8b4df0a7c543ee51dcc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37299866"
---
# <a name="optimize-sql-trace"></a>Otimizar o Rastreamento do SQL
  Embora a execução do Rastreamento do SQL imponha custos ao desempenho, por usar recursos do sistema para coletar os dados, há diversos procedimentos que podem minimizar esse efeito. Para minimizar os custos ao desempenho devidos a um rastreamento, tente o seguinte:  
  
-   Considere o uso do prompt de comando para executar os rastreamentos: Usar uma interface gráfica do usuário atrapalha o desempenho. Para obter mais informações, veja [sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql).  
  
-   Evite incluir eventos que ocorrem com frequência. Se possível, restrinja seu rastreamento por meio de classes de evento e filtros específicos. Quanto menos eventos forem coletados no rastreamento, menos recursos do sistema serão necessários para dar suporte a ele.  
  
-   Direcione o rastreamento de modo a coletar apenas eventos que forneçam dados relevantes. Por exemplo, se o rastreamento for destinado a identificar deadlocks, inclua a classe de evento **Lock:Deadlock** , mas não a classe de evento **Lock:Acquired** . Se você incluir ambas as classes de evento, o rastreamento terá de responder a cada bloqueio adquirido e a execução lhe custará o dobro.  
  
-   Evite coletar dados duplicados. Por exemplo, se coletar **SQL:BatchStarted** e **SQL:BatchCompleted**, você poderá minimizar o tamanho do conjunto de resultados coletando dados de texto apenas para a classe de evento **SQL:BatchStarted** .  
  
-   Use filtros na definição do rastreamento. Por exemplo, se souber que certo usuário está informando baixo desempenho durante consultas ad hoc, crie um filtro baseado em **LoginName**. Defina o filtro de modo a incluir apenas eventos cujo **LoginName** corresponda ao nome de usuário em questão.  
  
 Se for necessário executar um rastreamento de eventos que estão gerando um impacto significativo sobre o desempenho, considere limitar o impacto sobre o desempenho do servidor usando um dos seguintes métodos:  
  
-   Execute rastreamentos com duração mais curta. É possível controlar a duração da execução de um rastreamento habilitando um horário de parada. Isso será especialmente importante se você não puder limitar as classes de evento ou filtrar um evento. Habilitar um horário de parada assegura que o desempenho incorrido não durará indefinidamente.  
  
-   Limite o tamanho dos resultados do rastreamento. É possível limitar o tamanho máximo do arquivo de resultados do rastreamento. Essa estratégia garante que pare de haver custo ao desempenho quando o limite de tamanho de arquivo for atingido (se a substituição de arquivo não estiver habilitada).  
  
-   Limite o número de eventos retornados. Com o [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] , é possível limitar o número de eventos retornados salvando o rastreamento em uma tabela e definindo o número máximo de linhas. Os resultados do rastreamento continuam sendo retornados na tela do [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] quando o número máximo de linhas é atingido, mas elimina-se o custo decorrido do registro dos resultados em uma tabela.  
  
## <a name="see-also"></a>Consulte também  
 [Filtrar um rastreamento](../sql-trace/filter-a-trace.md)  
  
  
