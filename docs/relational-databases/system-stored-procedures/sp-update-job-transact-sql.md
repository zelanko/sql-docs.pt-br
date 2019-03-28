---
title: sp_update_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_job
- sp_update_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_job
ms.assetid: cbdfea38-9e42-47f3-8fc8-5978b82e2623
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c12e078505c8049511e59973c26d6a1417c7eae0
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537848"
---
# <a name="spupdatejob-transact-sql"></a>sp_update_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera os atributos de um trabalho.  
  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @job_id = ] job_id` O número de identificação do trabalho a ser atualizado. *job_id*está **uniqueidentifier**.  
  
`[ @job_name = ] 'job_name'` O nome do trabalho. *job_name* está **nvarchar (128)**.  
  
> **OBSERVAÇÃO:** Qualquer um dos *job_id* ou *job_name* deve ser especificado, mas não podem ser especificados.  
  
`[ @new_name = ] 'new_name'` O novo nome para o trabalho. *new_name* está **nvarchar (128)**.  
  
`[ @enabled = ] enabled` Especifica se o trabalho está habilitado (**1**) ou não habilitado (**0**). *habilitada* está **tinyint**.  
  
`[ @description = ] 'description'` A descrição do trabalho. *description* is **nvarchar(512)**.  
  
`[ @start_step_id = ] step_id` O número de identificação da primeira etapa a ser executada para o trabalho. *step_id* está **int**.  
  
`[ @category_name = ] 'category'` A categoria do trabalho. *categoria* está **nvarchar (128)**.  
  
`[ @owner_login_name = ] 'login'` O nome do logon que possui o trabalho. *login* está **nvarchar (128)** somente os membros dos **sysadmin** função de servidor fixa pode alterar a propriedade do trabalho.  
  
`[ @notify_level_eventlog = ] eventlog_level` Especifica quando colocar uma entrada no log de aplicativo do Microsoft Windows para este trabalho. *eventlog_level*está **int**, e pode ser um destes valores.  
  
|Valor|Descrição (ação)|  
|-----------|----------------------------|  
|**0**|Never|  
|**1**|Caso haja êxito|  
|**2**|Caso haja falha|  
|**3**|Always|  
  
`[ @notify_level_email = ] email_level` Especifica quando enviar um email após a conclusão deste trabalho. *email_level*está **int**. *email_level*usa os mesmos valores *eventlog_level*.  
  
`[ @notify_level_netsend = ] netsend_level` Especifica quando enviar uma mensagem de rede após a conclusão deste trabalho. *netsend_level*está **int**. *netsend_level*usa os mesmos valores *eventlog_level*.  
  
`[ @notify_level_page = ] page_level` Especifica quando enviar uma página após a conclusão deste trabalho. *page_level* está **int**. *page_level*usa os mesmos valores *eventlog_level*.  
  
`[ @notify_email_operator_name = ] 'operator_name'` O nome do operador a quem o email é enviado quando *email_level* for atingido. *email_name* está **nvarchar (128)**.  
  
`[ @notify_netsend_operator_name = ] 'netsend_operator'` O nome do operador para quem a mensagem de rede será enviada. *netsend_operator* está **nvarchar (128)**.  
  
`[ @notify_page_operator_name = ] 'page_operator'` O nome do operador para o qual uma página é enviada. *page_operator* está **nvarchar (128)**.  
  
`[ @delete_level = ] delete_level` Especifica quando excluir o trabalho. *delete_value*está **int**. *delete_level*usa os mesmos valores *eventlog_level*.  
  
`[ @automatic_post = ] automatic_post` Reservado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_update_job** deve ser executado a partir de **msdb** banco de dados.  
  
 **sp_update_job** altera somente essas configurações para o qual parâmetro valores são fornecidos. Se um parâmetro for omitido, a configuração atual será retida.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Somente os membros da **sysadmin** pode usar este procedimento armazenado para editar os atributos de trabalhos pertencentes a outros usuários.  
  
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
  
  
