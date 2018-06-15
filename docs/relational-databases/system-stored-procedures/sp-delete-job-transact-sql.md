---
title: sp_delete_job (Transact-SQL) | Microsoft Docs
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
- sp_delete_job
- sp_delete_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_job
ms.assetid: b85db6e4-623c-41f1-9643-07e5ea38db09
caps.latest.revision: 43
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 90d213daa9d5a17a6630142e06e5b7ef441a9e9c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33262909"
---
# <a name="spdeletejob-transact-sql"></a>sp_delete_job (Transact-SQL)
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
 [ **@job_id=** ] *job_id*  
 É o número de identificação do trabalho a ser excluído. *job_id* é **uniqueidentifier**, com um padrão NULL.  
  
 [ **@job_name=** ] **'***job_name***'**  
 É o nome do trabalho a ser excluído. *job_name* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  O *job_id* ou *job_name*deve ser especificado; não podem ser especificados.  
  
 [  **@originating_server=** ] **'***server***'**  
 Para uso interno.  
  
 [  **@delete_history=** ] *delete_history*  
 Especifica se o histórico do trabalho deve ser excluído. *delete_history* é **bit**, com um padrão de **1**. Quando *delete_history* é **1**, o histórico de trabalho para o trabalho é excluído. Quando *delete_history* é **0**, o histórico de trabalho não será excluído.  
  
 Observe que, quando um trabalho é excluído e o histórico não será excluído, informações de histórico para o trabalho não serão exibidos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] histórico de trabalho de interface de usuário gráfica Agent, mas as informações ainda residem no **sysjobhistory**tabela o **msdb** banco de dados.  
  
 [ **@delete_unused_schedule=** ] *delete_unused_schedule*  
 Especifica se as agendas anexadas a esse trabalho devem ser excluídas se não estiverem anexadas a nenhum outro. *delete_unused_schedule* é **bit**, com um padrão de **1**. Quando *delete_unused_schedule* é **1**, agendas anexadas a esse trabalho são excluídas se nenhum outro trabalho referenciar a agenda. Quando *delete_unused_schedule* é **0**, as agendas não são excluídas.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Remarks  
 O **@originating_server** argumento é reservado para uso interno.  
  
 O **@delete_unused_schedule** argumento fornece compatibilidade com versões anteriores do SQL Server removendo automaticamente agendas que não estão associadas a qualquer trabalho. Observe que esse parâmetro padroniza o comportamento de compatibilidade com versões anteriores. Para manter as agendas que não estão associadas a um trabalho, você deve fornecer o valor **0** como o **@delete_unused_schedule** argumento.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] gerencia trabalhos de forma fácil e com representação gráfica. Além disso, ele é recomendado para criar e gerenciar a infraestrutura de trabalhos.  
  
 Este procedimento armazenado não pode excluir planos de manutenção e não pode excluir trabalhos que fazem parte de planos de manutenção. Em vez disso, use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para excluir planos de manutenção.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
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
  
  
