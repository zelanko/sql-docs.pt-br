---
title: sys. dm_clr_tasks (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_clr_tasks
- sys.dm_clr_tasks_TSQL
- dm_clr_tasks
- dm_clr_tasks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_tasks dynamic management view
ms.assetid: 462b9061-09fa-4858-9707-03d6cc19c769
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8a4726504794c70909664633168bfc3730ff65c7
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82824697"
---
# <a name="sysdm_clr_tasks-transact-sql"></a>sys.dm_clr_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para todas as tarefas de CLR (Common Language Runtime) que estão atualmente em execução. Um lote [!INCLUDE[tsql](../../includes/tsql-md.md)] que contém uma referência a uma rotina CLR cria uma tarefa separada para execução de todo o código gerenciado nesse lote. Várias instruções no lote que requerem o uso de execução de código gerenciado usam a mesma tarefa de CLR. A tarefa de CLR é responsável por manter objetos e estado que pertencem à execução de código gerenciado, bem como as transições entre a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o CLR.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**task_address**|**varbinary (8)**|Endereço da tarefa de CLR.|  
|**sos_task_address**|**varbinary (8)**|Endereço da tarefa de lote [!INCLUDE[tsql](../../includes/tsql-md.md)] subjacente.|  
|**appdomain_address**|**varbinary (8)**|Endereço do domínio de aplicativo no qual esta tarefa está em execução.|  
|**state**|**nvarchar(128)**|O estado atual da tarefa.|  
|**abort_state**|**nvarchar(128)**|Define se a anulação está atualmente ativada (se a tarefa tiver sido cancelada). Há vários estados envolvidos ao anular tarefas.|  
|**tipo**|**nvarchar(128)**|Tipo de tarefa.|  
|**affinity_count**|**int**|Afinidade da tarefa.|  
|**forced_yield_count**|**int**|Número de horas que a tarefa foi forçada a produzir.|  
  
## <a name="permissions"></a>Permissões  

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   
  
## <a name="see-also"></a>Consulte Também  
 [Funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas ao Common Language Runtime &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  

