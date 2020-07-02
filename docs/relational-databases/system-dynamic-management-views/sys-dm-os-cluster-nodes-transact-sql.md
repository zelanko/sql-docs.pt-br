---
title: sys. dm_os_cluster_nodes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 384cfd63e613b419f87cac7ca60454ddd8a3c90c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754212"
---
# <a name="sysdm_os_cluster_nodes-transact-sql"></a>sys.dm_os_cluster_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha para cada nó na configuração de instância de cluster de failover. Se a instância atual for uma instância clusterizada, ela retornará uma lista de nós nos quais essa instância de cluster de failover (anteriormente "servidor virtual") foi definida. Se a instância de servidor atual não for uma instância clusterizada de failover, ela retornará um conjunto de linhas vazio.  
  
> **Observação:** Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use o nome **Sys. dm_pdw_nodes_os_cluster_nodes**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**NodeName**|**sysname**|Nome de um nó na configuração da instância clusterizada de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (servidor virtual).|  
|status|**int**|Status do nó em uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância de cluster de failover: 0, 1, 2, 3,-1. Para obter mais informações, consulte [função GetClusterNodeState](https://go.microsoft.com/fwlink/?LinkId=204794).|  
|status_description|**nvarchar (20)**|Descrição do status do nó de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 0 = ativo<br /><br /> 1 = inativo<br /><br /> 2 = pausado<br /><br /> 3 = unindo<br /><br /> -1 = desconhecido|  
|is_current_owner|bit|1 indica que este nó é o proprietário atual do recurso de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|pdw_node_id|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="remarks"></a>Comentários  
 Quando o clustering de failover está habilitado, a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser executada em qualquer um dos nós do cluster de failover que são criados como parte da instância de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (servidor virtual).  
  
> **Observação:** Essa exibição substitui a função fn_virtualservernodes, que será preterida em uma versão futura.  
  
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
|Node3|1|ligar|0|  
  
## <a name="see-also"></a>Consulte Também  
 [sys. dm_os_cluster_properties &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-properties-transact-sql.md)   
 [sys. dm_io_cluster_shared_drives &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md)   
 [sys. fn_virtualservernodes &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-virtualservernodes-transact-sql.md)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  



