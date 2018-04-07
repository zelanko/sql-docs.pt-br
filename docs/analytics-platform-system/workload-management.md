---
title: Gerenciamento de carga de trabalho (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/12/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 69063b1a-a8f3-453a-83ab-afbe7eb4f463
caps.latest.revision: 11
ms.openlocfilehash: 6dde6c1af7b704e5bd1ed0e03516ad94f191ad9d
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="workload-management"></a>Gerenciamento de carga de trabalho
Recursos de gerenciamento de carga de trabalho do SQL Server PDW permitem que os usuários e administradores para atribuir solicitações pré-definir as configurações de memória e simultaneidade. Use o gerenciamento de carga de trabalho para melhorar o desempenho da carga de trabalho, consistente ou misto, permitindo solicitações para os recursos apropriados sem anteriores em todas as solicitações para sempre.  
  
Por exemplo, com as técnicas de gerenciamento de carga de trabalho no SQL Server PDW, você pode:  
  
-   Aloca um grande número de recursos para um trabalho de carregamento.  
  
-   Especifique mais recursos para a criação de um índice columnstore.  
  
-   Solucionar problemas de uma junção de hash desempenho lento para ver se ele precisa de mais memória e, em seguida, atribua a ele mais memória.  
  
## <a name="Basics"></a>Noções básicas de gerenciamento de carga de trabalho  
  
### <a name="key-terms"></a>Principais termos  
Gerenciamento de carga de trabalho  
*Gerenciamento de carga de trabalho* é a capacidade de entender e ajustar a utilização de recursos do sistema para obter o melhor desempenho de solicitações simultâneas.  
  
Classe de recurso  
No SQL Server PDW, um *classe de recurso* é uma função de servidor interna que tem pré-atribuídos limites de memória e simultaneidade. SQL Server PDW aloca recursos para solicitações de acordo com a associação de função de servidor de classe do recurso do logon que envia solicitações.  
  
Em nós de computação, a implementação de classes de recurso usa o recurso administrador de recursos no SQL Server. Para obter mais informações sobre o administrador de recursos, consulte [Resource Governor](http://msdn.microsoft.com/en-us/library/bb933866(v=sql.11).aspx) no MSDN.  
  
### <a name="understand-current-resource-utilization"></a>Compreender a utilização de recursos atual  
Para entender a utilização de recursos do sistema para as solicitações em execução no momento, use as exibições de gerenciamento dinâmico do SQL Server PDW. Por exemplo, você pode usar DMVs para entender se uma junção de hash grande com execução lenta pode se beneficiar de mais memória.  
  
<!-- MISSING LINKS
For examples, see [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md).  
-->
  
### <a name="adjust-resource-allocations"></a>Ajustar as alocações de recursos  
Para ajustar a utilização de recursos, altere a associação de classe de recurso do logon que está enviando a solicitação. As funções de servidor de classe de recurso são nomeadas **mediumrc**, **largerc**, e **xlargerc**. Eles representam alocações médio, grande e extra grande, respectivamente.  
  
Por exemplo, para alocar uma grande quantidade de recursos do sistema para uma solicitação, adicione o logon que está enviando a solicitação para o **largerc** função de servidor. A seguinte instrução ALTER SERVER ROLE adiciona o logon Anna à função de servidor largerc.  
  
```sql  
ALTER SERVER ROLE largerc ADD MEMBER Anna;  
```  
  
## <a name="RC"></a>Descrição da classe de recurso  
A tabela a seguir descreve as classes de recursos e suas alocações de recursos do sistema.  
  
|Classe de recurso|Importância da solicitação|Uso máximo de memória *|Slots de simultaneidade (máximo = 32)|Description|  
|------------------|----------------------|--------------------------|---------------------------------------|---------------|  
|padrão|Média|400 MB|1|Por padrão, cada logon é permitida uma pequena quantidade de memória e recursos de simultaneidade para suas solicitações.<br /><br />Quando um logon é adicionado a uma classe de recurso, a nova classe terá precedência. Quando um logon é descartado de todas as classes de recursos, o logon voltarão a alocação de recursos padrão.|  
|MediumRC|Média|1200 MB|3|Exemplos de solicitações que possam precisar de classe de recurso de mídia:<br /><br />Operações de CTAS que têm grande junções de hash.<br /><br />Selecione as operações que precisam de mais memória para evitar o cache em disco.<br /><br />Carregando dados em índices columnstore clusterizados.<br /><br />Compilando, recriar e reorganizar índices columnstore clusterizados para tabelas menores que 10 a 15 com.|  
|largerc|Alta|2.8 GB|7|Exemplos de solicitações que possam precisar de classe de recurso grande:<br /><br />Operações CTAS muito grandes que junções de hash grande ou contenham agregações grandes, como grandes cláusulas ORDER BY ou GROUP BY.<br /><br />Selecione as operações que exigem grandes quantidades de memória para operações como junções de hash ou agregações como cláusulas ORDER BY ou GROUP BY<br /><br />Carregando dados em índices columnstore clusterizados.<br /><br />Compilando, recriar e reorganizar índices columnstore clusterizados para tabelas menores que 10 a 15 com.|  
|xlargerc|Alta|8.4 GB|22|É a classe de recurso muito grande para solicitações que podem exigir o consumo de recursos muito tempo de execução.|  
  
<sup>*</sup>Uso máximo da memória é uma aproximação.  
  
### <a name="request-importance"></a>Importância da solicitação  
A importância de solicitação é mapeado para a quantidade de tempo de CPU que o SQL Server, em execução em nós de computação, dará a solicitações.  Solicitações com prioridade mais alta recebem mais tempo de CPU.  
  
### <a name="maximum-memory-usage"></a>Uso máximo da memória  
Uso máximo da memória é a quantidade máxima de memória disponível que pode ser usado por uma solicitação em cada espaço de processamento. Por exemplo uma solicitação de mediumrc pode usar até 1.200 MB para o processamento dentro de cada distribuição. É importante garantir que dados não são desviados para evitar que algumas distribuições de executar a maioria do trabalho.  
  
### <a name="concurrency-slots"></a>Slots de simultaneidade  
A meta de alocação de 1, 3, 7 e 22 slots de simultaneidade é permitir que os processos de pequenos e grandes sejam executadas ao mesmo tempo, sem bloquear o processo pequeno quando um grande processo está em execução.  Por exemplo, SQL Server PDW pode alocar o máximo de 32 slots de simultaneidade para executar 1 solicitação muito grande (22 slots), 1 solicitação grande (7 slots) e 1 solicitação média (3 slots) ao mesmo tempo.  
  
Exemplos de alocar até 32 slots de simultaneidade para solicitações simultâneas:  
  
-   28 slots = 4 grande  
  
-   30 slots = 10 médio  
  
-   32 slots = 32 padrão  
  
-   32 slots = 1 extra grande + 1 médio grande + 1  
  
-   32 slots = 2 médio grande + 4 + 6 padrão  
  
Suponha 6 solicitações grandes são enviadas ao SQL Server PDW, e, em seguida, 10 solicitações padrão são enviadas. SQL Server PDW processará as solicitações em ordem de prioridade da seguinte maneira:  
  
-   Alocar 28 slots de simultaneidade para iniciar o processamento 4 solicitações grandes, como memória se torna disponível e manter 2 solicitações grandes na fila.  
  
-   Alocar 4 slots de simultaneidade para iniciar o processamento de solicitações de padrão de 4 e manter 6 solicitações de padrão na fila de espera.  
  
Como concluir solicitações e slots de simultaneidade ficam disponíveis, PDW do SQL Server alocará as solicitações restantes de acordo com a prioridade e recursos disponíveis. Por exemplo, quando há simultaneidade 7 slots abrir, esperar solicitações grandes terá prioridade mais alta para 7 slots que solicitações médias de espera.  Se abrir 6 slots, SQL Server PDW alocará 6 solicitações mais tamanho padrão. No entanto, slots de memória e simultaneidade devem todas estar disponíveis antes do SQL Server PDW permite que uma solicitação executar.  
  
Em cada classe de recurso, as solicitações execute primeiro na ordem do primeiro a sair (PEPS).  
  
## <a name="GeneralRemarks"></a>Comentários gerais  
Se um logon for membro de mais de uma classe de recurso, a classe com a maioria dos recursos terá precedência.  
  
Quando um logon é adicionado ou removido de uma classe de recurso, a alteração entra em vigor imediatamente para todas as solicitações futuras; solicitações atuais que estão em execução ou aguardando não são afetadas. O logon não necessário desconectar e reconectar-se para que a alteração deverá ocorrer.  
  
Para cada logon, as configurações de classe de recurso são aplicadas às operações e instruções individuais e não à sessão.  
  
Antes de PDW do SQL Server executa uma instrução, ele tenta adquirir os slots de simultaneidade necessários para a solicitação. Se ele não é possível adquirir suficiente slots de simultaneidade, o SQL Server PDW passa a solicitação em um estado de espera para execução. Todo sistema de recursos que já foram alocados para a solicitação são retornados para o sistema.  
  
A maioria das instruções SQL sempre precisa de alocações de recursos padrão e, portanto, não é controladas pelas classes de recurso. Por exemplo, CREATE LOGIN só precisa de uma pequena quantidade de recursos e é alocado os recursos padrão, mesmo se o logon chamando CREATE LOGIN for um membro de uma classe de um recurso.  Por exemplo, se Ana é um membro da classe de recurso largerc e ela envia uma instrução CREATE LOGIN, a instrução CREATE LOGIN será executado com o número padrão de recursos.  
  
Instruções SQL e operações regidas pelas classes de recursos:  
  
-   ALTER INDEX REBUILD  
  
-   ALTER INDEX REORGANIZE  
  
-   RECRIAÇÃO DA TABELA DE ALTERAÇÃO  
  
-   CRIAR UM ÍNDICE CLUSTERIZADO  
  
-   CREATE CLUSTERED COLUMNSTORE INDEX  
  
-   CRIAR TABELA COMO SELECT  
  
-   CRIAR TABELA DE REMOTA COMO SELECT  
  
-   Carregamento de dados com **dwloader**.  
  
-   INSERT-SELECT  
  
-   UPDATE  
  
-   DELETE  
  
-   RESTAURAR banco de dados ao restaurar em um dispositivo com mais nós de computação.  
  
-   Selecione, excluindo as consultas de DMV  
  
## <a name="Limits"></a>Limitações e restrições  
As classes de recurso determinam as alocações de memória e simultaneidade.  Eles não controlam operações de entrada/saída.  
  
## <a name="Metadata"></a>Metadados  
DMVs que contêm informações sobre classes de recursos e membros de classe de recurso.  
  
-   [sys.server_role_members](../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
-   [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
DMVs que contêm informações sobre o estado das solicitações e os recursos que exigem:  
  
-   [sys.dm_pdw_lock_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
-   [sys.dm_pdw_resource_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
Exibições do sistema relacionados expostas DMVs SQL Server em nós de computação. Consulte [exibições de gerenciamento dinâmico do SQL Server](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) para obter links para esses DMVs no MSDN.  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys.dm_pdw_nodes_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys.dm_pdw_nodws_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_exec_sessions  
  
-   sys.dm_pdw_nodes_exec_requests  
  
-   sys.dm_pdw_nodes_exec_query_memory_grants  
  
-   sys.dm_pdw_nodes_exec_query_resource_semaphores  
  
-   sys.dm_pdw_nodes_os_memory_brokers  
  
-   sys.dm_pdw_nodes_os_memory_cache_entries  
  
-   sys.dm_pdw_nodes_exec_cached_plans  
  
## <a name="RelatedTasks"></a>Tarefas relacionadas  
[Tarefas de gerenciamento de carga de trabalho](workload-management-tasks.md)  
  
<!-- MISSING LINKS
See the Workload Management section of [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md) for the following tasks:  
  
1.  Find the number of active requests for each resource group.  
  
2.  Determine if my requests need more memory  
  
3.  Determine if there are a high number of query optimizations or suboptimal plan generations.  
  
4.  Determine Average CPU time per request in each resource pool to date  
  
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
