---
title: DM os_stacks (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2b1c72f0fe51052cefc366b7b7f81444e77e94de
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43104612"
---
# <a name="sysdmosstacks-transact-sql"></a>sys.dm_os_stacks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Esta exibição de gerenciamento dinâmica é usada internamente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para fazer o seguinte:  
  
-   Manter o controle de dados de depuração como alocações pendentes.  
  
-   Supor ou validar a lógica usada pelos componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nos lugares em que o componente pressupõe que uma determinada chamada foi feita.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**stack_address**|**varbinary(8)**|Endereço exclusivo para esta alocação de pilha. Não permite valor nulo.|  
|**frame_index**|**int**|Cada linha representa uma função chamada que, quando classificada em ordem crescente pelo índice do quadro para um determinado **stack_address**, retorna a pilha de chamadas completa. Não permite valor nulo.|  
|**frame_address**|**varbinary(8)**|Endereço da chamada de função. Não permite valor nulo.|  
  
## <a name="remarks"></a>Remarks  
 **DM os_stacks** exige que os símbolos do servidor e outros componentes estejam presentes no servidor para exibir as informações corretamente.  
  
## <a name="permissions"></a>Permissões

Na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Na [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` permissão no banco de dados.   


## <a name="see-also"></a>Consulte também  
  [Sistema operacional SQL Server relacionados exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  
