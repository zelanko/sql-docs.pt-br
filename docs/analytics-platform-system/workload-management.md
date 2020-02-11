---
title: Gerenciamento de carga de trabalho
description: Gerenciamento de carga de trabalho no Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: d14714cb23a9f6b0d6cc63ddca5049cb6741017c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74399440"
---
# <a name="workload-management-in-analytics-platform-system"></a>Gerenciamento de carga de trabalho no Analytics Platform System

Os recursos de gerenciamento de carga de trabalho de SQL Server PDW permitem que usuários e administradores atribuam solicitações para configurações predefinidas de memória e simultaneidade. Use o gerenciamento de carga de trabalho para melhorar o desempenho de sua carga de trabalho, seja consistente ou mista, permitindo que as solicitações tenham os recursos apropriados sem a falta de nenhuma solicitação para sempre.  
  
Por exemplo, com as técnicas de gerenciamento de carga de trabalho no SQL Server PDW, você pode:  
  
-   Aloque um grande número de recursos para um trabalho de carga.  
  
-   Especifique mais recursos para criar um índice columnstore.  
  
-   Solucione um problema de hash de execução lenta para ver se ele precisa de mais memória e, em seguida, dê a ele mais memória.  
  
## <a name="Basics"></a>Noções básicas de gerenciamento de carga de trabalho  
  
### <a name="key-terms"></a>Principais termos  
Gerenciamento da Carga de Trabalho  
O *Gerenciamento de carga de trabalho* é a capacidade de entender e ajustar a utilização de recursos do sistema a fim de obter o melhor desempenho para solicitações simultâneas.  
  
Classe de recurso  
No SQL Server PDW, uma *classe de recurso* é uma função de servidor interna que tem limites previamente atribuídos para memória e simultaneidade. SQL Server PDW aloca recursos para solicitações de acordo com a associação de função de servidor de classe de recurso do logon que envia as solicitações.  
  
Nos nós de computação, a implementação das classes de recurso usa o recurso Resource Governor no SQL Server. Para obter mais informações sobre Resource Governor, consulte [resource governor](../relational-databases/resource-governor/resource-governor.md) no msdn.  
  
### <a name="understand-current-resource-utilization"></a>Entender a utilização atual de recursos  
Para entender a utilização de recursos do sistema para as solicitações em execução no momento, use as exibições de gerenciamento dinâmico SQL Server PDW. Por exemplo, você pode usar DMVs para entender se uma junção de hash grande de execução lenta poderia se beneficiar com a existência de mais memória.  
  
<!-- MISSING LINKS
For examples, see [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md).  
-->
  
### <a name="adjust-resource-allocations"></a>Ajustar alocações de recursos  
Para ajustar a utilização de recursos, altere a associação de classe de recurso do logon que está enviando a solicitação. As funções de servidor da classe de recurso são nomeadas **mediumrc**, **largerc**e **xlargerc**. Elas representam alocações de recursos muito grandes, grandes e extras, respectivamente.  
  
Por exemplo, para alocar uma grande quantidade de recursos do sistema a uma solicitação, adicione o logon que está enviando a solicitação para a função de servidor **largerc** . A instrução ALTER SERVER ROLE a seguir adiciona o logon Anna à função de servidor largerc.  
  
```sql  
ALTER SERVER ROLE largerc ADD MEMBER Anna;  
```  
  
## <a name="RC"></a>Descrições de classe de recurso  
A tabela a seguir descreve as classes de recurso e suas alocações de recursos do sistema.  
  
|Classe de recurso|Importância da solicitação|Uso máximo de memória *|Slots de simultaneidade (máximo = 32)|DESCRIÇÃO|  
|------------------|----------------------|--------------------------|---------------------------------------|---------------|  
|padrão|Média|400 MB|1|Por padrão, cada logon é permitido uma pequena quantidade de memória e recursos de simultaneidade para suas solicitações.<br /><br />Quando um logon é adicionado a uma classe de recurso, a nova classe tem precedência. Quando um logon é Descartado de todas as classes de recurso, o logon reverte para a alocação de recursos padrão.|  
|MediumRC|Média|1200 MB|3|Exemplos de solicitações que podem precisar da classe de recurso médio:<br /><br />Operações CTAS que têm grandes junções de hash.<br /><br />Selecione operações que precisam de mais memória para evitar o cache em disco.<br /><br />Carregando dados em índices columnstore clusterizados.<br /><br />Criação, recriação e reorganização de índices columnstore clusterizados para tabelas menores que têm 10-15 colunas.|  
|Largerc|Alta|2,8 GB|7|Exemplos de solicitações que podem precisar da classe de recurso grande:<br /><br />Operações CTAS muito grandes que têm enormes junções de hash ou que contêm grandes agregações, como cláusulas grandes ORDER BY ou GROUP BY.<br /><br />Selecione operações que exigem quantidades muito grandes de memória para operações como junções de hash ou agregações, como cláusulas ORDENAr por ou GROUP BY<br /><br />Carregando dados em índices columnstore clusterizados.<br /><br />Criação, recriação e reorganização de índices columnstore clusterizados para tabelas menores que têm 10-15 colunas.|  
|xlargerc|Alta|8,4 GB|22|A classe extra grande de recursos é para solicitações que podem exigir consumo extra de recursos grandes em tempo de execução.|  
  
<sup>*</sup>O uso máximo de memória é uma aproximação.  
  
### <a name="request-importance"></a>Importância da solicitação  
A importância da solicitação é mapeada para a quantidade de tempo de CPU que SQL Server, em execução nos nós de computação, fornecerá as solicitações.  As solicitações com prioridade mais alta recebem mais tempo de CPU.  
  
