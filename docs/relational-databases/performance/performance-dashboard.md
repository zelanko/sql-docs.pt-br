---
title: Painel de Desempenho | Microsoft Docs
ms.custom: ''
ms.date: 12/14/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- performance dashboard [SQL Server]
- performance dashboard reports
- perf dashboard
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753e
author: pelopes
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 0372e215646640f1f587964cddd8a302894e633d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754493"
---
# <a name="performance-dashboard"></a>Painel de Desempenho
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] versão 17.2 e posteriores incluem o Painel de Desempenho. Este painel foi projetado para fornecer visualmente insights rápidos sobre o estado de desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (no [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] em diante) e da Instância Gerenciada do [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]. 

O Painel de Desempenho ajuda a identificar rapidamente se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] está passando por um gargalo de desempenho. Se for encontrado um gargalo, capture facilmente dados de diagnóstico adicionais que podem ser necessários para resolver o problema. Alguns problemas comuns de desempenho que o Painel de Desempenho pode ajudar a identificar incluem:
-  Gargalos de CPU (e quais consultas estão consumindo a maior parte da CPU)
-  Gargalos de E/S (e quais consultas estão realizando a maior parte da E/S)
-  Recomendações de índice geradas pelo Otimizador de Consulta (índices ausentes)
-  Bloqueio
-  Contenção de recursos (incluindo a contenção de trava)

O Painel de Desempenho também ajuda a identificar consultas dispendiosas executadas antes e várias métricas estão disponíveis para definir o alto custo: CPU, Gravações Lógicas, Leituras Lógicas, Duração, Leituras Físicas e Tempo do CLR.

O painel de desempenho é dividido nas seções e sub-relatórios a seguir:
-  Utilização da CPU do Sistema
-  Solicitações em Espera Atuais
-  Atividade Atual
   -  Solicitações do Usuário
   -  Sessões do Usuário
   -  Taxa de Acertos do Cache
-  informações Históricas
   -  Esperas
   -  Travas
   -  Estatísticas de E/S
   -  Consultas Dispendiosas
- Informações Diversas
  -  Rastreamentos Ativos
  -  Sessões do Active xEvent
  -  Bancos de dados
  -  Índices Ausentes

> [!NOTE] 
> Internamente, o Painel de Desempenho usa DMVs (Exibições de Gerenciamento Dinâmico) e DMFs (Funções de Gerenciamento Dinâmico) relacionadas a [Execução](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md), [Índice](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md) e [E/S](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md).

## <a name="to-view-the-performance-dashboard"></a>Para exibir o Painel de Desempenho 
  
Para exibir o Painel de Desempenho, clique com o botão direito do mouse no nome da instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Pesquisador de Objetos, selecione **Relatórios**, **Relatórios Padrão** e clique em **Painel de Desempenho**.  
  
![Painel de Desempenho no menu](../../relational-databases/performance/media/perf_dashboard_ssms.png "Painel de Desempenho no menu")  
  
O Painel de Desempenho será exibido como uma nova guia. Abaixo está um exemplo em que um gargalo de CPU está claramente presente:  
  
![Tela principal do Painel de Desempenho](../../relational-databases/performance/media/perf_dashboard.png "Tela principal do Painel de Desempenho")  
  
## <a name="remarks"></a>Comentários
O relatório **Índices Ausentes** mostra os índices potencialmente ausentes que o Otimizador de Consulta identificou durante a compilação da consulta. No entanto, essas recomendações não devem ser interpretadas pelo valor nominal. A Microsoft recomenda que índices com pontuação maior que 100.000 sejam avaliados para criação, uma vez que eles têm o maior aprimoramento previsto para consultas do usuário. 

> [!TIP]
> Sempre avalie se uma nova sugestão de índice é comparável a um índice existente na mesma tabela, em que os mesmos resultados práticos podem ser obtidos simplesmente alterando um índice existente, em vez de criar um novo índice. Por exemplo, dado um novo índice sugerido nas colunas C1, C2 e C3, primeiro avalie se há um índice existente nas colunas C1 e C2. Nesse caso, pode ser preferível simplesmente adicionar a coluna C3 ao índice existente (preservando a ordem das colunas preexistentes) para evitar a criação de um novo índice.
> Para obter mais informações, confira o [Guia de Design e Arquitetura de Índice](../../relational-databases/sql-server-index-design-guide.md).

O relatório **Esperas** filtra todas as esperas ociosas e suspensas. Para obter mais informações sobre esperas, confira [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) e [Ajuste de desempenho do SQL Server 2005 usando esperas e filas](https://download.microsoft.com/download/4/7/a/47a548b9-249e-484c-abd7-29f31282b04d/performance_tuning_waits_queues.doc).

Os relatórios de **Consultas Dispendiosas** são redefinidos quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é reiniciado, pois os dados nas DMVs subjacentes são desmarcados. Do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] em diante, informações detalhadas sobre consultas dispendiosas podem ser encontradas no Repositório de Consultas. 

> [!NOTE]
> O Painel de Desempenho foi inicialmente lançado como um download autônomo para [SQL Server 2005](https://techcommunity.microsoft.com/t5/SQL-Server-Support/SQL-Server-2005-Performance-Dashboard-Reports/ba-p/315415) e depois atualizado para [SQL Server 2012](https://www.microsoft.com/download/details.aspx?id=29063).

## <a name="permissions"></a>Permissões  
Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], requer permissões `VIEW SERVER STATE` e `ALTER TRACE`. Em [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)], requer a permissão `VIEW DATABASE STATE` no banco de dados.

## <a name="see-also"></a>Consulte Também  
 [Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [Ferramentas para monitoramento e ajuste de desempenho](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [Abrir o Monitor de Atividade &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)     
 [Monitor de atividade](../../relational-databases/performance-monitor/activity-monitor.md)     
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
