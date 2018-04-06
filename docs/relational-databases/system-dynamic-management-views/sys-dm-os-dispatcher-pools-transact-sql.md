---
title: sys.dm_os_dispatcher_pools (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_dispatcher_pools_TSQL
- dm_os_dispatcher_pools
- sys.dm_os_dispatcher_pools
- sys.dm_os_dispatcher_pools_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- extended events [SQL Server], views
- sys.dm_os_dispatcher_pools DMV
ms.assetid: b9edbc83-c6bc-4753-9bb5-a454cfe7d6bf
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 44b6e630c1afe8360796656eca1d1814a92067e0
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/05/2018
---
# <a name="sysdmosdispatcherpools-transact-sql"></a>sys.dm_os_dispatcher_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre os pools de distribuidores da sessão. Os pools de distribuidores são pools de thread usados por componentes do sistema para executar processamento em segundo plano.  
  
> [!NOTE]  
>  Para chamar essa de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_dispatcher_pools**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|dispatcher_pool_address|**varbinary(8)**|O endereço do pool de distribuidores. dispatcher_pool_address é exclusivo. Não permite valor nulo.|  
|tipo|**nvarchar(256)**|Tipo de pool de distribuidores. Não permite valor nulo. Existem dois tipos de pools de distribuidores:<br /><br /> DISP_POOL_XE_ENGINE<br /><br /> DISP_POOL_XE_SESSION<br /><br /> O DMV para obter a lista completa de consulta|  
|nome|**nvarchar(256)**|Nome do pool de distribuidores. Não permite valor nulo.|  
|dispatcher_count|**Int**|Número de threads ativos de distribuidor. Não permite valor nulo.|  
|dispatcher_ideal_count|**Int**|Número de threads de distribuidor que o pool de distribuidores pode aumentar para usar. Não permite valor nulo.|  
|dispatcher_timeout_ms|**Int**|Período, em milissegundos, em que o distribuidor aguardará um novo trabalho antes de sair. Não permite valor nulo.|  
|dispatcher_waiting_count|**Int**|Número de threads ociosos de distribuidor. Não permite valor nulo.|  
|queue_length|**Int**|Número de itens de trabalho que aguardam para serem manipulados pelo pool de distribuidores. Não permite valor nulo.|  
|pdw_node_id|**Int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões

Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` no banco de dados.   

## <a name="see-also"></a>Consulte também  
  
  


