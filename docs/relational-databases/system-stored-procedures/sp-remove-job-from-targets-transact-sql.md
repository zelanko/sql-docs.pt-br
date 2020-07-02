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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 033a2c950ec695a64aced30a383d25206e7f6d10
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85751686"
---
# <a name="sp_remove_job_from_targets-transact-sql"></a>sp_remove_job_from_targets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Remove o trabalho especificado de determinados servidores de destino ou grupos de servidores de destino.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_remove_job_from_targets [ @job_id = ] job_id   
     | [ @job_name = ] 'job_name'   
     [ , [ @target_server_groups = ] 'target_server_groups' ]   
     [ , [ @target_servers = ] 'target_servers' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_id = ] job_id`O número de identificação do trabalho do qual remover os servidores de destino ou os grupos de servidores de destino especificados. *Job_id* ou *job_name* deve ser especificado, mas ambos não podem ser especificados. *job_id* é **uniqueidentifier**, com um padrão de NULL.  
  
`[ @job_name = ] 'job_name'`O nome do trabalho do qual remover os servidores de destino ou grupos de servidores de destino especificados. *Job_id* ou *job_name* deve ser especificado, mas ambos não podem ser especificados. *job_name* é **sysname**, com um padrão de NULL.  
  
`[ @target_server_groups = ] 'target_server_groups'`Uma lista separada por vírgulas de grupos de servidores de destino a serem removidos do trabalho especificado. *target_server_groups* é **nvarchar (1024)**, com um padrão de NULL.  
  
`[ @target_servers = ] 'target_servers'`Uma lista separada por vírgulas de servidores de destino a serem removidos do trabalho especificado. *target_servers* é **nvarchar (1024)**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="permissions"></a>Permissões  
 As permissões para executar este procedimento assumem como padrão os membros da função de servidor fixa **sysadmin** .  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_apply_job_to_targets](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_jobserver](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
