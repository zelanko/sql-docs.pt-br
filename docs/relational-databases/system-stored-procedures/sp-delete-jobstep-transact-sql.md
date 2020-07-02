---
title: sp_delete_jobstep (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_jobstep
- sp_delete_jobstep_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobstep
ms.assetid: 421ede8e-ad57-474a-9fb9-92f70a3e77e3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d9c7fc017bf0a668712f6800571ef6a84ada47e5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750616"
---
# <a name="sp_delete_jobstep-transact-sql"></a>sp_delete_jobstep (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Remove uma etapa de trabalho de um trabalho.  
  
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_delete_jobstep { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,   
     [ @step_id = ] step_id   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_id = ] job_id`O número de identificação do trabalho do qual a etapa será removida. *job_id*é **uniqueidentifier**, com um padrão de NULL.  
  
`[ @job_name = ] 'job_name'`O nome do trabalho do qual a etapa será removida. *job_name*é **sysname**, com um padrão de NULL.  
  
> **Observação:** O *job_id* ou *job_name* deve ser especificado; Não é possível especificar ambos.  
  
`[ @step_id = ] step_id`O número de identificação da etapa que está sendo removida. *step_id*é **int**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 A remoção de uma etapa de trabalho atualiza automaticamente as outras etapas de trabalho que fazem referência à etapa excluída.  
  
 Para obter mais informações sobre as etapas associadas a um trabalho específico, execute **sp_help_jobstep**.  
  
> **Observação:** Chamar **sp_delete_jobstep** com um valor de *step_id* igual a zero exclui todas as etapas de trabalho para o trabalho.  
  
 O Microsoft SQL Server Management Studio fornece uma forma fácil e gráfica para gerenciar trabalhos. Além disso, ele é recomendado para criar e gerenciar a infraestrutura do trabalho.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Somente os membros do **sysadmin** podem excluir uma etapa de trabalho que pertence a outro usuário.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove a etapa de trabalho `1` do trabalho `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1 ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir ou modificar trabalhos](../../ssms/agent/view-or-modify-jobs.md)   
 [&#41;&#40;Transact-SQL de sp_add_jobstep](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_update_jobstep](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_jobstep](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
