---
title: sys. dm_os_child_instances (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_child_instances
- sys.dm_os_child_instances_TSQL
- dm_os_child_instances
- dm_os_child_instances_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server state information [SQL Server]
- sys.dm_os_child_instances dynamic management view
- monitoring server health
ms.assetid: 1bef3074-0ccc-48fa-8f3d-14f3d99df86b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 59a58348f5428f568f40d28b4e83bc6bc040647c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67900241"
---
# <a name="sysdm_os_child_instances-transact-sql"></a>sys.dm_os_child_instances (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada instância de usuário que foi criada a partir da instância do servidor pai.  
  
> **IMPORTANTE:** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 As informações retornadas de **Sys. dm_os_child_instances** podem ser usadas para determinar o estado de cada instância de usuário (heart_beat) e para obter o nome do pipe (instance_pipe_name) que pode ser usado para criar uma conexão com a [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] instância de usuário usando ou SQLCmd. Será possível conectar-se a uma Instância de Usuário somente depois que ela for iniciada por um processo externo, como um aplicativo cliente. As ferramentas de gerenciamento SQL não podem iniciar uma Instância de Usuário.  
  
> **Observação:** As instâncias de usuário são apenas [!INCLUDE[ssExpressEd11](../../includes/ssexpressed11-md.md)] um recurso do.  
> 
> **Observação** Para chamá-lo [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]ou, use o nome **Sys. dm_pdw_nodes_os_child_instances**.  
  
|Coluna|Tipo de dados|DESCRIÇÃO|  
|------------|---------------|-----------------|  
|**owning_principal_name**|**nvarchar(256)**|O nome do usuário para o qual esta instância de usuário foi criada.|  
|owning_principal_sid|nvarchar(256)|SID (Identificador de Segurança) da entidade que possui esta instância de usuário. Isto corresponde ao SID do Windows.|  
|owning_principal_sid_binary|varbinary(85)|Versão binária do SID do usuário que possui a Instância de usuário|  
|**instance_name**|**nvarchar(128)**|O nome desta instância de usuário.|  
|**instance_pipe_name**|**nvarchar(260)**|Quando uma instância de usuário for criada, um pipe nomeado será criado para que aplicativos se conectem. Esse nome pode ser usado em uma cadeia de caracteres de conexão a fim de conectar a esta instância de usuário.|  
|**os_process_id**|**Inteiro**|O número do processo do Windows para esta instância de usuário.|  
|**os_process_creation_date**|**Horário**|A data e a hora em que este processo de instância de usuário foi iniciado pela última vez.|  
|**heart_beat**|**nvarchar (5)**|Estado atual desta instância de usuário; ALIVE ou DEAD.|  
|**pdw_node_id**|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre a exibição de gerenciamento dinâmico, consulte [funções e exibições de gerenciamento dinâmico &#40;&#41;do Transact-SQL](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) nos manuais online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Instâncias de usuário para não administradores](https://msdn.microsoft.com/85385aae-10fb-4f8b-9eeb-cce2ee7da019)  
  
  



