---
title: Monitorar e ajustar o desempenho | Microsoft Docs
ms.custom: 
ms.date: 07/18/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- instances of SQL Server, monitoring performance
- monitoring server performance [SQL Server]
- Database Engine [SQL Server], performance
- monitoring performance [SQL Server], about performance
- server performance [SQL Server]
- monitoring performance [SQL Server]
- database performance [SQL Server], about performance
- tuning databases [SQL Server], about performance
- status information [SQL Server], performance monitoring
- database monitoring [SQL Server], about performance
- monitoring [SQL Server], queries performance
- server performance [SQL Server], about performance
- tuning databases [SQL Server]
- database performance [SQL Server]
- monitoring [SQL Server], server performance
- database monitoring [SQL Server]
- monitoring server performance [SQL Server], about monitoring server performance
ms.assetid: 87f23f03-0f19-4b2e-bfae-efa378f7a0d4
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f9825e46e8f39d8077df64a2e15b6a2eeec47c03
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="monitor-and-tune-for-performance"></a>Monitorar e ajustar o desempenho
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] A meta do monitoramento de bancos de dados é avaliar o desempenho do servidor. Um monitoramento eficaz envolve a criação de instantâneos periódicos do desempenho atual para isolar processos que estão ocasionando problemas, e a coleta contínua de dados para o controle das tendências de desempenho.  
  
 A avaliação contínua do desempenho de banco de dados ajuda a minimizar tempos de resposta e a maximizar a taxa de transferência, permitindo alcançar desempenho ótimo. Tráfego de rede, E/S de disco e uso de CPU eficientes são fundamentais para um desempenho ótimo. É preciso analisar minuciosamente os requisitos de aplicativos, compreender a estrutura lógica e física dos dados, avaliar o uso de banco de dados e negociar compensações entre usos conflitantes, tais como a do processamento de transações online (OLTP) versus o apoio à decisão.  
  
## <a name="monitoring-and-tuning-databases-for-performance"></a>Monitorando e ajustando o desempenho de bancos de dados  
 O Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o sistema operacional Microsoft Windows fornecem utilitários que lhe permitem exibir a condição atual do banco de dados e acompanhar o desempenho conforme as condições mudam. Há uma variedade de ferramentas e técnicas que podem ser usadas para monitorar o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O monitoramento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ajuda a:  
  
-   Determinar se o desempenho pode ser melhorado. Por exemplo, ao monitorar os tempos de resposta a consultas utilizadas com frequência, é possível determinar se são necessárias alterações na consulta ou nos índices das tabelas.  
  
-   Avaliar a atividade de usuário. Por exemplo, monitorando os usuários que tentam se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é possível determinar se a segurança está configurada adequadamente e testar aplicativos ou sistemas de desenvolvimento. Por exemplo, monitorando consultas SQL à medida que são executadas, é possível determinar se estão escritas corretamente e produzindo os resultados esperados.  
  
-   Solucionar problemas ou depurar componentes de aplicativos, como procedimentos armazenados.  
  
## <a name="monitoring-in-a-dynamic-environment"></a>Monitorando em um ambiente dinâmico  
Mudanças nas condições resultam em alterações no desempenho. Em suas avaliações, você poderá consultar alterações no desempenho à medida que o número de usuários aumenta, o acesso de usuário e os métodos de conexões mudam, o conteúdo do banco de dados cresce, os aplicativos cliente se modificam, os dados nos aplicativos se alteram, as consultas se tornam mais complexas e o tráfego de rede aumenta. Com as ferramentas para monitorar o desempenho, é possível associar algumas alterações no desempenho a mudanças de condições e consultas complexas. **Exemplos:**:  
  
-   Monitorando os tempos de resposta a consultas utilizadas com frequência, é possível determinar se são necessárias alterações na consulta ou nos índices das tabelas em que as consultas são executadas.  
  
-   Monitorando consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] à medida que são executadas, é possível determinar se elas estão escritas corretamente e produzindo os resultados esperados.  
  
-   Monitorando os usuários que tentam se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é possível determinar se a segurança está configurada adequadamente e testar aplicativos ou sistemas de desenvolvimento.  
  
 O tempo de resposta é o tempo necessário para que a primeira linha do conjunto de resultados seja retornada para o usuário, na forma de uma confirmação visual de que uma consulta está sendo processada. A taxa de transferência é o número total de consultas manipuladas pelo servidor durante um período de tempo especificado.  
  
 À medida que o número de usuário aumenta, aumenta a competição por recursos do servidor, o que, por sua vez, aumenta o tempo de resposta e diminui o processamento global.  
  
## <a name="monitoring-and-performance-tuning-tasks"></a>Tarefas de monitoramento e ajuste de desempenho  
  
|Tópico| Tarefa|  
|-----------|----------------------|  
|[Monitorar componentes do SQL Server](../../relational-databases/performance/monitor-sql-server-components.md)|As etapas necessárias para monitorar qualquer componente do SQL Server.|  
|[Ferramentas para monitoramento e ajuste de desempenho](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)|Lista as ferramentas de monitoramento e ajuste disponíveis no SQL Server.|  
|[Estabelecer uma linha de base de desempenho](../../relational-databases/performance/establish-a-performance-baseline.md)|Como estabelecer uma linha de base de desempenho.|  
|[Isolar problemas de desempenho](../../relational-databases/performance/isolate-performance-problems.md)|Isole problemas de desempenho do banco de dados.|  
|[Identificar afunilamentos](../../relational-databases/performance/identify-bottlenecks.md)|Monitorar e acompanhar o desempenho de servidor para identificar afunilamentos.|  
|[Monitoramento de desempenho e atividade de servidor](../../relational-databases/performance/server-performance-and-activity-monitoring.md)|Usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e as ferramentas de monitoramento de desempenho e atividades do Windows.|  
|[Exibir e salvar planos de execução](../../relational-databases/performance/display-and-save-execution-plans.md)|Exiba e salve os planos de execução em um arquivo em formato XML.|  
|[Estatísticas de consulta dinâmica](../../relational-databases/performance/live-query-statistics.md)|Exiba estatísticas em tempo real sobre as etapas de execução da consulta.|  
|[Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)|Usar o Repositório de Consultas para capturar automaticamente um histórico das consultas, planos e estatísticas de tempo de execução e os mantém para sua análise.|  
|[Como usar o Repositório de Consultas com OLTP in-memory](../../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)|Considerações sobre tabelas com otimização de memória.|  
|[Melhor prática com o Repositório de Consultas](../../relational-databases/performance/best-practice-with-the-query-store.md)|Recomendações sobre como usar o Repositório de Consultas.|  
  
## <a name="see-also"></a>Consulte também  
 [Administração automatizada em toda a empresa](http://msdn.microsoft.com/library/44d8365b-42bd-4955-b5b2-74a8a9f4a75f)   
 [Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/database-engine-tuning-advisor.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
