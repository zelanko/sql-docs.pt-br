---
title: sys.dm_exec_query_optimizer_memory_gateways (Transact-SQL) | Microsoft Docs
description: Retorna o status atual de semáforos de recursos usado para limitar a otimização de consultas simultâneas
ms.custom: ''
ms.date: 04/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 33a3c8b0e1af48d9b93177045cc4d3eff3823f25
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43065165"
---
# <a name="sysdmexecqueryoptimizermemorygateways-transact-sql"></a>sys.dm_exec_query_optimizer_memory_gateways (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Retorna o status atual de semáforos de recursos usado para limitar a otimização de consultas simultâneas.

|coluna|Tipo|Description|  
|----------|---------------|-----------------|  
|**pool_id**|**int**|ID do pool de recursos sob o Resource Governor|  
|**name**|**sysname**|Compilar o nome de porta (Gateway pequeno, médio de Gateway, o Gateway grande)|
|**max_count**|**int**|A contagem máxima configurada de compilações simultâneas|
|**active_count**|**int**|A contagem de ativa no momento de compilações neste portão|
|**waiter_count**|**int**|O número de waiters neste portão|
|**threshold_factor**|**bigint**|Fator de limite que define a parte de máximo de memória usada pela otimização de consulta.  Para gateway pequeno, threshold_factor indica o uso de memória de otimizador máximo em bytes para uma consulta quando for necessário para obter um acesso no gateway pequeno.  Para o gateway de médio e grande threshold_factor mostra a parte da memória total do servidor disponível para essa porta. Ao calcular o limite de uso de memória para a porta, ele é usado como um divisor.|
|**threshold**|**bigint**|Memória próximo do limite em bytes.  A consulta é necessária para obter um acesso a esse gateway se seu consumo de memória atingir esse limite.  "-1" se a consulta não é necessário para obter um acesso a esse gateway.|
|**is_active**|**bit**|Se a consulta é necessário para passar a porta atual ou não.|


## <a name="permissions"></a>Permissões  
SQL Server requer a permissão VIEW SERVER STATE no servidor.

Banco de dados SQL do Azure requer a permissão VIEW DATABASE STATE no banco de dados.


## <a name="remarks"></a>Remarks  
SQL Server usa uma abordagem em camadas do gateway para limitar o número de compilações simultâneas permitidas.  Três gateways são usados, incluindo pequeno, médio e grande. Gateways de ajudam a evitar o esgotamento dos recursos de memória geral pelos maiores consumidores de necessidade de memória de compilação.

Aguarda um resultado de gateway na compilação atrasada. Atrasos na compilação, além de solicitações limitadas terá um RESOURCE_SEMAPHORE_QUERY_COMPILE associado acúmulo de tipo de espera. O tipo de espera RESOURCE_SEMAPHORE_QUERY_COMPILE pode indicar que consultas estão usando uma grande quantidade de memória para compilação e que a memória foi esgotada ou como alternativa, há memória suficiente disponível em geral, porém disponíveis unidades em uma determinada gateway foram esgotados. A saída de **sys.dm_exec_query_optimizer_memory_gateways** pode ser usado para solucionar problemas de cenários em que havia memória suficiente para compilar um plano de execução de consulta.  

## <a name="examples"></a>Exemplos  

### <a name="a-viewing-statistics-on-resource-semaphores"></a>A. Exibindo estatísticas de semáforos de recurso  
Quais são as estatísticas de gateway de memória de otimizador atuais para esta instância do SQL Server?

```  
SELECT [pool_id], [name], [max_count], [active_count],
       [waiter_count], [threshold_factor], [threshold],
       [is_active]
FROM sys.dm_exec_query_optimizer_memory_gateways;   

```  

## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](./system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](./execution-related-dynamic-management-views-and-functions-transact-sql.md)  
[Como usar o comando DBCC MEMORYSTATUS para monitorar o uso de memória no SQL Server 2005](https://support.microsoft.com/help/907877/how-to-use-the-dbcc-memorystatus-command-to-monitor-memory-usage-on-sql-server-2005)
[compilação de consulta grande aguarda RESOURCE_SEMAPHORE_QUERY_COMPILE no SQL Server 2014](https://support.microsoft.com/help/3024815/large-query-compilation-waits-on-resource-semaphore-query-compile-in-sql-server-2014)
