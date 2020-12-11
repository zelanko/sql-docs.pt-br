---
description: sys.dm_os_stacks (Transact-SQL)
title: sys.dm_os_stacks (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 04f9fe453b2f3e74a96ebd20565d92038bff4bae
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97325134"
---
# <a name="sysdm_os_stacks-transact-sql"></a>sys.dm_os_stacks (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Esta exibição de gerenciamento dinâmica é usada internamente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para fazer o seguinte:  
  
-   Manter o controle de dados de depuração como alocações pendentes.  
  
-   Supor ou validar a lógica usada pelos componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nos lugares em que o componente pressupõe que uma determinada chamada foi feita.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**stack_address**|**varbinary (8)**|Endereço exclusivo para esta alocação de pilha. Não permite valor nulo.|  
|**frame_index**|**int**|Cada linha representa uma chamada de função que, quando classificada em ordem crescente por índice de quadro para um determinado **stack_address**, retorna a pilha de chamadas completa. Não permite valor nulo.|  
|**frame_address**|**varbinary (8)**|Endereço da chamada de função. Não permite valor nulo.|  
  
## <a name="remarks"></a>Comentários  
 **Sys.dm_os_stacks** requer que os símbolos do servidor e outros componentes estejam presentes no servidor para exibir as informações corretamente.  
  
## <a name="permissions"></a>Permissões

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nos objetivos do serviço básico, S0 e S1 do banco de dados SQL, e para bancos de dados em pools elásticos, o `Server admin` ou uma `Azure Active Directory admin` conta é necessária. Em todos os outros objetivos de serviço do banco de dados SQL, a `VIEW DATABASE STATE` permissão é necessária no banco de dados.   


## <a name="see-also"></a>Consulte Também  
  [SQL Server exibições de gerenciamento dinâmico relacionadas ao sistema operacional &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  
