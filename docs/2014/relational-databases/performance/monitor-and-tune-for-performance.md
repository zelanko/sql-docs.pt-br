---
title: Monitorar e ajustar o desempenho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 683e8044b235828741fe429f133af82d1977031a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63150711"
---
# <a name="monitor-and-tune-for-performance"></a>Monitorar e ajustar o desempenho
  A meta do monitoramento de bancos de dados é avaliar o desempenho do servidor. Um monitoramento eficaz envolve a criação de instantâneos periódicos do desempenho atual para isolar processos que estão ocasionando problemas, e a coleta contínua de dados para o controle das tendências de desempenho.  
  
 A avaliação contínua do desempenho de banco de dados ajuda a minimizar tempos de resposta e a maximizar a taxa de transferência, permitindo alcançar desempenho ótimo. Tráfego de rede, E/S de disco e uso de CPU eficientes são fundamentais para um desempenho ótimo. É preciso analisar minuciosamente os requisitos de aplicativos, compreender a estrutura lógica e física dos dados, avaliar o uso de banco de dados e negociar compensações entre usos conflitantes, tais como a do processamento de transações online (OLTP) versus o apoio à decisão.  
  
## <a name="benefits-of-monitoring-and-tuning-databases-for-performance"></a>Benefícios de monitorar e ajustar bancos de dados para desempenho  
 O Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o sistema operacional Microsoft Windows fornecem utilitários que lhe permitem visualizar a condição atual do banco de dados e rastrear o desempenho conforme as condições mudam. Há uma variedade de ferramentas e técnicas que podem ser usadas para monitorar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Compreender como monitorar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ajudá-lo a:  
  
-   Determinar se o desempenho pode ser melhorado. Por exemplo, ao monitorar os tempos de resposta a consultas utilizadas com frequência, é possível determinar se são necessárias alterações na consulta ou nos índices das tabelas.  
  
-   Avaliar a atividade de usuário. Por exemplo, monitorando os usuários que tentam se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é possível determinar se a segurança está configurada adequadamente e testar aplicativos ou sistemas de desenvolvimento. Por exemplo, monitorando consultas SQL à medida que são executadas, é possível determinar se estão escritas corretamente e produzindo os resultados esperados.  
  
-   Solucionar eventuais problemas ou depurar componentes de aplicativos, como procedimentos armazenados.  
  
### <a name="monitoring-in-a-dynamic-environment"></a>Monitorando em um ambiente dinâmico  
 Monitorar é importante porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece serviço em um ambiente dinâmico. Mudanças nas condições resultam em alterações no desempenho. Em suas avaliações, você poderá consultar alterações no desempenho à medida que o número de usuários aumenta, o acesso de usuário e os métodos de conexões mudam, o conteúdo do banco de dados cresce, os aplicativos cliente se modificam, os dados nos aplicativos se alteram, as consultas se tornam mais complexas e o tráfego de rede aumenta. Usando as ferramentas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para monitorar o desempenho, é possível associar algumas alterações no desempenho a mudanças de condições e consultas complexas. Os seguintes cenários constituem exemplos:  
  
-   Monitorando os tempos de resposta a consultas utilizadas com frequência, é possível determinar se são necessárias alterações na consulta ou nos índices das tabelas em que as consultas são executadas.  
  
-   Monitorando consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] à medida que são executadas, é possível determinar se elas estão escritas corretamente e produzindo os resultados esperados.  
  
-   Monitorando os usuários que tentam se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é possível determinar se a segurança está configurada adequadamente e testar aplicativos ou sistemas de desenvolvimento.  
  
 O tempo de resposta é o tempo necessário para que a primeira linha do conjunto de resultados seja retornada para o usuário, na forma de uma confirmação visual de que uma consulta está sendo processada. A taxa de transferência é o número total de consultas manipuladas pelo servidor durante um período de tempo especificado.  
  
 À medida que o número de usuário aumenta, aumenta a competição por recursos do servidor, o que, por sua vez, aumenta o tempo de resposta e diminui o processamento global.  
  
## <a name="monitoring-and-tuning-performance-tasks"></a>Monitorando e ajustando tarefas de desempenho  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|[Monitorar componentes do SQL Server](monitor-sql-server-components.md)|Fornece as etapas necessárias exigida para monitorar com eficácia qualquer componente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Ferramentas para monitoramento e ajuste de desempenho](performance-monitoring-and-tuning-tools.md)|Lista as ferramentas de monitoramento e ajuste do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Estabelecer uma linha de base de desempenho](establish-a-performance-baseline.md)|Fornece informações sobre como estabelecer uma linha de base de desempenho.|  
|[Isolar problemas de desempenho](isolate-performance-problems.md)|Descreve como isolar problemas de desempenho de banco de dados.|  
|[Identificar afunilamentos](identify-bottlenecks.md)|Descreve como monitorar e acompanhar o desempenho de servidor para identificar gargalos.|  
|[Monitoramento de desempenho e atividade de servidor](server-performance-and-activity-monitoring.md)|Descreve como usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e as ferramentas de monitoramento de desempenho e atividades do Windows.|  
|[Exibir e salvar planos de execução](display-and-save-execution-plans.md)|Descreve como exibir e salvar planos de execução em um arquivo em formato XML.|  
|[Monitorando o desempenho com o repositório de consultas](monitoring-performance-by-using-the-query-store.md)|O Armazenamento de Consulta captura automaticamente um histórico das consultas, planos e estatísticas de tempo de execução e os mantém para sua análise.|  
  
## <a name="see-also"></a>Consulte também  
 [Administração automatizada em toda a empresa](../../ssms/agent/automated-administration-across-an-enterprise.md)   
 [Orientador de Otimização do Mecanismo de Banco de Dados](database-engine-tuning-advisor.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
