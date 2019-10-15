---
title: sp_delete_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_job
- sp_delete_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_job
ms.assetid: b85db6e4-623c-41f1-9643-07e5ea38db09
author: stevestein
ms.author: sstein
ms.openlocfilehash: fc733ca2b56ef9fa96be5ab2adf6486419e0e250
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2019
ms.locfileid: "72306275"
---
# <a name="sp_delete_job-transact-sql"></a>sp_delete_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exclui um trabalho.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_delete_job { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,  
     [ , [ @originating_server = ] 'server' ]   
     [ , [ @delete_history = ] delete_history ]  
     [ , [ @delete_unused_schedule = ] delete_unused_schedule ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_id = ] job_id` é o número de identificação do trabalho a ser excluído. *job_id* é **uniqueidentifier**, com um padrão de NULL.  
  
`[ @job_name = ] 'job_name'` é o nome do trabalho a ser excluído. *job_name* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  *Job_id* ou *job_name*devem ser especificados; Não é possível especificar ambos.  
  
`[ @originating_server = ] 'server'` para uso interno.  
  
`[ @delete_history = ] delete_history` especifica se o histórico do trabalho deve ser excluído. *delete_history* é **bit**, com um padrão de **1**. Quando *delete_history* é **1**, o histórico de trabalho do trabalho é excluído. Quando *delete_history* é **0**, o histórico do trabalho não é excluído.  
  
 Observe que, quando um trabalho é excluído e o histórico não é excluído, as informações históricas do trabalho não são exibidas no histórico do trabalho da interface gráfica do usuário do agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas as informações ainda residirão na tabela **no sysjobhistory** no **msdb** banco de dados.  
  
`[ @delete_unused_schedule = ] delete_unused_schedule` especifica se as agendas anexadas a esse trabalho serão excluídas se não estiverem anexadas a nenhum outro trabalho. *delete_unused_schedule* é **bit**, com um padrão de **1**. Quando *delete_unused_schedule* for **1**, os agendamentos anexados a esse trabalho serão excluídos se nenhum outro trabalho fizer referência à agenda. Quando *delete_unused_schedule* é **0**, os agendamentos não são excluídos.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 O argumento **\@originating_server** é reservado para uso interno.  
  
 O argumento **\@delete_unused_schedule** fornece compatibilidade com versões anteriores do SQL Server removendo automaticamente os agendamentos que não estão anexados a nenhum trabalho. Observe que esse parâmetro padroniza o comportamento de compatibilidade com versões anteriores. Para manter os agendamentos que não estão anexados a um trabalho, você deve fornecer o valor **0** como o argumento **\@delete_unused_schedule** .  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] gerencia trabalhos de forma fácil e com representação gráfica. Além disso, ele é recomendado para criar e gerenciar a infraestrutura de trabalhos.  
  
 Este procedimento armazenado não pode excluir planos de manutenção e não pode excluir trabalhos que fazem parte de planos de manutenção. Em vez disso, use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para excluir planos de manutenção.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Membros da função de servidor fixa **sysadmin** podem executar **sp_delete_job** para excluir qualquer trabalho. Um usuário que não for membro da função de servidor fixa **sysadmin** poderá excluir somente os trabalhos que forem de sua propriedade.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir exclui o trabalho `NightlyBackups`.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_delete_job  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
