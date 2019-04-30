---
title: Gerenciamento de carga de trabalho no Analytics Platform System | Microsoft Docs
description: Gerenciamento de carga de trabalho no Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2281262c086f4d8dcab27debc8bb735ea5e8e1ba
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63157467"
---
# <a name="workload-management-in-analytics-platform-system"></a>Gerenciamento de carga de trabalho no Analytics Platform System

Recursos de gerenciamento de carga de trabalho do SQL Server PDW permitem que os usuários e administradores para atribuir solicitações pré-definir configurações de memória e simultaneidade. Use o gerenciamento de carga de trabalho para melhorar o desempenho da carga de trabalho, consistente ou misto, permitindo que solicitações para os recursos apropriados sem privando todas as solicitações para sempre.  
  
Por exemplo, com as técnicas de gerenciamento de carga de trabalho no SQL Server PDW, você pode:  
  
-   Aloca um grande número de recursos para um trabalho de carregamento.  
  
-   Especifique mais recursos para a criação de um índice columnstore.  
  
-   Solucionar problemas de uma junção de hash de desempenho lento para ver se ele precisa de mais memória e, em seguida, dê a ele mais memória.  
  
## <a name="Basics"></a>Noções básicas de gerenciamento de carga de trabalho  
  
### <a name="key-terms"></a>Principais termos  
Gerenciamento de carga de trabalho  
*Gerenciamento de carga de trabalho* é a capacidade de entender e ajustar a utilização de recursos do sistema para obter o melhor desempenho para solicitações simultâneas.  
  
Classe de recurso  
No SQL Server PDW, uma *classe de recurso* é uma função de servidor interna que tem limites predefinidos para a memória e simultaneidade. SQL Server PDW aloca recursos para solicitações de acordo com a associação de função de servidor de classe do recurso do logon que envia as solicitações.  
  
Em nós de computação, a implementação de classes de recurso usa o recurso de administrador de recursos no SQL Server. Para obter mais informações sobre o Resource Governor, consulte [Resource Governor](../relational-databases/resource-governor/resource-governor.md) no MSDN.  
  
### <a name="understand-current-resource-utilization"></a>Entender a utilização de recursos atual  
Para entender a utilização de recursos do sistema para as solicitações em execução no momento, use as exibições de gerenciamento dinâmico do SQL Server PDW. Por exemplo, você pode usar DMVs para entender se uma junção de hash grande de execução lenta poderia se beneficiar de mais memória.  
  
<!-- MISSING LINKS
For examples, see [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md).  
-->
  
### <a name="adjust-resource-allocations"></a>Ajustar as alocações de recursos  
Para ajustar a utilização de recursos, altere a associação de classe de recurso do logon que está enviando a solicitação. As funções de servidor de classe de recurso são nomeadas **mediumrc**, **largerc**, e **xlargerc**. Eles representam as alocações de recursos de médio, grande e extra grande, respectivamente.  
  
Por exemplo, para alocar uma grande quantidade de recursos do sistema para uma solicitação, adicione o logon que está enviando a solicitação para o **largerc** função de servidor. A instrução alterar função de servidor a seguir adiciona o logon Anna à função de servidor largerc.  
  
```sql  
ALTER SERVER ROLE largerc ADD MEMBER Anna;  
```  
  
## <a name="RC"></a>Descrições de classes de recurso  
A tabela a seguir descreve as classes de recursos e suas alocações de recursos do sistema.  
  
|Classe de recurso|Importância da solicitação|Uso máximo da memória *|Slots de simultaneidade (máximo = 32)|Descrição|  
|------------------|----------------------|--------------------------|---------------------------------------|---------------|  
|padrão|Média|400 MB|1|Por padrão, cada logon é permitida uma pequena quantidade de memória e recursos de simultaneidade para suas solicitações.<br /><br />Quando um logon é adicionado a uma classe de recurso, a nova classe terá precedência. Quando um logon é descartado de todas as classes de recursos, o logon reverterá para a alocação de recurso padrão.|  
|MediumRC|Média|1200 MB|3|Exemplos de solicitações que talvez seja necessário a classe de recursos de mídia:<br /><br />Operações de CTAS que tenham grandes junções de hash.<br /><br />Selecione as operações que precisam de mais memória para evitar o armazenamento em cache em disco.<br /><br />Carregar dados em índices columnstore clusterizados.<br /><br />Compilar, recompilar e reorganizar índices de columnstore clusterizado para tabelas menores com 10 a 15 colunas.|  
|Largerc|Alta|2,8 GB|7|Exemplos de solicitações que talvez seja necessário a classe de recurso grande:<br /><br />Operações de CTAS muito grandes que junções de hash grande ou que contêm agregações grandes, como grandes cláusulas ORDER BY ou GROUP BY.<br /><br />Selecione as operações que exigem grandes quantidades de memória para operações como junções de hash ou agregações como cláusulas ORDER BY ou GROUP BY<br /><br />Carregar dados em índices columnstore clusterizados.<br /><br />Compilar, recompilar e reorganizar índices de columnstore clusterizado para tabelas menores com 10 a 15 colunas.|  
|xlargerc|Alta|8.4 GB|22|É a classe de recurso muito grande para solicitações que podem exigir o consumo de recurso muito grande em tempo de execução.|  
  
<sup>*</sup>Uso máximo da memória é uma aproximação.  
  
### <a name="request-importance"></a>Importância da solicitação  
A importância de solicitação é mapeado para a quantidade de tempo de CPU que o SQL Server, em execução em nós de computação, dará às solicitações.  Solicitações com prioridade mais alta recebem mais tempo de CPU.  
  
