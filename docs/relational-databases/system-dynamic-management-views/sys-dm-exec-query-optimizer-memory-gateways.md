---
title: sys. dm_exec_query_optimizer_memory_gateways (Transact-SQL)
description: Retorna o status atual dos semáforos de recursos usados para restringir a otimização de consultas simultâneas
ms.custom: seo-dt-2019
ms.date: 04/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: language-reference
f1_keywords:
- dm_exec_query_optimizer_memory_gateways_TSQL
- dm_exec_query_optimizer_memory_gateways
- sys.dm_exec_query_optimizer_memory_gateways_TSQL
- sys.dm_exec_query_optimizer_memory_gateways
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_optimizer_memory_gateways dynamic management view
author: josack
ms.author: josack
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 01b0a68658112ebde642dde3f9c1fa0fb1d73c57
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734736"
---
# <a name="sysdm_exec_query_optimizer_memory_gateways-transact-sql"></a>sys. dm_exec_query_optimizer_memory_gateways (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asdw](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asdw.md)]

Retorna o status atual dos semáforos de recursos usados para restringir a otimização de consultas simultâneas.

|Coluna|Tipo|Description|  
|----------|---------------|-----------------|  
|**pool_id**|**int**|ID do pool de recursos em Resource Governor|  
|**name**|**sysname**|Nome da porta de compilação (gateway pequeno, gateway médio, gateway grande)|
|**max_count**|**int**|A contagem máxima configurada de compilações simultâneas|
|**active_count**|**int**|A contagem ativa atualmente de compilações neste portão|
|**waiter_count**|**int**|O número de aguardadores nesta porta|
|**threshold_factor**|**bigint**|Fator de limite que define a parte máxima da memória usada pela otimização de consulta.  Para o gateway pequeno, threshold_factor indica o uso máximo de memória do otimizador em bytes para uma consulta antes de ser necessário para obter um acesso no gateway pequeno.  Para o gateway médio e grande, threshold_factor mostra a parte da memória total do servidor disponível para esse portão. Ele é usado como um divisor ao calcular o limite de uso de memória para a porta.|
|**threshold**|**bigint**|Próximo limite de memória em bytes.  A consulta é necessária para obter um acesso a esse gateway se seu consumo de memória atingir esse limite.  "-1" se a consulta não for necessária para obter um acesso a esse gateway.|
|**is_active**|**bit**|Se a consulta é necessária para passar o portão atual ou não.|


## <a name="permissions"></a>Permissões  
SQL Server requer a permissão VIEW SERVER STATE no servidor.

O banco de dados SQL do Azure requer a permissão VIEW DATABASE STATE no banco de dados.


## <a name="remarks"></a>Comentários  
SQL Server usa uma abordagem de gateway em camadas para limitar o número de compilações simultâneas permitidas.  São usados três gateways, incluindo pequeno, médio e grande. Os gateways ajudam a evitar o esgotamento de recursos de memória geral por uma maior memória de compilação, exigindo consumidores.

Aguarda um resultado de gateway em compilação atrasada. Além dos atrasos na compilação, as solicitações limitadas terão uma acumulação de RESOURCE_SEMAPHORE_QUERY_COMPILE de tipo de espera associada. O tipo de espera RESOURCE_SEMAPHORE_QUERY_COMPILE pode indicar que as consultas estão usando uma grande quantidade de memória para compilação e que a memória foi esgotada ou, como alternativa, há memória suficiente disponível em geral, no entanto, as unidades disponíveis em um gateway específico foram esgotadas. A saída de **Sys. dm_exec_query_optimizer_memory_gateways** pode ser usada para solucionar problemas de cenários em que não havia memória suficiente para compilar um plano de execução de consulta.  

## <a name="examples"></a>Exemplos  

### <a name="a-viewing-statistics-on-resource-semaphores"></a>a. Exibindo estatísticas em semáforos de recursos  
Quais são as estatísticas de gateway de memória do otimizador atual para esta instância do SQL Server?

```  
SELECT [pool_id], [name], [max_count], [active_count],
       [waiter_count], [threshold_factor], [threshold],
       [is_active]
FROM sys.dm_exec_query_optimizer_memory_gateways;   

```  

## <a name="see-also"></a>Consulte Também  
 [Funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](./system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](./execution-related-dynamic-management-views-and-functions-transact-sql.md)  
[Como usar o comando DBCC MEMORYSTATUS para monitorar o uso de memória no SQL Server 2005](https://support.microsoft.com/help/907877/how-to-use-the-dbcc-memorystatus-command-to-monitor-memory-usage-on-sql-server-2005) 
 A [compilação de consulta grande aguarda RESOURCE_SEMAPHORE_QUERY_COMPILE no SQL Server 2014](https://support.microsoft.com/help/3024815/large-query-compilation-waits-on-resource-semaphore-query-compile-in-sql-server-2014)
