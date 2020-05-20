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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 53bb2daacf55bf86693f2e083262083d7cbff22b
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831234"
---
# <a name="sp_delete_job-transact-sql"></a>sp_delete_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exclui um trabalho.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_delete_job { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,  
     [ , [ @originating_server = ] 'server' ]   
     [ , [ @delete_history = ] delete_history ]  
     [ , [ @delete_unused_schedule = ] delete_unused_schedule ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_id = ] job_id`É o número de identificação do trabalho a ser excluído. *job_id* é **uniqueidentifier**, com um padrão de NULL.  
  
`[ @job_name = ] 'job_name'`É o nome do trabalho a ser excluído. *job_name* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  O *job_id* ou *job_name*deve ser especificado; Não é possível especificar ambos.  
  
`[ @originating_server = ] 'server'`Para uso interno.  
  
`[ @delete_history = ] delete_history`Especifica se o histórico do trabalho deve ser excluído. *delete_history* é **bit**, com um padrão de **1**. Quando *delete_history* for **1**, o histórico de trabalho do trabalho será excluído. Quando *delete_history* é **0**, o histórico do trabalho não é excluído.  
  
 Observe que, quando um trabalho é excluído e o histórico não é excluído, as informações históricas para o trabalho não serão exibidas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] histórico do trabalho da interface gráfica do usuário do agente, mas as informações ainda residirão na tabela **no sysjobhistory** no banco de dados **msdb** .  
  
`[ @delete_unused_schedule = ] delete_unused_schedule`Especifica se as agendas anexadas a esse trabalho serão excluídas se não estiverem anexadas a nenhum outro trabalho. *delete_unused_schedule* é **bit**, com um padrão de **1**. Quando *delete_unused_schedule* for **1**, os agendamentos anexados a esse trabalho serão excluídos se nenhum outro trabalho fizer referência à agenda. Quando *delete_unused_schedule* é **0**, as agendas não são excluídas.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 O argumento ** \@ originating_server** é reservado para uso interno.  
  
 O argumento ** \@ delete_unused_schedule** fornece compatibilidade com versões anteriores do SQL Server removendo automaticamente os agendamentos que não estão anexados a nenhum trabalho. Observe que esse parâmetro padroniza o comportamento de compatibilidade com versões anteriores. Para reter agendamentos que não estão anexados a um trabalho, você deve fornecer o valor **0** como o argumento de ** \@ delete_unused_schedule** .  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_add_job](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_job](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_update_job](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
