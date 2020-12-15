---
description: sys.dm_workload_management_workload_groups_stats (Transact-SQL)
title: sys.dm_workload_management_workload_groups_stats (Transact-SQL) | Microsoft Docs
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
monikerRange: = azure-sqldw-latest
ms.openlocfilehash: 89daf919af43c130c23477596e34d6a19654fd12
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474757"
---
# <a name="sysdm_workload_management_workload_groups_stats-transact-sql"></a>sys.dm_workload_management_workload_groups_stats (Transact-SQL)
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

Retorna estatísticas do grupo de carga de trabalho e os valores efetivos do grupo de cargas de trabalho no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] .  
  
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

## <a name="see-also"></a>Consulte também

 [Exibições de gerenciamento dinâmico do Azure Synapse Analytics e Parallel data warehouse &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