### <a name="maximum-memory-usage"></a>Uso máximo de memória  
O uso máximo de memória é a quantidade máxima de memória disponível que uma solicitação pode usar dentro de cada espaço de processamento. Por exemplo, uma solicitação mediumrc pode usar até 1200 MB para processamento em cada distribuição. Ainda é importante garantir que os dados não sejam distorcidos a fim de evitar que algumas distribuições executem a maior parte do trabalho.  
  
### <a name="concurrency-slots"></a>Slots de simultaneidade  
A meta de alocar slots de simultaneidade de 1, 3, 7 e 22 é permitir que processos grandes e pequenos sejam executados ao mesmo tempo, sem bloquear processos pequenos quando um processo grande está em execução.  Por exemplo, SQL Server PDW pode alocar no máximo 32 slots de simultaneidade para executar uma solicitação grande extra (22 slots), uma solicitação grande (7 slots) e uma solicitação média (3 slots) ao mesmo tempo.  
  
Exemplos de alocação de até 32 slots de simultaneidade para solicitações simultâneas:  
  
-   28 slots = 4 grandes  
  
-   30 slots = 10 média  
  
-   32 slots = 32 padrão  
  
-   32 slots = 1 extra grande + 1 grande + 1 média  
  
-   32 slots = 2 grandes + 4 padrão médio + 6  
  
Suponha que 6 solicitações grandes sejam enviadas para SQL Server PDW e 10 solicitações padrão sejam enviadas. SQL Server PDW processará as solicitações em ordem de prioridade da seguinte maneira:  
  
-   Aloque 28 slots de simultaneidade para iniciar o processamento 4 solicitações grandes à medida que a memória se torna disponível e mantenha duas solicitações grandes na fila.  
  
-   Aloque 4 slots de simultaneidade para iniciar o processamento de 4 solicitações padrão e manter 6 solicitações padrão na fila de espera.  
  
À medida que as solicitações forem concluídas e os slots de simultaneidade forem disponibilizados, SQL Server PDW alocará as solicitações restantes de acordo com os recursos e a prioridade disponíveis. Por exemplo, quando há 7 Slots de simultaneidade abertos, a espera de solicitações grandes terá prioridade mais alta para os 7 slots do que a espera de solicitações médias.  Se 6 slots forem abertos, SQL Server PDW alocará 6 mais solicitações de tamanho padrão. No entanto, os slots de memória e simultaneidade devem estar disponíveis antes que SQL Server PDW permita a execução de uma solicitação.  
  
Dentro de cada classe de recurso, as solicitações são executadas na ordem primeiro a entrar primeiro a sair (FIFO).  
  
## <a name="GeneralRemarks"></a>Comentários gerais  
Se um logon for membro de mais de uma classe de recurso, a classe com a maioria dos recursos terá precedência.  
  
Quando um logon é adicionado ou descartado de uma classe de recurso, a alteração entra em vigor imediatamente para todas as solicitações futuras; as solicitações atuais que estão em execução ou aguardando não são afetadas. O logon não precisa ser desconectado e reconectado para que a alteração ocorra.  
  
Para cada logon, as configurações de classe de recurso são aplicadas a instruções e operações individuais, e não à sessão.  
  
Antes que SQL Server PDW execute uma instrução, ele tenta adquirir os slots de simultaneidade necessários para a solicitação. Se ele não puder adquirir slots de simultaneidade suficientes, SQL Server PDW moverá a solicitação para um estado de espera de execução. Todos os recursos do sistema que já foram alocados para a solicitação são retornados para o sistema.  
  
A maioria das instruções SQL sempre precisa das alocações de recursos padrão e, portanto, não são controladas por classes de recursos. Por exemplo, CREATE LOGIN precisa apenas de uma pequena quantidade de recursos e é alocado os recursos padrão mesmo se o logon que chama CREATE LOGIN for um membro de uma classe de recurso.  Por exemplo, se Anna for um membro da classe de recurso largerc e enviar uma instrução CREATE LOGIN, a instrução CREATE LOGIN será executada com o número padrão de recursos.  
  
Instruções e operações SQL governadas por classes de recursos:  
  
-   ALTER INDEX REBUILD  
  
-   ALTER INDEX REORGANIZE  
  
-   ALTER TABLE REBUILD  
  
-   CRIAR ÍNDICE CLUSTERIZADO  
  
-   CREATE CLUSTERED COLUMNSTORE INDEX  
  
-   CREATE TABLE AS SELECT  
  
-   CRIAR TABELA REMOTA COMO SELECT  
  
-   Carregando dados com **dwloader**.  
  
-   INSERT-SELECT  
  
-   UPDATE  
  
-   Delete (excluir)  
  
-   Restaure o banco de dados ao restaurar em um dispositivo com mais nós de computação.  
  
-   SELECIONAR, excluindo consultas somente DMV  
  
## <a name="Limits"></a>Limitações e Restrições  
As classes de recurso regem a memória e as alocações de simultaneidade.  Eles não controlam as operações de entrada/saída.  
  
## <a name="Metadata"></a>Metadados  
DMVs que contêm informações sobre classes de recursos e membros de classe de recurso.  
  
-   [sys.server_role_members](../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
-   [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
DMVs que contêm informações sobre o estado das solicitações e os recursos que eles precisam:  
  
-   [sys.dm_pdw_lock_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
-   [sys.dm_pdw_resource_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
Exibições do sistema relacionadas expostas dos DMVs SQL Server nos nós de computação. Consulte [SQL Server exibições de gerenciamento dinâmico](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) para obter links para esses DMVS no msdn.  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys.dm_pdw_nodes_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys. dm_pdw_nodws_resource_governor_workload_groups  
  
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
  
