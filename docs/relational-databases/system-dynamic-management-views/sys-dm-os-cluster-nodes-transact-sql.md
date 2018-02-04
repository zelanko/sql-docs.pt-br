---
title: sys.dm_os_cluster_nodes (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_os_cluster_nodes_TSQL
- dm_os_cluster_nodes_TSQL
- dm_os_cluster_nodes
- sys.dm_os_cluster_nodes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_cluster_nodes dynamic management view
ms.assetid: 92fa804e-2d08-42c6-a36f-9791544b1d42
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d70e6512f4018c7cf5283e2cf3b93972edae6878
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmosclusternodes-transact-sql"></a>sys.dm_os_cluster_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada nó na configuração de instância de cluster de failover. Se a instância atual for uma instância clusterizada, ela retornará uma lista de nós nos quais essa instância de cluster de failover (anteriormente "servidor virtual") foi definida. Se a instância de servidor atual não for uma instância clusterizada de failover, ela retornará um conjunto de linhas vazio.  
  
> **Observação:** chamá-la de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_cluster_nodes**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**NodeName**|**sysname**|Nome de um nó na configuração da instância clusterizada de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (servidor virtual).|  
|status|**Int**|Status do nó de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância de cluster de failover: 0, 1, 2, 3, -1. Para obter mais informações, consulte [função GetClusterNodeState](http://go.microsoft.com/fwlink/?LinkId=204794).|  
|status_description|**nvarchar(20)**|Descrição do status do nó de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 0 = ativo<br /><br /> 1 = inativo<br /><br /> 2 = pausado<br /><br /> 3 = unindo<br /><br /> -1 = desconhecido|  
|is_current_owner|bit|1 indica que este nó é o proprietário atual do recurso de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|pdw_node_id|**Int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="remarks"></a>Remarks  
 Quando o clustering de failover está habilitado, a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser executada em qualquer um dos nós do cluster de failover que são criados como parte da instância de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (servidor virtual).  
  
> **Observação:** essa exibição substitui a função fn_virtualservernodes, que será preterida em uma versão futura.  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão VIEW SERVER STATE na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa sys. dm_os_cluster_nodes para retornar os nós em uma instância de servidor clusterizado.  
  
```  
SELECT NodeName, status, status_description, is_current_owner   
FROM sys.dm_os_cluster_nodes;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|NodeName|status|status_description|is_current_owner|  
|--------------|------------|-------------------------|------------------------|  
|node1|0|ativo|1|  
|node2|0|ativo|0|  
|Node3|1|inativo|0|  
  
## <a name="see-also"></a>Consulte também  
 [sys.dm_os_cluster_properties &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-properties-transact-sql.md)   
 [sys.dm_io_cluster_shared_drives &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md)   
 [sys.fn_virtualservernodes &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-virtualservernodes-transact-sql.md)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  



