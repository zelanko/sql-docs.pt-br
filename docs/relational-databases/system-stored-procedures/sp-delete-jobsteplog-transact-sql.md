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
ms.openlocfilehash: 66b353c7fc79b49cb9cd3fb9fe228075f3a0d473
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72305092"
---
# <a name="sp_delete_jobsteplog-transact-sql"></a>sp_delete_jobsteplog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove todos os logs de etapa de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent especificados com os argumentos. Use esse procedimento armazenado para manter a tabela **sysjobstepslogs** no banco de dados **msdb** .  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_delete_jobsteplog { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
       [ , [ @step_id = ] step_id | [ @step_name = ] 'step_name' ]  
       [ , [ @older_than = ] 'date' ]  
       [ , [ @larger_than = ] 'size_in_bytes' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_id = ] 'job_id'`O número de identificação do trabalho que contém o log da etapa de trabalho a ser removido. *job_id* é **int**, com um padrão de NULL.  
  
`[ @job_name = ] 'job_name'`O nome do trabalho. *job_name* é **sysname**, com um padrão de NULL.  
  
> **Observação:** *Job_id* ou *job_name* deve ser especificado, mas ambos não podem ser especificados.  
  
`[ @step_id = ] step_id`O número de identificação da etapa no trabalho para o qual o log da etapa de trabalho deve ser excluído. Se não estiver incluído, todos os logs de etapa de trabalho no trabalho serão excluídos, a menos que ** \@older_than** ou ** \@larger_than** sejam especificados. *step_id* é **int**, com um padrão de NULL.  
  
`[ @step_name = ] 'step_name'`O nome da etapa no trabalho para o qual o log da etapa de trabalho deve ser excluído. *step_name* é **sysname**, com um padrão de NULL.  
  
> **Observação:** *Step_id* ou *step_name* pode ser especificado, mas ambos não podem ser especificados.  
  
`[ @older_than = ] 'date'`A data e a hora do log de etapa de trabalho mais antigo que você deseja manter. Todos os logs de etapa de trabalho mais antigos do que essa data e hora são removidos. *Date* é **DateTime**, com um padrão de NULL. Tanto ** \@older_than** quanto ** \@larger_than** podem ser especificados.  
  
`[ @larger_than = ] 'size_in_bytes'`O tamanho em bytes do maior log de etapa de trabalho que você deseja manter. Todos os logs de etapa de trabalho maiores que esse serão removidos. Tanto ** \@larger_than** quanto ** \@older_than** podem ser especificados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 **sp_delete_jobsteplog** está no banco de dados **msdb** .  
  
 Se nenhum argumento, exceto ** \@job_id** ou ** \@job_name** forem especificados, todos os logs de etapa de trabalho do trabalho especificado serão excluídos.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar esse procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Somente membros do **sysadmin** podem excluir um log de etapa de trabalho pertencente a outro usuário.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-removing-all-job-step-logs-from-a-job"></a>a. Removendo todos os logs de etapa de trabalho de um trabalho  
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
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_help_jobsteplog](../../relational-databases/system-stored-procedures/sp-help-jobsteplog-transact-sql.md)   
 [SQL Server Agent procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
