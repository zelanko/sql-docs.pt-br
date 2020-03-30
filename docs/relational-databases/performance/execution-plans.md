---
title: Planos de execução | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- query plans [SQL Server]
- execution plans [SQL Server]
- execution plan [SQL Server]
- query plan [SQL Server]
- query execution plans
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753f
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 81a9f0e52c061ec494143eb4f61158546f5e57f9
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "78256920"
---
# <a name="execution-plans"></a>Planos de execução
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Para poder executar consultas, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] deve analisar a instrução para determinar a maneira mais eficiente de acessar os dados necessários. Essa análise é tratada por um componente chamado de Otimizador de Consulta. A entrada do Otimizador de Consulta consiste em uma consulta, o esquema de banco de dados (definições de tabela e de índice) e as estatísticas de banco de dados. A saída do Otimizador de Consulta é um plano de execução de consulta, às vezes chamado de plano de consulta ou plano de execução.   

Um plano de execução de consulta é uma definição do seguinte: 

- **A sequência em que as tabelas de origem são acessadas.**  
  Normalmente, há muitas sequências pelas quais o servidor de banco de dados pode acessar as tabelas base para criar o conjunto de resultados. Por exemplo, se uma instrução `SELECT` fizesse referência a três tabelas, o servidor de banco de dados poderia acessar `TableA`primeiro, usar os dados de `TableA` para extrair as linhas correspondentes de `TableB`e usar os dados de `TableB` para extrair dados de `TableC`. As outras sequências em que o servidor de banco de dados poderia acessar as tabelas são:  
  `TableC`, `TableB`, `TableA`ou  
  `TableB`, `TableA`, `TableC`ou  
  `TableB`, `TableC`, `TableA`ou  
  `TableC`, `TableA`, `TableB`  

- **Os métodos usados para extrair dados de cada tabela.**  
  Geralmente, há métodos diferentes para acessar os dados em cada tabela. Se forem necessárias apenas algumas linhas com valores de chave específicos, o servidor de banco de dados poderá usar um índice. Se forem necessárias todas as linhas da tabela, o servidor de banco de dados poderá ignorar os índices e executar um exame na tabela. Se forem necessárias todas as linhas de uma tabela, mas houver um índice cujas colunas de chave estão em um `ORDER BY`, executando um exame de índice em vez de um exame de tabela, uma classificação separada do conjunto de resultados poderá ser salva. Se uma tabela for muito pequena, os exames de tabela poderão ser o método mais eficiente para quase todos os acessos à tabela.
  
- **Os métodos usados para computar cálculos e como filtrar, agregar e classificar dados de cada tabela.**  
  Como os dados são acessados a partir de tabelas, existem métodos diferentes para executar cálculos em dados, como a computação de valores escalares, e para agregar e classificar dados conforme definido no texto da consulta, por exemplo, ao usar uma cláusula `GROUP BY` ou `ORDER BY`, e como filtrar dados, por exemplo, ao usar uma cláusula `WHERE` ou `HAVING`.

> [!NOTE]
> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] tem três opções para exibir os planos de execução:        
> -  O ***[Plano de Execução Estimado](../../relational-databases/performance/display-the-estimated-execution-plan.md)***, que é o plano compilado, como produzido pelo Otimizador de Consulta com base em estimativas.        
> -  O ***[Plano de Execução Real](../../relational-databases/performance/display-an-actual-execution-plan.md)***, que é o mesmo que o plano compilado mais o [contexto de execução](../../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse). Inclui informações de runtime disponíveis depois que a execução é concluída, como avisos de execução, ou em versões mais recentes do [!INCLUDE[ssde_md](../../includes/ssde_md.md)], o tempo decorrido e o tempo de CPU usados durante a execução.        
> -  As ***[Estatísticas de Consulta Dinâmica](../../relational-databases/performance/live-query-statistics.md)***, que são o mesmo que o plano compilado, mais o contexto de execução. Isso inclui informações de runtime durante o progresso da execução e é atualizado a cada segundo. As informações de runtime incluem, por exemplo, o número real de linhas que fluem pelos operadores.       

> [!TIP]
> Para obter mais informações sobre o processamento de consultas e planos de execução de consulta, confira as seções [Otimizar as instruções SELECT](../../relational-databases/query-processing-architecture-guide.md#optimizing-select-statements) e [Cache e Reutilização do Plano de Execução](../../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse) do Guia de Arquitetura de Processamento de Consultas.

## <a name="in-this-section"></a>Nesta seção  
[Infraestrutura de criação de perfil de consulta](../../relational-databases/performance/query-profiling-infrastructure.md)     
[Exibir e salvar planos de execução](../../relational-databases/performance/display-and-save-execution-plans.md)     
[Comparar e analisar planos de execução](../../relational-databases/performance/compare-and-analyze-execution-plans.md)     
[Guias de plano](../../relational-databases/performance/plan-guides.md)     

## <a name="see-also"></a>Consulte Também  
[Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
[Ferramentas para monitoramento e ajuste de desempenho](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
[Guia de arquitetura de processamento de consultas](../../relational-databases/query-processing-architecture-guide.md)    
[Estatísticas de consulta dinâmica](../../relational-databases/performance/live-query-statistics.md)     
[Monitor de atividade](../../relational-databases/performance-monitor/activity-monitor.md)     
[Monitorando o desempenho com o Repositório de Consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
[sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)     
[sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)     
[Sinalizadores de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)    
[Referência de operadores físicos e lógicos de plano de execução](../../relational-databases/showplan-logical-and-physical-operators-reference.md)
