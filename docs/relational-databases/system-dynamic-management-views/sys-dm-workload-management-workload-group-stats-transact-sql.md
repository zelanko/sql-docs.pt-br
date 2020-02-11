---
title: sys. dm_workload_management_workload_groups_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/02/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: = azure-sqldw-latest||= sqlallproducts-allversions
ms.openlocfilehash: 6e77239d019cb51e66a34a3a5b909e01c28a7faa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73633430"
---
# <a name="sysdm_workload_management_workload_groups_stats-transact-sql"></a>sys. dm_workload_management_workload_groups_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Retorna estatísticas do grupo de carga de trabalho e os valores efetivos [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]do grupo de cargas de trabalho no.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|group_id|**int**|ID exclusivo do grupo de carga de trabalho.||
|name|**sysname**|Nome do grupo de carga de trabalho.||
|statistics_start_time|**datetime**|Hora em que a coleta de estatísticas começou para o grupo de carga de trabalho.  O valor é quando o grupo de cargas de trabalho foi criado ou quando a instância é pausada ou dimensionada.||
|total_request_count|**bigint**|Conta cumulativa de solicitações concluídas no grupo de carga de trabalho.||
|total_shared_resource_reqeusts|**bigint**|Contagem cumulativa de solicitações concluídas no grupo de cargas de trabalho que usavam recursos do pool compartilhado.||
|total_queued_request_count|**bigint**|Contagem cumulativa de solicitações enfileiradas após o limite de max_concurrency atingido.||
|total_request_execution_timeouts|**bigint**|Contagem cumulativa de solicitações no grupo de cargas de trabalho que atingiram o tempo limite antes da conclusão com base na configuração de query_execution_timeout_sec.||
|effective_min_percentage_resource|**tinyint**|A configuração min_percentage_resource efetiva permitida Considerando o nível de serviço e as configurações do grupo de carga de trabalho. Os min_percentage_resource efetivos podem ser ajustados em níveis mais baixos de serviço.  Por exemplo, em DW100c, o menor min_percentage_resource permitido é 25%.  O min_percentage_resource será ajustado para 0% se o valor não puder ser concedido no nível de serviço.  Por exemplo, min_percentage_resource definido como 10% em DW6000c, teria um effective_min_percentage_resource de 0% quando reduzido para DW100c.||
|effective_cap_percentage_resource|**tinyint**|O cap_percentage_resource efetivo para o grupo de carga de trabalho.  Se houver outros grupos de cargas de trabalho com min_percentage_resource > 0, a effective_cap_percentage_resource será reduzida proporcionalmente.||
|effective_request_min_resource_grant_percent|**decimal (5, 2)**|O valor de tempo de execução efetivo para request_min_resource_grant_percent do grupo de carga de trabalho. O valor efetivo Considerando o nível de serviço e como o grupo de carga de trabalho é configurado.  Se min_percentage_resource for ajustado por causa do nível de serviço, effective_request_min_resource_grant_percent será ajustado de acordo.||
|effective_request_max_resource_grant_percent|**decimal (5, 2)**|O valor de tempo de execução efetivo para request_max_resource_grant_percent do grupo de carga de trabalho Considerando a configuração de todos os grupos de carga de trabalho.||
|||||

## <a name="see-also"></a>Confira também

 [Exibições de gerenciamento dinâmico de SQL Data Warehouse e paralelo data warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
