---
title: sp_attach_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_attach_schedule_TSQL
- sp_attach_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_attach_schedule
ms.assetid: 80c80eaf-cf23-4ed8-b8dd-65fe59830dd1
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5c1ec7f73e6fefadb9e73ca8295afb858f6d1d6a
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394385"
---
# <a name="spattachschedule-transact-sql"></a>sp_attach_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Define uma agenda para um trabalho.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_attach_schedule  
     { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,   
     { [ @schedule_id = ] schedule_id   
     | [ @schedule_name = ] 'schedule_name' }  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@job_id=** ] *job_id*  
 O número de identificação do trabalho para o qual a agenda é adicionada. *job_id*está **uniqueidentifier**, com um padrão NULL.  
  
 [  **@job_name =** ] **'***job_name***'**  
 O nome do trabalho ao qual a agenda é adicionada. *job_name*está **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  Qualquer um dos *job_id* ou *job_name* deve ser especificado, mas não podem ser especificados.  
  
 [  **@schedule_id =** ] *schedule_id*  
 O número de identificação da agenda a ser definida para o trabalho. *schedule_id*está **int**, com um padrão NULL.  
  
 [  **@schedule_name =** ] **'***schedule_name***'**  
 O nome da agenda a ser definida para o trabalho. *schedule_name*está **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  Qualquer um dos *schedule_id* ou *schedule_name* deve ser especificado, mas não podem ser especificados.  
  
## <a name="remarks"></a>Remarks  
 A agenda e o trabalho devem ter o mesmo proprietário.  
  
 Uma agenda pode ser definida para mais de um trabalho. Um trabalho pode ser executado em mais de uma agenda.  
  
 Esse procedimento armazenado deve ser executado a partir de **msdb** banco de dados.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Observe que o proprietário do trabalho pode anexar e desanexar o trabalho de uma agenda sem precisar ser também o proprietário da agenda. No entanto, uma agenda não pode ser excluída se a desanexação deixá-la sem trabalhos, a menos que o chamador seja o proprietário da agenda.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_detach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)  
  
  
