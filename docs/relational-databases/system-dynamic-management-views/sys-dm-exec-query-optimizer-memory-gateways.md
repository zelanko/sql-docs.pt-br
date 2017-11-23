---
title: sys.dm_exec_query_optimizer_memory_gateways (Transact-SQL) | Microsoft Docs
description: "Retorna o status atual do recurso semáforos usado para limitar a otimização de consultas simultâneas"
ms.custom: 
ms.date: 04/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_exec_query_optimizer_memory_gateways_TSQL
- dm_exec_query_optimizer_memory_gateways
- sys.dm_exec_query_optimizer_memory_gateways_TSQL
- sys.dm_exec_query_optimizer_memory_gateways
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_query_optimizer_memory_gateways dynamic management view
author: josack
ms.author: josack
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cf31a066798e1c88d0d6d475edda87f2df08ba05
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexecqueryoptimizermemorygateways-transact-sql"></a>sys.dm_exec_query_optimizer_memory_gateways (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Retorna o status atual do recurso semáforos usado para limitar a otimização de consultas simultâneas.

|Coluna|Tipo|Description|  
|----------|---------------|-----------------|  
|**pool_id**|**int**|ID do pool de recursos em administrador de recursos|  
|**name**|**sysname**|Compile o nome de porta (Gateway pequeno, médio Gateway, Gateway grande)|
|**max_count**|**int**|A contagem máxima configurada de compilações simultâneas|
|**active_count**|**int**|A contagem ativa no momento de compilações neste portão|
|**waiter_count**|**int**|O número de objetos waiter neste portão|
|**threshold_factor**|**bigint**|Fator de limite que define a parte de máximo de memória usada pela otimização de consulta.  Para o gateway pequeno, threshold_factor indica o uso de memória de otimizador máximo em bytes para uma consulta antes que seja necessária para acessar o gateway pequeno.  Para o gateway de médio e grande, threshold_factor mostra a parte da memória total do servidor disponível para essa porta. Ele é usado como um divisor ao calcular o limite de uso de memória para a porta.|
|**limite**|**bigint**|Memória próxima do limite em bytes.  A consulta é necessária para obter um acesso a este gateway se seu consumo de memória atingir esse limite.  "-1" se a consulta não é necessário para acessar a este gateway.|
|**is_active**|**bit**|Se a consulta é necessário para passar a porta atual ou não.|


## <a name="permissions"></a>Permissões  
SQL Server requer a permissão VIEW SERVER STATE no servidor.

Banco de dados SQL do Azure requer a permissão VIEW DATABASE STATE no banco de dados.


## <a name="remarks"></a>Comentários  
SQL Server usa uma abordagem em camadas do gateway para limitar o número de compilações simultâneas permitidas.  Três gateways são usados, incluindo pequeno, médio e grande. Gateways ajudam a evitar o esgotamento de recursos de memória geral maiores consumidores de necessidade de memória de compilação.

Espera-se em um resultado de gateway na compilação atrasada. Além de atrasos na compilação, solicitações limitadas terá um associado RESOURCE_SEMAPHORE_QUERY_COMPILE acúmulo do tipo de espera. O tipo de espera RESOURCE_SEMAPHORE_QUERY_COMPILE pode indicar que consultas estão usando uma grande quantidade de memória para a compilação e que a memória esgotada ou como alternativa há memória suficiente disponível em geral, porém disponíveis unidades em uma determinada gateway foram esgotados. A saída de **sys.dm_exec_query_optimizer_memory_gateways** pode ser usado para solucionar problemas de cenários em que havia memória suficiente para compilar um plano de execução de consulta.  

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
 [Funções e exibições de gerenciamento dinâmico &#40; relacionadas à execução Transact-SQL &#41;](./execution-related-dynamic-management-views-and-functions-transact-sql.md)  
[Como usar o comando DBCC MEMORYSTATUS para monitorar o uso de memória no SQL Server 2005](https://support.microsoft.com/help/907877/how-to-use-the-dbcc-memorystatus-command-to-monitor-memory-usage-on-sql-server-2005)
[compilação de consulta grande espera RESOURCE_SEMAPHORE_QUERY_COMPILE no SQL Server 2014](https://support.microsoft.com/help/3024815/large-query-compilation-waits-on-resource-semaphore-query-compile-in-sql-server-2014)
