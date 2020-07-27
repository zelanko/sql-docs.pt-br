---
title: Monitorar e ajustar o desempenho | Microsoft Docs
description: Saiba mais sobre como monitorar bancos de dados para avaliar o desempenho do servidor, usar instantâneos periódicos e reunir dados continuamente para acompanhar as tendências de desempenho.
ms.custom: ''
ms.date: 07/18/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
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
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7706c41442ee412cacea4e61b76a14ac7129d72f
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458863"
---
# <a name="monitor-and-tune-for-performance"></a>Monitorar e ajustar o desempenho
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  A meta do monitoramento de bancos de dados é avaliar o desempenho do servidor. Um monitoramento eficaz envolve a criação de instantâneos periódicos do desempenho atual para isolar processos que estão ocasionando problemas, e a coleta contínua de dados para o controle das tendências de desempenho.  
  
 A avaliação contínua do desempenho de banco de dados ajuda a minimizar tempos de resposta e a maximizar a taxa de transferência, permitindo alcançar desempenho ótimo. Tráfego de rede, E/S de disco e uso de CPU eficientes são fundamentais para um desempenho ótimo. É preciso analisar minuciosamente os requisitos de aplicativos, compreender a estrutura lógica e física dos dados, avaliar o uso de banco de dados e negociar compensações entre usos conflitantes, tais como a do processamento de transações online (OLTP) versus o apoio à decisão.  
  
## <a name="monitoring-and-tuning-databases-for-performance"></a>Monitorando e ajustando o desempenho de bancos de dados  
 O Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o sistema operacional Microsoft Windows fornecem utilitários que lhe permitem exibir a condição atual do banco de dados e acompanhar o desempenho conforme as condições mudam. Há uma variedade de ferramentas e técnicas que podem ser usadas para monitorar o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O monitoramento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ajuda a:  
  
-   Determinar se o desempenho pode ser melhorado. Por exemplo, ao monitorar os tempos de resposta a consultas utilizadas com frequência, é possível determinar se são necessárias alterações na consulta ou nos índices das tabelas.  
  
-   Avaliar a atividade de usuário. Por exemplo, monitorando os usuários que tentam se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é possível determinar se a segurança está configurada adequadamente e testar aplicativos ou sistemas de desenvolvimento. Por exemplo, monitorando consultas SQL à medida que são executadas, é possível determinar se estão escritas corretamente e produzindo os resultados esperados.  
  
-   Solucionar problemas ou depurar componentes de aplicativos, como procedimentos armazenados.  
  
## <a name="monitoring-in-a-dynamic-environment"></a>Monitorando em um ambiente dinâmico  
Mudanças nas condições resultam em alterações no desempenho. Em suas avaliações, você poderá consultar alterações no desempenho à medida que o número de usuários aumenta, o acesso de usuário e os métodos de conexões mudam, o conteúdo do banco de dados cresce, os aplicativos cliente se modificam, os dados nos aplicativos se alteram, as consultas se tornam mais complexas e o tráfego de rede aumenta. Com as ferramentas para monitorar o desempenho, é possível associar algumas alterações no desempenho a mudanças de condições e consultas complexas. **Exemplos:**  
  
-   Monitorando os tempos de resposta a consultas utilizadas com frequência, é possível determinar se são necessárias alterações na consulta ou nos índices das tabelas em que as consultas são executadas.  
  
-   Monitorando consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] à medida que são executadas, é possível determinar se elas estão escritas corretamente e produzindo os resultados esperados.  
  
-   Monitorando os usuários que tentam se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é possível determinar se a segurança está configurada adequadamente e testar aplicativos ou sistemas de desenvolvimento.  
  
O tempo de resposta é o tempo necessário para que a primeira linha do conjunto de resultados seja retornada para o usuário, na forma de uma confirmação visual de que uma consulta está sendo processada. A taxa de transferência é o número total de consultas manipuladas pelo servidor durante um período de tempo especificado.  
  
À medida que o número de usuário aumenta, aumenta a competição por recursos do servidor, o que, por sua vez, aumenta o tempo de resposta e diminui o processamento global.  
  
## <a name="monitoring-and-performance-tuning-tasks"></a>Tarefas de monitoramento e ajuste de desempenho  
  
|Tópico| Tarefa|  
|-----------|----------------------|  
|[Monitorar componentes do SQL Server](../../relational-databases/performance/monitor-sql-server-components.md)|Etapas necessárias para monitorar qualquer componente do SQL Server, como o Monitor de Atividade, Funções e Eventos Estendidos e Exibições de Gerenciamento Dinâmico, etc.|  
|[Ferramentas para monitoramento e ajuste de desempenho](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)|Lista as ferramentas de monitoramento e de ajuste disponíveis com o SQL Server, como Estatísticas de Consulta em Tempo Real e o Orientador de Otimização do Mecanismo de Banco de Dados.|  
|[Atualizando bancos de dados usando o Assistente de Ajuste de Consulta](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)|Mantenha a estabilidade do desempenho da carga de trabalho durante a atualização para o nível de compatibilidade do banco de dados mais recente.|  
|[Monitorando o desempenho com o Repositório de Consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)|Usar o Repositório de Consultas para capturar automaticamente um histórico das consultas, planos e estatísticas de runtime e os mantém para sua análise.|  
|[Estabelecer uma linha de base de desempenho](../../relational-databases/performance/establish-a-performance-baseline.md)|Como estabelecer uma linha de base de desempenho.|  
|[Isolar problemas de desempenho](../../relational-databases/performance/isolate-performance-problems.md)|Isole problemas de desempenho do banco de dados.|  
|[Identificar afunilamentos](../../relational-databases/performance/identify-bottlenecks.md)|Monitorar e acompanhar o desempenho de servidor para identificar gargalos.|  
|[Usar DMVs para determinar as estatísticas de uso e o desempenho das exibições](../../relational-databases/performance/use-dmvs-determine-usage-performance-views.md)|Aborda a metodologia e os scripts usados para obter informações sobre o desempenho de consultas.|  
|[Monitoramento de desempenho e atividade de servidor](../../relational-databases/performance/server-performance-and-activity-monitoring.md)|Usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e as ferramentas de monitoramento de desempenho e atividades do Windows.|  
|[Monitorar o uso de recursos](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)|Usando o Monitor do Sistema (também conhecido como perfmon) para medir o desempenho de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando contadores de desempenho.|  

  
## <a name="see-also"></a>Confira também  
 [Administração automatizada em toda a empresa](../../ssms/agent/automated-administration-across-an-enterprise.md)    
 [Comparar e analisar planos de execução](../../relational-databases/performance/compare-and-analyze-execution-plans.md)    
 [Exibir e salvar planos de execução](../../relational-databases/performance/display-and-save-execution-plans.md)    
  
  
