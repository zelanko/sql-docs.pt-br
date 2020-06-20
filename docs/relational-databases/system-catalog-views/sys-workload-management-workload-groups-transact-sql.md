---
title: sys. workload_management_workload_groups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/05/2019
ms.prod: sql
ms.technology: system-objects
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: b103ff109c946262367467673da0bf9c8ef8f5eb
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85011427"
---
# <a name="sysworkload_management_workload_groups-transact-sql"></a>sys. workload_management_workload_groups (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

 Retorna detalhes para grupos de cargas de trabalho.  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|
|group_id|**int**|ID exclusivo do grupo de carga de trabalho. Não permite valor nulo.||
|name|**sysname**|Nome do grupo de carga de trabalho. Deve ser exclusivo para a instância.  Não permite valor nulo.||
|importance|**nvarchar(128)**|É a importância relativa de uma solicitação neste grupo de carga de trabalho e entre grupos de carga de trabalho para recursos compartilhados. Não permite valor nulo.|baixa, below_normal, normal (padrão), above_normal, alta||
|min_percentage_resource|**tinyint**|Quantidade garantida de recursos para solicitações no grupo de cargas de trabalho. Os recursos não são compartilhados com outros grupos de carga de trabalho. Não permite valor nulo.||
|cap_percentage_resource|**tinyint**|Limite de alocação de porcentagem de recursos para solicitações no grupo de cargas de trabalho. Limita o número máximo de recursos alocados para o nível especificado. O intervalo permitido para o valor é de 1 a 100.||
|request_min_resource_grant_percent|**decimal (5, 2)**|Especifica a quantidade mínima de recursos alocados a uma solicitação. O intervalo permitido para value é de 0,75 a 100.||
|request_max_resource_grant_percent |**decimal (5, 2)**|Especifica a quantidade máxima de recursos alocados a uma solicitação.||
|query_execution_timeout_sec|**int**|A quantidade de tempo de execução, em segundos, permitida antes que a consulta seja cancelada.  As consultas não podem ser canceladas depois que atingirem a fase de retorno da execução.  query_execution_timeout_sec não inclui o tempo gasto na fila.|
|query_wait_timeout_sec|**int**|INTERNAL||
|create_time|**datetime**|Hora em que o grupo de cargas de trabalho foi criado. Não permite valor nulo.||
modify_time|**datetime**|Hora em que o grupo de cargas de trabalho foi modificado pela última vez. Não permite valor nulo.||
|&nbsp;||||
  
## <a name="permissions"></a>Permissões

Requer a permissão VIEW SERVER STAT.

## <a name="next-steps"></a>Próximas etapas

 Para obter uma lista de todas as exibições de catálogo para SQL Data Warehouse e data warehouse paralelo, consulte [exibições de catálogo SQL data warehouse e parallel data warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md). Para criar um grupo de carga de trabalho, consulte [Criar grupo de carga de trabalho](../../t-sql/statements/create-workload-group-transact-sql.md). Para obter mais informações sobre a classificação de carga de trabalho, consulte [isolamento de carga de trabalho](/azure/sql-data-warehouse/sql-data-warehouse-workload-isolation)
