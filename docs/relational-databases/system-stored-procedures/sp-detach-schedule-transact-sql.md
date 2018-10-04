---
title: sp_detach_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_detach_schedule
- sp_detach_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_detach_schedule
ms.assetid: 9a1fc335-1bef-4638-a33a-771c54a5dd19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9a7ba1ee6a8fae84d0371c30758fcd2be1098b60
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47649264"
---
# <a name="spdetachschedule-transact-sql"></a>sp_detach_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove uma associação entre uma agenda e um trabalho.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_detach_schedule   
     { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,  
       { [ @schedule_id = ] schedule_id | [ @schedule_name = ] 'schedule_name' } ,  
     [ @delete_unused_schedule = ] delete_unused_schedule   
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@job_id=** ] *job_id*  
 O número de identificação do trabalho do qual remover a agenda. *job_id* está **uniqueidentifier**, com um padrão NULL.  
  
 [ **@job_name=** ] **'***job_name***'**  
 O nome do trabalho do qual remover a agenda. *job_name* está **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  Qualquer um dos *job_id* ou *job_name* deve ser especificado, mas não podem ser especificados.  
  
 [  **@schedule_id=** ] *schedule_id*  
 O número de identificação da agenda a ser removida do trabalho. *schedule_id* está **int**, com um padrão NULL.  
  
 [  **@schedule_name=** ] **'***schedule_name***'**  
 O nome da agenda a ser removida do trabalho. *schedule_name* está **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  Qualquer um dos *schedule_id* ou *schedule_name* deve ser especificado, mas não podem ser especificados.  
  
 [ **@delete_unused_schedule=** ] *delete_unused_schedule*  
 Especifica se agendas de trabalho não usadas devem ser excluídas. *delete_unused_schedule* está **bit**, com um padrão de **0**, que significa que todas as agendas serão mantidas, mesmo se nenhum trabalho fizer referência a eles. Se definido como **1**, as agendas de trabalho serão excluídas se nenhum trabalho fizer referência a eles.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Observe que o proprietário do trabalho pode anexar e desanexar o trabalho de uma agenda sem precisar ser também o proprietário da agenda. No entanto, uma agenda não pode ser excluída se a desanexação deixá-la sem trabalhos, a menos que o chamador seja o proprietário da agenda.  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verifica se o usuário possui a agenda. Somente os membros dos **sysadmin** função de servidor fixa pode desanexar agendas de trabalhos pertencentes a outro usuário.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove uma associação entre uma agenda `'NightlyJobs'` e um trabalho `'BackupDatabase'`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_detach_schedule  
    @job_name = 'BackupDatabase',  
    @schedule_name = 'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)  
  
  
