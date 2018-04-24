---
title: Otimizar o rastreamento do SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: sql-trace
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- time [SQL Server], traces
- SQL Trace, performance
- traces [SQL Server], performance
- performance [SQL Server], trace
ms.assetid: 50944218-925f-4576-aec8-4379846d7681
caps.latest.revision: 25
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0eba27be64b60231aeb0b9a11e7ae1c48a80cf71
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="optimize-sql-trace"></a>Otimizar o Rastreamento do SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Embora a execução do Rastreamento do SQL imponha custos ao desempenho, por usar recursos do sistema para coletar os dados, há diversos procedimentos que podem minimizar esse efeito. Para minimizar os custos ao desempenho devidos a um rastreamento, tente o seguinte:  
  
-   Considere o uso do prompt de comando para executar os rastreamentos: Usar uma interface gráfica do usuário atrapalha o desempenho. Para obter mais informações, veja [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md).  
  
-   Evite incluir eventos que ocorrem com frequência. Se possível, restrinja seu rastreamento por meio de classes de evento e filtros específicos. Quanto menos eventos forem coletados no rastreamento, menos recursos do sistema serão necessários para dar suporte a ele.  
  
-   Direcione o rastreamento de modo a coletar apenas eventos que forneçam dados relevantes. Por exemplo, se o rastreamento for destinado a identificar deadlocks, inclua a classe de evento **Lock:Deadlock** , mas não a classe de evento **Lock:Acquired** . Se você incluir ambas as classes de evento, o rastreamento terá de responder a cada bloqueio adquirido e a execução lhe custará o dobro.  
  
-   Evite coletar dados duplicados. Por exemplo, se coletar **SQL:BatchStarted** e **SQL:BatchCompleted**, você poderá minimizar o tamanho do conjunto de resultados coletando dados de texto apenas para a classe de evento **SQL:BatchStarted** .  
  
-   Use filtros na definição do rastreamento. Por exemplo, se souber que certo usuário está informando baixo desempenho durante consultas ad hoc, crie um filtro baseado em **LoginName**. Defina o filtro de modo a incluir apenas eventos cujo **LoginName** corresponda ao nome de usuário em questão.  
  
 Se for necessário executar um rastreamento de eventos que estão gerando um impacto significativo sobre o desempenho, considere limitar o impacto sobre o desempenho do servidor usando um dos seguintes métodos:  
  
-   Execute rastreamentos com duração mais curta. É possível controlar a duração da execução de um rastreamento habilitando um horário de parada. Isso será especialmente importante se você não puder limitar as classes de evento ou filtrar um evento. Habilitar um horário de parada assegura que o desempenho incorrido não durará indefinidamente.  
  
-   Limite o tamanho dos resultados do rastreamento. É possível limitar o tamanho máximo do arquivo de resultados do rastreamento. Essa estratégia garante que pare de haver custo ao desempenho quando o limite de tamanho de arquivo for atingido (se a substituição de arquivo não estiver habilitada).  
  
-   Limite o número de eventos retornados. Com o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] , é possível limitar o número de eventos retornados salvando o rastreamento em uma tabela e definindo o número máximo de linhas. Os resultados do rastreamento continuam sendo retornados na tela do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] quando o número máximo de linhas é atingido, mas elimina-se o custo decorrido do registro dos resultados em uma tabela.  
  
## <a name="see-also"></a>Consulte Também  
 [Filtrar um rastreamento](../../relational-databases/sql-trace/filter-a-trace.md)  
  
  
