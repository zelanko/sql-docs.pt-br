---
description: sys.dm_os_hosts (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bc04cbc95d7b08903c596937bdec482311d29f63
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97321876"
---
# <a name="sysdm_os_hosts-transact-sql"></a>sys.dm_os_hosts (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna todos os hosts registrados atualmente em uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta exibição também retorna os recursos usados por esses hosts.  
  
> [!NOTE]  
>  Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use o nome **Sys.dm_pdw_nodes_os_hosts**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**host_address**|**varbinary (8)**|Endereço de memória interna do objeto de host.|  
|**tipo**|**nvarchar(60)**|Tipo de componente hospedado. Por exemplo:<br /><br /> SOSHOST_CLIENTID_SERVERSNI= SQL Server Native Interface<br /><br /> SOSHOST_CLIENTID_SQLOLEDB = SQL Server Native Client OLE DB Provider<br /><br /> SOSHOST_CLIENTID_MSDART = Microsoft Data Access Run Time|  
|**name**|**nvarchar(32)**|Nome do host.|  
|**enqueued_tasks_count**|**int**|Número total de tarefas que o host colocou nas filas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**active_tasks_count**|**int**|Número de tarefas em execução atualmente que o host colocou nas filas.|  
|**completed_ios_count**|**int**|Número total de E/S emitidas e concluídas por meio deste host.|  
|**completed_ios_in_bytes**|**bigint**|Contagem total de bytes das E/S concluídas por meio deste host.|  
|**active_ios_count**|**int**|Número total de solicitações de E/S relacionadas a este host que neste momento está aguardando conclusão.|  
|**default_memory_clerk_address**|**varbinary (8)**|Endereço da memória do objeto de administrador de memória associado a este host. Para obter mais informações, consulte [sys.dm_os_memory_clerks &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).|  
|**pdw_node_id**|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="permissions"></a>Permissões

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nos objetivos do serviço básico, S0 e S1 do banco de dados SQL, e para bancos de dados em pools elásticos, o `Server admin` ou uma `Azure Active Directory admin` conta é necessária. Em todos os outros objetivos de serviço do banco de dados SQL, a `VIEW DATABASE STATE` permissão é necessária no banco de dados.   

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
|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.|  
  
```  
SELECT h.type, SUM(mc.pages_kb) AS commited_memory  
FROM sys.dm_os_memory_clerks AS mc   
INNER JOIN sys.dm_os_hosts AS h   
    ON mc.memory_clerk_address = h.default_memory_clerk_address  
GROUP BY h.type;  
```  
  
## <a name="see-also"></a>Consulte Também  

 [&#41;&#40;Transact-SQL de sys.dm_os_memory_clerks ](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)   
 [SQL Server exibições de gerenciamento dinâmico relacionadas ao sistema operacional &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


