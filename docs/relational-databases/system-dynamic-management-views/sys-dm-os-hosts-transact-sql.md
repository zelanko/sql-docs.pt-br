---
title: sys.dm_os_hosts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_hosts_TSQL
- dm_os_hosts
- dm_os_hosts_TSQL
- sys.dm_os_hosts
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_hosts dynamic management view
ms.assetid: a313ff3b-1fe9-421e-b94b-cea19c43b0e5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 43083d569ca8f06571ce52445b2a2d9c2bb6178e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63047850"
---
# <a name="sysdmoshosts-transact-sql"></a>sys.dm_os_hosts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna todos os hosts registrados atualmente em uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta exibição também retorna os recursos usados por esses hosts.  
  
> [!NOTE]  
>  Chamá-lo partir [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_hosts**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**host_address**|**varbinary(8)**|Endereço de memória interna do objeto de host.|  
|**type**|**nvarchar(60)**|Tipo de componente hospedado. Por exemplo,<br /><br /> SOSHOST_CLIENTID_SERVERSNI= SQL Server Native Interface<br /><br /> SOSHOST_CLIENTID_SQLOLEDB = SQL Server Native Client OLE DB Provider<br /><br /> SOSHOST_CLIENTID_MSDART = Microsoft Data Access Run Time|  
|**name**|**nvarchar(32)**|Nome do host.|  
|**enqueued_tasks_count**|**int**|Número total de tarefas que o host colocou nas filas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**active_tasks_count**|**int**|Número de tarefas em execução atualmente que o host colocou nas filas.|  
|**completed_ios_count**|**int**|Número total de E/S emitidas e concluídas por meio deste host.|  
|**completed_ios_in_bytes**|**bigint**|Contagem total de bytes das E/S concluídas por meio deste host.|  
|**active_ios_count**|**int**|Número total de solicitações de E/S relacionadas a este host que neste momento está aguardando conclusão.|  
|**default_memory_clerk_address**|**varbinary(8)**|Endereço da memória do objeto de administrador de memória associado a este host. Para obter mais informações, consulte [DM os_memory_clerks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).|  
|**pdw_node_id**|**int**|**Aplica-se ao**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões

Na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Na [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` permissão no banco de dados.   

## <a name="remarks"></a>Comentários  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite que os componentes, como um provedor OLE DB, que não fazem parte de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executável, aloquem memória e participem de programação não preemptiva. Esses componentes são hospedados por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e todos os recursos alocados por eles são controlados. A hospedagem permite que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possa cuidar mais dos recursos usados por componentes externos para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executável.  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
|De|Para|Relação|  
|----------|--------|------------------|  
|sys.dm_os_hosts. default_memory_clerk_address|sys.dm_os_memory_clerks. memory_clerk_address|um para um|  
|sys.dm_os_hosts. host_address|sys.dm_os_memory_clerks. host_address|um para um|  
  
## <a name="examples"></a>Exemplos  
 O exemplo seguinte determina a quantidade total de memória confirmada por um componente hospedado.  
  
||  
|-|  
|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
```  
SELECT h.type, SUM(mc.pages_kb) AS commited_memory  
FROM sys.dm_os_memory_clerks AS mc   
INNER JOIN sys.dm_os_hosts AS h   
    ON mc.memory_clerk_address = h.default_memory_clerk_address  
GROUP BY h.type;  
```  
  
## <a name="see-also"></a>Consulte também  

 [sys.dm_os_memory_clerks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)   
 [Sistema operacional SQL Server relacionados exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


