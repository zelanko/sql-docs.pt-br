---
title: sp_update_job (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_update_job
- sp_update_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_job
ms.assetid: cbdfea38-9e42-47f3-8fc8-5978b82e2623
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 03171bfdee98063c9bf460b9555c1a7c5d02568d
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="spupdatejob-transact-sql"></a>sp_update_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera os atributos de um trabalho.  
  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_update_job [ @job_id =] job_id | [@job_name =] 'job_name'  
     [, [@new_name =] 'new_name' ]   
     [, [@enabled =] enabled ]  
     [, [@description =] 'description' ]   
     [, [@start_step_id =] step_id ]  
     [, [@category_name =] 'category' ]   
     [, [@owner_login_name =] 'login' ]  
     [, [@notify_level_eventlog =] eventlog_level ]  
     [, [@notify_level_email =] email_level ]  
     [, [@notify_level_netsend =] netsend_level ]  
     [, [@notify_level_page =] page_level ]  
     [, [@notify_email_operator_name =] 'operator_name' ]  
     [, [@notify_netsend_operator_name =] 'netsend_operator' ]  
     [, [@notify_page_operator_name =] 'page_operator' ]  
     [, [@delete_level =] delete_level ]   
     [, [@automatic_post =] automatic_post ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@job_id =**] *job_id*  
 O número de identificação do trabalho a ser atualizado. *job_id*é **uniqueidentifier**.  
  
 [ **@job_name =**] **'***job_name***'**  
 O nome do trabalho. *job_name*is **nvarchar(128)**.  
  
> **Observação:** ou *job_id* ou *job_name* devem ser especificados, mas não podem ser especificados.  
  
 [ **@new_name =**] **'***new_name***'**  
 O novo nome do trabalho. *new_name*is **nvarchar(128)**.  
  
 [  **@enabled =**] *habilitado*  
 Especifica se o trabalho está habilitado (**1**) ou não habilitado (**0**). *habilitado*é **tinyint**.  
  
 [  **@description =**] **'***descrição***'**  
 A descrição do trabalho. *Descrição* é **nvarchar (512)**.  
  
 [  **@start_step_id =**] *step_id*  
 O número de identificação da primeira etapa a ser executada para o trabalho. *step_id*é **int**.  
  
 [  **@category_name =**] **'***categoria***'**  
 ID da categoria do trabalho. *category*is **nvarchar(128)**.  
  
 [ **@owner_login_name =**] **'***login***'**  
 O nome do logon que é o proprietário do trabalho. *logon*é **nvarchar (128)** somente os membros do **sysadmin** função de servidor fixa pode alterar a propriedade do trabalho.  
  
 [  **@notify_level_eventlog =**] *eventlog_level*  
 Especifica quando colocar uma entrada no log de aplicativo do Microsoft Windows para este trabalho. *eventlog_level*é **int**, e pode ser um destes valores.  
  
|Value|Descrição (ação)|  
|-----------|----------------------------|  
|**0**|Never|  
|**1**|Caso haja êxito|  
|**2**|Caso haja falha|  
|**3**|Always|  
  
 [  **@notify_level_email =**] *email_level*  
 Especifica quando enviar um email após a conclusão deste trabalho. *email_level*é **int**. *email_level*usa os mesmos valores como *eventlog_level*.  
  
 [  **@notify_level_netsend =**] *netsend_level*  
 Especifica quando enviar uma mensagem de rede após a conclusão deste trabalho. *netsend_level*é **int**. *netsend_level*usa os mesmos valores como *eventlog_level*.  
  
 [  **@notify_level_page =**] *page_level*  
 Especifica quando enviar uma página após a conclusão deste trabalho. *page_level*é **int**. *page_level*usa os mesmos valores como *eventlog_level*.  
  
 [  **@notify_email_operator_name =**] **'***operator_name***'**  
 O nome do operador para quem o email é enviado quando *email_level* for atingido. *nome_email* é **nvarchar (128)**.  
  
 [  **@notify_netsend_operator_name =**] **'***netsend_operator***'**  
 O nome do operador para o qual a mensagem de rede é enviada. *netsend_operator* é **nvarchar (128)**.  
  
 [  **@notify_page_operator_name =**] **'***page_operator***'**  
 O nome do operador para o qual a página é enviada. *page_operator* é **nvarchar (128)**.  
  
 [  **@delete_level =**] *delete_level*  
 Especifica quando excluir o trabalho. *delete_value*é **int**. *delete_level*usa os mesmos valores como *eventlog_level*.  
  
 [ **@automatic_post =**] *automatic_post*  
 Reservado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_update_job** deve ser executado a partir de **msdb** banco de dados.  
  
 **sp_update_job** altera somente essas configurações para quais valores são fornecidos. Se um parâmetro for omitido, a configuração atual será retida.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Somente membros da **sysadmin** pode usar esse procedimento armazenado para editar os atributos de trabalhos pertencentes a outros usuários.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir altera o nome, a descrição e o status habilitado do trabalho `NightlyBackups`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_job  
    @job_name = N'NightlyBackups',  
    @new_name = N'NightlyBackups -- Disabled',  
    @description = N'Nightly backups disabled during server migration.',  
    @enabled = 0 ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
