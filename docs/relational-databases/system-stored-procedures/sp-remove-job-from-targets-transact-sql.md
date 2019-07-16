---
title: sp_remove_job_from_targets (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_remove_job_from_targets_TSQL
- sp_remove_job_from_targets
dev_langs:
- TSQL
helpviewer_keywords:
- sp_remove_job_from_targets
ms.assetid: b8171fb1-c11d-4244-8618-a12e28a150ce
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1ba55c2744d1fad0b6453e0f1d1cd2ea96934bfa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006974"
---
# <a name="spremovejobfromtargets-transact-sql"></a>sp_remove_job_from_targets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove o trabalho especificado de determinados servidores de destino ou grupos de servidores de destino.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_remove_job_from_targets [ @job_id = ] job_id   
     | [ @job_name = ] 'job_name'   
     [ , [ @target_server_groups = ] 'target_server_groups' ]   
     [ , [ @target_servers = ] 'target_servers' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_id = ] job_id` O número de identificação do trabalho do qual remover os servidores de destino especificados ou grupos de servidores de destino. Qualquer um dos *job_id* ou *job_name* deve ser especificado, mas não podem ser especificados. *job_id* está **uniqueidentifier**, com um padrão NULL.  
  
`[ @job_name = ] 'job_name'` O nome do trabalho do qual remover os servidores de destino especificados ou grupos de servidores de destino. Qualquer um dos *job_id* ou *job_name* deve ser especificado, mas não podem ser especificados. *job_name* está **sysname**, com um padrão NULL.  
  
`[ @target_server_groups = ] 'target_server_groups'` Uma lista separada por vírgulas de grupos de servidores de destino a ser removido do trabalho especificado. *target_server_groups* está **nvarchar(1024)** , com um padrão NULL.  
  
`[ @target_servers = ] 'target_servers'` Uma lista separada por vírgulas de servidores de destino a ser removido do trabalho especificado. *target_servers* está **nvarchar(1024)** , com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="permissions"></a>Permissões  
 As permissões para executar esse procedimento usam como padrão membros da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove o trabalho `Weekly Sales Backups` criado anteriormente do grupo de servidores de destino `Servers Processing Customer Orders` e dos servidores `SEATTLE1` e `SEATTLE2`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_remove_job_from_targets  
    @job_name = N'Weekly Sales Backups',  
    @target_server_groups = N'Servers Processing Customer Orders',   
    @target_servers = N'SEATTLE2,SEATTLE1' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_apply_job_to_targets &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
