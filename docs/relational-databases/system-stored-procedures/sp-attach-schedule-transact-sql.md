---
title: sp_attach_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_attach_schedule_TSQL
- sp_attach_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_attach_schedule
ms.assetid: 80c80eaf-cf23-4ed8-b8dd-65fe59830dd1
author: stevestein
ms.author: sstein
ms.openlocfilehash: f85095941311459da2fdc757a11895795ebb418e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046157"
---
# <a name="sp_attach_schedule-transact-sql"></a>sp_attach_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Define uma agenda para um trabalho.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_attach_schedule  
     { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,   
     { [ @schedule_id = ] schedule_id   
     | [ @schedule_name = ] 'schedule_name' }  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_id = ] job_id`O número de identificação do trabalho para o qual o agendamento é adicionado. *job_id*é **uniqueidentifier**, com um padrão de NULL.  
  
`[ @job_name = ] 'job_name'`O nome do trabalho ao qual a agenda é adicionada. *job_name*é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  *Job_id* ou *job_name* deve ser especificado, mas ambos não podem ser especificados.  
  
`[ @schedule_id = ] schedule_id`O número de identificação da agenda a ser definido para o trabalho. *schedule_id*é **int**, com um padrão de NULL.  
  
`[ @schedule_name = ] 'schedule_name'`O nome do agendamento a ser definido para o trabalho. *schedule_name*é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  *Schedule_id* ou *schedule_name* deve ser especificado, mas ambos não podem ser especificados.  
  
## <a name="remarks"></a>Comentários  
 A agenda e o trabalho devem ter o mesmo proprietário.  
  
 Uma agenda pode ser definida para mais de um trabalho. Um trabalho pode ser executado em mais de uma agenda.  
  
 Esse procedimento armazenado deve ser executado do banco de dados **msdb** .  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar esse procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Observe que o proprietário do trabalho pode anexar e desanexar o trabalho de uma agenda sem precisar ser também o proprietário da agenda. No entanto, uma agenda não poderá ser excluída se a desanexação não deixar nenhum trabalho, a menos que o chamador seja o proprietário da agenda.  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verifica se o usuário possui o trabalho e a agenda.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma agenda chamado `NightlyJobs`. Os trabalhos que usam essa agenda são executados diariamente quando a hora no servidor é `01:00`. O exemplo anexa a agenda ao trabalho `BackupDatabase` e ao trabalho `RunReports`.  
  
> [!NOTE]  
>  Este exemplo supõe que o trabalho `BackupDatabase` e o trabalho `RunReports` já existem.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_add_schedule  
    @schedule_name = N'NightlyJobs' ,  
    @freq_type = 4,  
    @freq_interval = 1,  
    @active_start_time = 010000 ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'BackupDatabase',  
   @schedule_name = N'NightlyJobs' ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'RunReports',  
   @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_add_schedule](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_detach_schedule](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_schedule](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)  
  
  
