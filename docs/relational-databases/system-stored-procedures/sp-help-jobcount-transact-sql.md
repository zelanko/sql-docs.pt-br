---
title: sp_help_jobcount (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobcount
- sp_help_jobcount_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobcount
ms.assetid: ae8ef851-646c-4889-bc11-c8ec78762572
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1f874aa26001b7d595f319a59d5c116907aa096e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68054965"
---
# <a name="sp_help_jobcount-transact-sql"></a>sp_help_jobcount (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fornece o número de trabalhos aos quais uma agenda é anexada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_jobcount   
     [ @schedule_name = ] 'schedule_name' ,  
     [ @schedule_id = ] schedule_id   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @schedule_id = ] schedule_id`O identificador da agenda a ser listada. *schedule_id* é **int**, sem padrão. *Schedule_id* ou *schedule_name* pode ser especificado.  
  
`[ @schedule_name = ] 'schedule_name'`O nome da agenda a ser listada. *schedule_name* é **sysname**, sem padrão. *Schedule_id* ou *schedule_name* pode ser especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Retorna o seguinte conjunto de resultados:  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**JobCount**|**int**|Número de trabalhos para a agenda especificada.|  
  
## <a name="remarks"></a>Comentários  
 Este procedimento lista o número de trabalhos anexados à agenda especificada.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar esse procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Somente os membros do **sysadmin** podem exibir contagens de trabalhos pertencentes a outros.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir lista o número de trabalhos anexados à agenda `NightlyJobs`.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_jobcount  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Agent procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_add_schedule](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_attach_schedule](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_schedule](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_detach_schedule](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
  
