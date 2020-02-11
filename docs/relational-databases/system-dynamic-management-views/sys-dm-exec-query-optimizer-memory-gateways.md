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
ms.openlocfilehash: 5720617f6652a8acb1ab8b6daf0e5e8919a86f8b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74165001"
---
# <a name="sysdm_exec_query_optimizer_memory_gateways-transact-sql"></a>sys. dm_exec_query_optimizer_memory_gateways (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Retorna o status atual dos semáforos de recursos usados para restringir a otimização de consultas simultâneas.

|Coluna|Type|DESCRIÇÃO|  
|----------|---------------|-----------------|  
|**pool_id**|**int**|ID do pool de recursos em Resource Governor|  
|**name**|**sysname**|Nome da porta de compilação (gateway pequeno, gateway médio, gateway grande)|
|**max_count**|**int**|A contagem máxima configurada de compilações simultâneas|
|**active_count**|**int**|A contagem ativa atualmente de compilações neste portão|
|**waiter_count**|**int**|O número de aguardadores nesta porta|
|**threshold_factor**|**bigint**|Fator de limite que define a parte máxima da memória usada pela otimização de consulta.  Para o gateway pequeno, threshold_factor indica o uso máximo de memória do otimizador em bytes para uma consulta antes de ser necessário para obter um acesso no gateway pequeno.  Para o gateway médio e grande, threshold_factor mostra a parte da memória total do servidor disponível para esse portão. Ele é usado como um divisor ao calcular o limite de uso de memória para a porta.|
|**os**|**bigint**|Próximo limite de memória em bytes.  A consulta é necessária para obter um acesso a esse gateway se seu consumo de memória atingir esse limite.  "-1" se a consulta não for necessária para obter um acesso a esse gateway.|
|**is_active**|**bit**|Se a consulta é necessária para passar o portão atual ou não.|


## <a name="permissions"></a>Permissões  
SQL Server requer a permissão VIEW SERVER STATE no servidor.

O banco de dados SQL do Azure requer a permissão VIEW DATABASE STATE no banco de dados.


## <a name="remarks"></a>Comentários  
SQL Server usa uma abordagem de gateway em camadas para limitar o número de compilações simultâneas permitidas.  São usados três gateways, incluindo pequeno, médio e grande. Os gateways ajudam a evitar o esgotamento de recursos de memória geral por uma maior memória de compilação, exigindo consumidores.

Aguarda um resultado de gateway em compilação atrasada. Além dos atrasos na compilação, as solicitações limitadas terão uma acumulação de RESOURCE_SEMAPHORE_QUERY_COMPILE de tipo de espera associada. O tipo de espera RESOURCE_SEMAPHORE_QUERY_COMPILE pode indicar que as consultas estão usando uma grande quantidade de memória para compilação e que a memória foi esgotada ou, como alternativa, há memória suficiente disponível em geral, no entanto, as unidades disponíveis em um determinado o gateway foi esgotado. A saída de **Sys. dm_exec_query_optimizer_memory_gateways** pode ser usada para solucionar problemas de cenários em que não havia memória suficiente para compilar um plano de execução de consulta.  

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
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](./system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](./execution-related-dynamic-management-views-and-functions-transact-sql.md)  
[Como usar o comando DBCC MEMORYSTATUS para monitorar o uso de memória na](https://support.microsoft.com/help/907877/how-to-use-the-dbcc-memorystatus-command-to-monitor-memory-usage-on-sql-server-2005)
[compilação de consulta grande do SQL Server 2005 aguarda RESOURCE_SEMAPHORE_QUERY_COMPILE no SQL Server 2014](https://support.microsoft.com/help/3024815/large-query-compilation-waits-on-resource-semaphore-query-compile-in-sql-server-2014)
