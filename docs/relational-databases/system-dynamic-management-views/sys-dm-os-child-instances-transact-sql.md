---
title: sys.dm_os_child_instances (Transact-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 69269e2934589841c42825f21494932b5306dd2d
ms.sourcegitcommit: 9f2edcdf958e6afce9a09fb2e572ae36dfe9edb0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50099277"
---
# <a name="sysdmoschildinstances-transact-sql"></a>sys.dm_os_child_instances (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada instância de usuário que foi criada a partir da instância do servidor pai.  
  
> **IMPORTANTE:** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 As informações retornadas **sys.dm_os_child_instances** pode ser usado para determinar o estado de cada instância de usuário (heart_beat) e obter o nome do pipe (instance_pipe_name) que pode ser usado para criar uma conexão para o usuário Instância usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou SQLCmd. Será possível conectar-se a uma Instância de Usuário somente depois que ela for iniciada por um processo externo, como um aplicativo cliente. As ferramentas de gerenciamento SQL não podem iniciar uma Instância de Usuário.  
  
> **Observação:** instâncias de usuário são um recurso do [!INCLUDE[ssExpressEd11](../../includes/ssexpressed11-md.md)] apenas.  
  
> **Observação** chamá-lo partir [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_child_instances**.  
  
|coluna|Data type|Description|  
|------------|---------------|-----------------|  
|**owning_principal_name**|**nvarchar(256)**|O nome do usuário para o qual esta instância de usuário foi criada.|  
|owning_principal_sid|nvarchar(256)|SID (Identificador de Segurança) da entidade que possui esta instância de usuário. Isto corresponde ao SID do Windows.|  
|owning_principal_sid_binary|varbinary(85)|Versão binária do SID do usuário que possui a Instância de usuário|  
|**instance_name**|**nvarchar(128)**|O nome desta instância de usuário.|  
|**instance_pipe_name**|**nvarchar(260)**|Quando uma instância de usuário for criada, um pipe nomeado será criado para que aplicativos se conectem. Esse nome pode ser usado em uma cadeia de caracteres de conexão a fim de conectar a esta instância de usuário.|  
|**os_process_id**|**Int**|O número do processo do Windows para esta instância de usuário.|  
|**os_process_creation_date**|**Datetime**|A data e a hora em que este processo de instância de usuário foi iniciado pela última vez.|  
|**heart_beat**|**nvarchar(5)**|Estado atual desta instância de usuário; ALIVE ou DEAD.|  
|**pdw_node_id**|**int**|**Aplica-se ao**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre a exibição de gerenciamento dinâmico, consulte [funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41; ](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online.  
  
## <a name="see-also"></a>Consulte também  
 [Instâncias de usuário para não administradores](http://msdn.microsoft.com/85385aae-10fb-4f8b-9eeb-cce2ee7da019)  
  
  