### <a name="maximum-memory-usage"></a>Uso máximo da memória  
Uso máximo da memória é a quantidade máxima de memória disponível, que uma solicitação pode usar dentro de cada espaço de processamento. Por exemplo uma solicitação de mediumrc pode usar até 1200 MB para o processamento em cada distribuição. Ele ainda é importante garantir que dados não estiverem distorcidos para evitar a necessidade de algumas distribuições que executou a maioria do trabalho.  
  
### <a name="concurrency-slots"></a>Slots de simultaneidade  
A meta da alocação de 1, 3, 7 e slots de simultaneidade 22 é permitir que os processos de grandes e pequeno porte sejam executados ao mesmo tempo, sem bloquear pequeno processo quando um processo grande está sendo executado.  Por exemplo, o PDW do SQL Server pode alocar no máximo 32 slots de simultaneidade para executar 1 solicitação extra grande (22 slots), 1 solicitação grande (7 slots) e 1 solicitação médio (3 slots) ao mesmo tempo.  
  
Exemplos de alocar até 32 slots de simultaneidade para solicitações simultâneas:  
  
-   slots de 28 = 4 grandes  
  
-   slots de 30 = Média 10  
  
-   32 slots = 32 padrão  
  
-   32 slots = 1 extra grande + 1 médio grande + 1  
  
-   32 slots = 2 médio grande + 4 + 6 padrão  
  
Suponha que 6 grandes solicitações são enviadas ao SQL Server PDW e, em seguida, 10 solicitações de padrão são enviadas. SQL Server PDW processará as solicitações em ordem de prioridade da seguinte maneira:  
  
-   Alocar 28 slots de simultaneidade para iniciar o processamento de solicitações grandes 4 como a memória disponível e manter 2 grandes solicitações na fila.  
  
-   Alocar 4 slots de simultaneidade para iniciar o processamento de solicitações de padrão de 4 e manter as 6 solicitações padrão na fila de espera.  
  
Conforme as solicitações de término e slots de simultaneidade se tornam disponíveis, o SQL Server PDW alocará as solicitações restantes de acordo com os recursos disponíveis e prioridade. Por exemplo, quando há abrir slots de simultaneidade 7, esperar grandes solicitações terão prioridade mais alta para os 7 slots que solicitações médio em espera.  Se abrir 6 slots, SQL Server PDW alocará 6 solicitações mais tamanho padrão. No entanto, slots de memória e simultaneidade devem todos estar disponíveis antes do SQL Server PDW permite que uma solicitação executar.  
  
Dentro de cada classe de recurso, as solicitações são executadas primeiro na ordem primeiro a sair (PEPS).  
  
## <a name="GeneralRemarks"></a>Comentários gerais  
Se um logon for membro de mais de uma classe de recurso, a classe com a maioria dos recursos terá precedência.  
  
Quando um logon é adicionado ou removido de uma classe de recurso, a alteração entra em vigor imediatamente para todas as solicitações futuras; solicitações atuais que estão em execução ou aguardando não são afetadas. O logon não precisa desconectar e reconectar-se para a alteração ocorrer.  
  
Para cada logon, as configurações de classe de recurso são aplicadas às operações e instruções individuais e não à sessão.  
  
Antes de PDW do SQL Server executa uma instrução, ele tenta adquirir os slots de simultaneidade necessários para a solicitação. Se ele não é possível adquirir os slots de simultaneidade suficientes, o SQL Server PDW passa a solicitação em um estado de espera para executado. Sistema de recursos de todos os que já foram alocados para a solicitação são retornados para o sistema.  
  
A maioria das instruções SQL sempre precisa de alocações de recursos padrão e, portanto, não é controlada pelas classes de recursos. Por exemplo, CREATE LOGIN só precisa de uma pequena quantidade de recursos e é alocado os recursos padrão, mesmo que o logon chamando CREATE LOGIN é um membro de uma classe de recurso.  Por exemplo, se Anna é um membro da classe de recurso largerc e ela envia uma instrução CREATE LOGIN, executará a instrução CREATE LOGIN com o número padrão de recursos.  
  
Instruções SQL e operações governadas por classes de recursos:  
  
-   ALTER INDEX REBUILD  
  
-   ALTER INDEX REORGANIZE  
  
-   RECOMPILAÇÃO DA TABELA DE ALTERAÇÃO  
  
-   CRIAR UM ÍNDICE CLUSTERIZADO  
  
-   CREATE CLUSTERED COLUMNSTORE INDEX  
  
-   CREATE TABLE AS SELECT  
  
-   CREATE REMOTE TABLE AS SELECT  
  
-   Carregamento de dados com **dwloader**.  
  
-   INSERT-SELECT  
  
-   UPDATE  
  
-   DELETE  
  
-   RESTAURAR banco de dados ao restaurar em um dispositivo com mais nós de computação.  
  
-   Selecione, excluindo as consultas de DMV  
  
## <a name="Limits"></a>Limitações e restrições  
As classes de recursos controlam alocações de memória e simultaneidade.  Eles não controlam as operações de entrada/saída.  
  
## <a name="Metadata"></a>Metadados  
DMVs que contêm informações sobre classes de recursos e membros de classe de recurso.  
  
-   [sys.server_role_members](../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
-   [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
DMVs que contêm informações sobre o estado de solicitações e os recursos que exigem:  
  
-   [sys.dm_pdw_lock_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
-   [sys.dm_pdw_resource_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
Exibições do sistema relacionadas expostas a partir de DMVs do SQL Server em nós de computação. Ver [exibições de gerenciamento dinâmico do SQL Server](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) para obter links para esses DMVs no MSDN.  
  
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
  
