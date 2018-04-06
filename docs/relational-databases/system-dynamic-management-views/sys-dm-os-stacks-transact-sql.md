---
title: sys.dm_os_stacks (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_stacks
- dm_os_stacks_TSQL
- sys.dm_os_stacks
- sys.dm_os_stacks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_stacks dynamic management view
ms.assetid: a69b06c4-28f0-4535-8fa1-9f132db4d916
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1536c18204a03ce093c40f1313293ef9d997caa9
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/05/2018
---
# <a name="sysdmosstacks-transact-sql"></a>sys.dm_os_stacks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Esta exibição de gerenciamento dinâmica é usada internamente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para fazer o seguinte:  
  
-   Manter o controle de dados de depuração como alocações pendentes.  
  
-   Supor ou validar a lógica usada pelos componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nos lugares em que o componente pressupõe que uma determinada chamada foi feita.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**stack_address**|**varbinary(8)**|Endereço exclusivo para esta alocação de pilha. Não permite valor nulo.|  
|**frame_index**|**Int**|Cada linha representa uma função chamada que, quando classificada em ordem crescente pelo índice de quadro para um determinado **stack_address**, retorna a pilha de chamadas completa. Não permite valor nulo.|  
|**frame_address**|**varbinary(8)**|Endereço da chamada de função. Não permite valor nulo.|  
  
## <a name="remarks"></a>Remarks  
 **sys.DM os_stacks** exige que os símbolos do servidor e outros componentes estejam presentes no servidor para exibir as informações corretamente.  
  
## <a name="permissions"></a>Permissões

Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` no banco de dados.   


## <a name="see-also"></a>Consulte também  
  [Sistema operacional SQL Server relacionadas exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  
