---
description: sys. dm_pdw_resource_waits (Transact-SQL)
title: sys. dm_pdw_resource_waits (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/26/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a43ce9a2-5261-41e3-97f0-555ba05ebed9
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: cf3b21433a4eb19be526487e9df03a8df7bce276
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474670"
---
# <a name="sysdm_pdw_resource_waits-transact-sql"></a>sys. dm_pdw_resource_waits (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Exibe informações de espera para todos os tipos de recurso no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] .  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|Posição da solicitação na lista de espera.|ordinal baseado em 0. Isso não é exclusivo em todas as entradas de espera.|  
|session_id|**nvarchar(32)**|ID da sessão na qual o estado de espera ocorreu.|Consulte session_id em [Sys. dm_pdw_exec_sessions &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|type|**nvarchar(255)**|Tipo de espera que essa entrada representa.|Valores possíveis:<br /><br /> Conexão<br /><br /> Simultaneidade de consultas locais<br /><br /> Simultaneidade de consultas distribuídas<br /><br /> Simultaneidade de DMS<br /><br /> Simultaneidade de backup|  
|object_type|**nvarchar(255)**|Tipo de objeto que é afetado pela espera.|Valores possíveis:<br /><br /> **OBJETO**<br /><br /> **BANCO**<br /><br /> **SYSTEM**<br /><br /> **ESQUEMA**<br /><br /> **APLICATIVO**|  
|object_name|**nvarchar (386)**|Nome ou GUID do objeto especificado que foi afetado pela espera.|Tabelas e exibições são exibidas com nomes de três partes.<br /><br /> Os índices e as estatísticas são exibidos com nomes de quatro partes.<br /><br /> Nomes, entidades de segurança e bancos de dados são nomes de cadeia de caracteres.|  
|request_id|**nvarchar(32)**|ID da solicitação na qual o estado de espera ocorreu.|QID o identificador da solicitação.<br /><br /> Identificador GUID para solicitações de carregamento.|  
|request_time|**datetime**|Hora em que o bloqueio ou o recurso foi solicitado.||  
|acquire_time|**datetime**|Hora em que o bloqueio ou o recurso foi adquirido.||  
|state|**nvarchar(50)**|Estado do estado de espera.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|Prioridade do item em espera.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|concurrency_slots_used|**int**|Interna|Consulte o [monitorar as esperas de recursos](#monitor-resource-waits) abaixo|  
|resource_class|**nvarchar (20)**|Interna |Consulte o [monitorar as esperas de recursos](#monitor-resource-waits) abaixo|  
  
## <a name="monitor-resource-waits"></a>Monitorar esperas de recursos 
Com a introdução de [grupos de cargas de trabalho](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-workload-isolation), os slots de simultaneidade não são mais aplicáveis.  Use a consulta abaixo e a `resources_requested` coluna para entender os recursos necessários para executar a solicitação.

```sql
select rw.wait_id
      ,rw.session_id
      ,rw.type
      ,rw.object_type
      ,rw.object_name
      ,rw.request_id
      ,rw.request_time
      ,rw.acquire_time
      ,rw.state
      ,resources_requested = s.effective_request_min_resource_grant_percent
      ,r.group_name
  from sys.dm_workload_management_workload_groups_stats s
  join sys.dm_pdw_exec_requests r on r.group_name = s.name collate SQL_Latin1_General_CP1_CI_AS
  join sys.dm_pdw_resource_waits rw on rw.request_id = r.request_id
```

## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico de SQL Data Warehouse e paralelo data warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
