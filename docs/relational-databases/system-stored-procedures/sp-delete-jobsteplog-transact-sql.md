---
title: sp_delete_jobsteplog (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_jobsteplog
- sp_delete_jobsteplog_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobsteplog
ms.assetid: e9ef4c99-abde-4038-b6a3-a25dcbaf0958
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 99f60818976dc3c89e11d2fd1256a7aecd7d8b63
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spdeletejobsteplog-transact-sql"></a>sp_delete_jobsteplog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove todos os logs de etapa de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent especificados com os argumentos. Use este procedimento armazenado para manter o **sysjobstepslogs** tabela o **msdb** banco de dados.  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_delete_jobsteplog { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
       [ , [ @step_id = ] step_id | [ @step_name = ] 'step_name' ]  
       [ , [ @older_than = ] 'date' ]  
       [ , [ @larger_than = ] 'size_in_bytes' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@job_id =**] **'***job_id***'**  
 O número de identificação do trabalho que contém o log de etapas do trabalho a ser removido. *job_id* é **int**, com um padrão NULL.  
  
 [  **@job_name =**] **'***job_name***'**  
 O nome do trabalho. *job_name* é **sysname**, com um padrão NULL.  
  
> **Observação:** ou *job_id* ou *job_name* devem ser especificados, mas não é possível especificar ambos.  
  
 [  **@step_id =**] *step_id*  
 O número de identificação da etapa no trabalho para o qual o log da etapa de trabalho deve ser excluído. Se não estiver incluído, todos os logs de etapa de trabalho do trabalho são excluídos, a menos que **@older_than** ou **@larger_than** são especificados. *step_id* é **int**, com um padrão NULL.  
  
 [  **@step_name =**] **'***step_name***'**  
 O nome da etapa no trabalho para o qual o log da etapa de trabalho deve ser excluído. *step_name* é **sysname**, com um padrão NULL.  
  
> **Observação:** ou *step_id* ou *step_name* podem ser especificados, mas não é possível especificar ambos.  
  
 [  **@older_than =**] **'***data***'**  
 A data e hora do log de etapa de trabalho mais antigo a ser mantido. Todos os logs de etapa de trabalho mais antigos do que essa data e hora são removidos. *data* é **datetime**, com um padrão NULL. Ambos **@older_than** e **@larger_than** pode ser especificado.  
  
 [  **@larger_than =**] **'***size_in_bytes***'**  
 O tamanho em bytes do maior log de etapa de trabalho a ser mantido. Todos os logs de etapa de trabalho maiores que esse serão removidos. Ambos **@larger_than** e **@older_than** pode ser especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Remarks  
 **sp_delete_jobsteplog** está no **msdb** banco de dados.  
  
 Se nenhum argumento exceto **@job_id** ou **@job_name** forem especificados, todos os logs de etapa de trabalho para o trabalho especificado serão excluídos.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Somente membros da **sysadmin** pode excluir um log de etapa de trabalho que pertence a outro usuário.  
  
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
  
### <a name="b-removing-the-job-step-log-for-a-particular-job-step"></a>B. Removendo o log de etapa de trabalho de uma determinada etapa de trabalho  
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
  
  
