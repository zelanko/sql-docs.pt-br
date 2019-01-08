---
title: sp_delete_jobsteplog (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_jobsteplog
- sp_delete_jobsteplog_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobsteplog
ms.assetid: e9ef4c99-abde-4038-b6a3-a25dcbaf0958
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 719038f8ce72bdb05ad9dbf3c3585c377abb3a75
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52526230"
---
# <a name="spdeletejobsteplog-transact-sql"></a>sp_delete_jobsteplog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove todos os logs de etapa de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent especificados com os argumentos. Use este procedimento armazenado para manter o **sysjobstepslogs** na tabela a **msdb** banco de dados.  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_delete_jobsteplog { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
       [ , [ @step_id = ] step_id | [ @step_name = ] 'step_name' ]  
       [ , [ @older_than = ] 'date' ]  
       [ , [ @larger_than = ] 'size_in_bytes' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@job_id =**] **'**_job_id_**'**  
 O número de identificação do trabalho que contém o log de etapas do trabalho a ser removido. *job_id* está **int**, com um padrão NULL.  
  
 [  **@job_name =**] **'**_job_name_**'**  
 O nome do trabalho. *job_name* está **sysname**, com um padrão NULL.  
  
> **OBSERVAÇÃO:** Qualquer um dos *job_id* ou *job_name* deve ser especificado, mas não podem ser especificados.  
  
 [  **@step_id =**] *step_id*  
 O número de identificação da etapa no trabalho para o qual o log da etapa de trabalho deve ser excluído. Se não estiver incluído, todos os logs de etapa de trabalho no trabalho são excluídos, a menos que **@older_than** ou **@larger_than** são especificados. *step_id* está **int**, com um padrão NULL.  
  
 [  **@step_name =**] **'**_step_name_**'**  
 O nome da etapa no trabalho para o qual o log da etapa de trabalho deve ser excluído. *step_name* está **sysname**, com um padrão NULL.  
  
> **OBSERVAÇÃO:** Qualquer um dos *step_id* ou *step_name* pode ser especificado, mas não podem ser especificados.  
  
 [  **@older_than =**] **'**_data_**'**  
 A data e hora do log de etapa de trabalho mais antigo a ser mantido. Todos os logs de etapa de trabalho mais antigos do que essa data e hora são removidos. *data* está **datetime**, com um padrão NULL. Ambos **@older_than** e **@larger_than** pode ser especificado.  
  
 [  **@larger_than =**] **'**_size_in_bytes_**'**  
 O tamanho em bytes do maior log de etapa de trabalho a ser mantido. Todos os logs de etapa de trabalho maiores que esse serão removidos. Ambos **@larger_than** e **@older_than** pode ser especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentários  
 **sp_delete_jobsteplog** está no **msdb** banco de dados.  
  
 Se nenhum argumento, exceto **@job_id** ou **@job_name** forem especificados, todos os logs de etapa de trabalho para o trabalho especificado serão excluídos.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Somente os membros da **sysadmin** pode excluir um log de etapa de trabalho que pertence a outro usuário.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-removing-all-job-step-logs-from-a-job"></a>A. Removendo todos os logs de etapa de trabalho de um trabalho  
 O exemplo a seguir remove todos os logs de etapa do trabalho para o trabalho `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup';  
GO  
```  
  
### <a name="b-removing-the-job-step-log-for-a-particular-job-step"></a>b. Removendo o log de etapa de trabalho de uma determinada etapa de trabalho  
 O exemplo a seguir remove o logs de etapa de trabalho para a etapa 2 do trabalho `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 2;  
GO  
```  
  
### <a name="c-removing-all-job-step-logs-based-on-age-and-size"></a>C. Removendo todos os logs de etapa de trabalho com base em idade e tamanho  
 O exemplo a seguir remove todos os logs de etapa de trabalho anteriores ao meio dia de 25 de outubro de 2005 e maiores que 100 megabytes (MB) do trabalho `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @older_than = '10/25/2005 12:00:00',  
    @larger_than = 104857600;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_help_jobsteplog &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobsteplog-transact-sql.md)   
 [Procedimentos armazenados do SQL Server Agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
