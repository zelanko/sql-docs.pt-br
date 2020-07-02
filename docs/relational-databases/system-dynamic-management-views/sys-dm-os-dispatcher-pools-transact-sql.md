---
title: sys. dm_os_dispatcher_pools (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6ec15e83ee3def969522963d757feeacfd2d5353
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754195"
---
# <a name="sysdm_os_dispatcher_pools-transact-sql"></a>sys.dm_os_dispatcher_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações sobre os pools de distribuidores da sessão. Os pools de distribuidores são pools de thread usados por componentes do sistema para executar processamento em segundo plano.  
  
> [!NOTE]  
>  Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use o nome **Sys. dm_pdw_nodes_os_dispatcher_pools**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|dispatcher_pool_address|**varbinary (8)**|O endereço do pool de distribuidores. dispatcher_pool_address é exclusivo. Não permite valor nulo.|  
|tipo|**nvarchar(256)**|Tipo de pool de distribuidores. Não permite valor nulo. Existem dois tipos de pools de distribuidores:<br /><br /> DISP_POOL_XE_ENGINE<br /><br /> DISP_POOL_XE_SESSION<br /><br /> Consultar o DMV para obter a lista completa|  
|name|**nvarchar(256)**|Nome do pool de distribuidores. Não permite valor nulo.|  
|dispatcher_count|**int**|Número de threads ativos de distribuidor. Não permite valor nulo.|  
|dispatcher_ideal_count|**int**|Número de threads de distribuidor que o pool de distribuidores pode aumentar para usar. Não permite valor nulo.|  
|dispatcher_timeout_ms|**int**|Período, em milissegundos, em que o distribuidor aguardará um novo trabalho antes de sair. Não permite valor nulo.|  
|dispatcher_waiting_count|**int**|Número de threads ociosos de distribuidor. Não permite valor nulo.|  
|queue_length|**int**|Número de itens de trabalho que aguardam para serem manipulados pelo pool de distribuidores. Não permite valor nulo.|  
|pdw_node_id|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="permissions"></a>Permissões

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   

## <a name="see-also"></a>Consulte Também  
  
  


