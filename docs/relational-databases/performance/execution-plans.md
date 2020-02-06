---
title: Planos de execução | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- query plans [SQL Server]
- execution plans [SQL Server]
- query execution plans
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753f
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 9bf75c2d176c4ea2c596f29f1ddda910e794ae12
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68232025"
---
# <a name="execution-plans"></a>Planos de execução
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Para poder executar consultas, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] deve analisar a instrução para determinar a maneira mais eficiente de acessar os dados necessários. Essa análise é tratada por um componente chamado de Otimizador de Consulta. A entrada do Otimizador de Consulta consiste em uma consulta, o esquema de banco de dados (definições de tabela e de índice) e as estatísticas de banco de dados. A saída do Otimizador de Consulta é um plano de execução de consulta, às vezes chamado de plano de consulta ou apenas de plano de execução.   

Um plano de execução de consulta é uma definição do seguinte: 

* A sequência em que as tabelas de origem são acessadas.  
  Normalmente, há muitas sequências pelas quais o servidor de banco de dados pode acessar as tabelas base para criar o conjunto de resultados. Por exemplo, se uma instrução `SELECT` fizesse referência a três tabelas, o servidor de banco de dados poderia acessar `TableA`primeiro, usar os dados de `TableA` para extrair as linhas correspondentes de `TableB`e usar os dados de `TableB` para extrair dados de `TableC`. As outras sequências em que o servidor de banco de dados poderia acessar as tabelas são:  
  `TableC`, `TableB`, `TableA`ou  
  `TableB`, `TableA`, `TableC`ou  
  `TableB`, `TableC`, `TableA`ou  
  `TableC`, `TableA`, `TableB`  

* Os métodos usados para extrair dados de cada tabela.  
  Geralmente, há métodos diferentes para acessar os dados em cada tabela. Se forem necessárias apenas algumas linhas com valores de chave específicos, o servidor de banco de dados poderá usar um índice. Se forem necessárias todas as linhas da tabela, o servidor de banco de dados poderá ignorar os índices e executar um exame na tabela. Se forem necessárias todas as linhas de uma tabela, mas houver um índice cujas colunas de chave estão em um `ORDER BY`, executando um exame de índice em vez de um exame de tabela, uma classificação separada do conjunto de resultados poderá ser salva. Se uma tabela for muito pequena, os exames de tabela poderão ser o método mais eficiente para quase todos os acessos à tabela.

> [!TIP]
> Para obter mais informações sobre o processamento de consultas e planos de execução de consulta, confira [Guia da Arquitetura de Processamento de Consultas](../../relational-databases/query-processing-architecture-guide.md).

## <a name="in-this-section"></a>Nesta seção  
  
-   [Infraestrutura de Criação de Perfil de Consulta](../../relational-databases/performance/query-profiling-infrastructure.md)  
  
-   [Exibir e salvar planos de execução](../../relational-databases/performance/display-and-save-execution-plans.md)  
  
-   [Comparar e analisar planos de execução](../../relational-databases/performance/compare-and-analyze-execution-plans.md)  

-   [Guias de plano](../../relational-databases/performance/plan-guides.md)  

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
