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
ms.openlocfilehash: aed989cc09922b7b480a7dd7b3ca6820d6b77ab2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67936748"
---
# <a name="sp_detach_schedule-transact-sql"></a>sp_detach_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove uma associação entre uma agenda e um trabalho.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_detach_schedule   
     { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,  
       { [ @schedule_id = ] schedule_id | [ @schedule_name = ] 'schedule_name' } ,  
     [ @delete_unused_schedule = ] delete_unused_schedule   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_id = ] job_id`O número de identificação do trabalho do qual remover o agendamento. *job_id* é **uniqueidentifier**, com um padrão de NULL.  
  
`[ @job_name = ] 'job_name'`O nome do trabalho do qual remover o agendamento. *job_name* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  *Job_id* ou *job_name* deve ser especificado, mas ambos não podem ser especificados.  
  
`[ @schedule_id = ] schedule_id`O número de identificação da agenda a ser removido do trabalho. *schedule_id* é **int**, com um padrão de NULL.  
  
`[ @schedule_name = ] 'schedule_name'`O nome do agendamento a ser removido do trabalho. *schedule_name* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  *Schedule_id* ou *schedule_name* deve ser especificado, mas ambos não podem ser especificados.  
  
`[ @delete_unused_schedule = ] delete_unused_schedule`Especifica se as agendas de trabalho não usadas devem ser excluídas. *delete_unused_schedule* é **bit**, com um padrão de **0**, o que significa que todos os agendamentos serão mantidos, mesmo que nenhum trabalho faça referência a eles. Se definido como **1**, as agendas de trabalho não utilizadas serão excluídas se nenhum trabalho fizer referência a elas.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar esse procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Observe que o proprietário do trabalho pode anexar e desanexar o trabalho de uma agenda sem precisar ser também o proprietário da agenda. No entanto, uma agenda não pode ser excluída se a desanexação deixá-la sem trabalhos, a menos que o chamador seja o proprietário da agenda.  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verifica se o usuário possui a agenda. Somente os membros da função de servidor fixa **sysadmin** podem desanexar agendas de trabalhos pertencentes a outro usuário.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_add_schedule](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_attach_schedule](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_schedule](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)  
  
  
