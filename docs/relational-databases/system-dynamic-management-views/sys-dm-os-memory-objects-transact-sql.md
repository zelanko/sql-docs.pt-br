---
description: sys.dm_os_memory_objects (Transact-SQL)
title: sys. dm_os_memory_objects (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_memory_objects
- sys.dm_os_memory_objects
- sys.dm_os_memory_objects_TSQL
- dm_os_memory_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_objects dynamic management view
ms.assetid: 5688bcf8-5da9-4ff9-960b-742b671d7096
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 42e6d315d2a3450223e7a5d9f1a6d9e75ac5d4b6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539337"
---
# <a name="sysdm_os_memory_objects-transact-sql"></a>sys.dm_os_memory_objects (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna objetos da memória que estão alocados no momento pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode usar **Sys. dm_os_memory_objects** para analisar o uso de memória e identificar possíveis vazamentos de memória.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**memory_object_address**|**varbinary (8)**|Endereço do objeto de memória. Não permite valor nulo.|  
|**parent_address**|**varbinary (8)**|Endereço do objeto de memória pai. Permite valor nulo.|  
|**pages_allocated_count**|**int**|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Número de páginas que são alocadas por esse objeto. Não permite valor nulo.|  
|**pages_in_bytes**|**bigint**|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> Quantidade de memória em bytes alocada por essa instância do objeto de memória. Não permite valor nulo.|  
|**creation_options**|**int**|Somente para uso interno. Permite valor nulo.|  
|**bytes_used**|**bigint**|Somente para uso interno. Permite valor nulo.|  
|**tipo**|**nvarchar(60)**|Tipo de objeto de memória.<br /><br /> Isso indica algum componente ao qual este objeto de memória pertence ou a função do objeto de memória. Permite valor nulo.|  
|**name**|**varchar(128)**|Somente para uso interno. Anulável.|  
|**memory_node_id**|**smallint**|ID de um nó de memória que está sendo usado por esse objeto de memória. Não permite valor nulo.|  
|**creation_time**|**datetime**|Somente para uso interno. Permite valor nulo.|  
|**max_pages_allocated_count**|**int**|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Número máximo de páginas alocadas por esse objeto de memória. Não permite valor nulo.|  
|**page_size_in_bytes**|**int**|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> Tamanho das páginas em bytes alocadas por esse objeto. Não permite valor nulo.|  
|**max_pages_in_bytes**|**bigint**|Quantidade máxima de memória sempre usada por esse objeto de memória. Não permite valor nulo.|  
|**page_allocator_address**|**varbinary (8)**|Endereço de memória do alocador de página. Não permite valor nulo. Para obter mais informações, consulte [Sys. dm_os_memory_clerks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).|  
|**creation_stack_address**|**varbinary (8)**|Somente para uso interno. Permite valor nulo.|  
|**sequence_num**|**int**|Somente para uso interno. Permite valor nulo.|  
|**partition_type**|**int**|**Aplica-se a**: [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] e posterior.<br /><br /> O tipo de partição:<br /><br /> 0-objeto de memória não particionável<br /><br /> 1-objeto de memória particionável, atualmente não particionado<br /><br /> 2-objeto de memória particionável, particionado por nó NUMA. Em um ambiente com um único nó NUMA, isso é equivalente a 1.<br /><br /> 3-objeto de memória particionável, particionado por CPU.|  
|**contention_factor**|**real**|**Aplica-se a**: [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] e posterior.<br /><br /> Um valor que especifica a contenção nesse objeto de memória, com 0 significando que não há contenção. O valor é atualizado sempre que um número especificado de alocações de memória foi feito refletindo a contenção durante esse período. Aplica-se somente a objetos de memória thread-safe.|  
|**waiting_tasks_count**|**bigint**|**Aplica-se a**: [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] e posterior.<br /><br /> Número de esperas neste objeto de memória. Esse contador é incrementado sempre que a memória é alocada a partir deste objeto de memória. O incremento é o número de tarefas que estão aguardando acesso a esse objeto de memória no momento. Aplica-se somente a objetos de memória thread-safe. Esse é um valor de melhor esforço sem uma garantia de exatidão.|  
|**exclusive_access_count**|**bigint**|**Aplica-se a**: [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] e posterior.<br /><br /> Especifica com que frequência este objeto de memória foi acessado exclusivamente. Aplica-se somente a objetos de memória thread-safe.  Esse é um valor de melhor esforço sem uma garantia de exatidão.|  
|**pdw_node_id**|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
 **partition_type**, **contention_factor**, **waiting_tasks_count**e **exclusive_access_count** ainda não foram implementadas no [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] .  
  
## <a name="permissions"></a>Permissões

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o  **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   

## <a name="remarks"></a>Comentários  
 Os objetos de memória são heaps. Eles fornecem alocações que possuem uma granularidade maior do que a fornecida pelos administradores de memória. Os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usam objetos de memória, em vez de administradores de memória. Os objetos de memória usam a interface do alocador de página do administrador de memória para alocar páginas. Eles não usam interfaces de memória virtuais ou compartilhadas. Dependendo dos padrões de alocação, os componentes podem criar tipos diferentes de objetos de memória para alocar regiões de tamanho arbitrário.  
  
 O tamanho de página típico para um objeto de memória é de 8 KB. Entretanto, objetos de memória incrementais podem ter tamanhos de página que variam de 512 bytes a 8 KB.  
  
> [!NOTE]  
>  O tamanho de página não é uma alocação máxima. Na verdade, o tamanho de página é a granularidade de alocação com suporte oferecida por um alocador de página e é implementado por um administrador de memória. Você pode solicitar alocações com mais de 8 KB de objetos de memória.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a quantidade de memória alocada em cada tipo de objeto de memória.  
  
```  
SELECT SUM (pages_in_bytes) as 'Bytes Used', type   
FROM sys.dm_os_memory_objects  
GROUP BY type   
ORDER BY 'Bytes Used' DESC;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
  [SQL Server exibições de gerenciamento dinâmico relacionadas ao sistema operacional &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_memory_clerks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)  
  
  


