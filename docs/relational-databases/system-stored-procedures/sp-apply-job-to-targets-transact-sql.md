---
title: sp_apply_job_to_targets (Transact-SQL) | Microsoft Docs
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
- sp_apply_job_to_targets
- sp_apply_job_to_targets_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_apply_job_to_targets
ms.assetid: 4a3e9173-7e3c-4100-a9ac-2f5d2c60a8b0
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7e7ec6285f807dd51b0a67ad55ab2e53634584e5
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33238147"
---
# <a name="spapplyjobtotargets-transact-sql"></a>sp_apply_job_to_targets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aplica um trabalho a um ou mais servidores de destino ou aos servidores de destino pertencentes a um ou mais grupos de servidores de destino.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_apply_job_to_targets { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @target_server_groups = ] 'target_server_groups' ]   
     [ , [ @target_servers = ] 'target_servers' ]   
     [ , [ @operation = ] 'operation' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@job_id =**] *job_id*  
 O número de identificação do trabalho a ser aplicado aos servidores de destino ou grupos de servidores de destino especificados. *job_id* é **uniqueidentifier**, com um padrão NULL.  
  
 [  **@job_name =**] **'***job_name***'**  
 O nome do trabalho a ser aplicado aos grupos de servidores de destino ou servidores de destino associados especificados. *job_name* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  O *job_id* ou *job_name* devem ser especificados, mas não é possível especificar ambos.  
  
 [  **@target_server_groups =**] **'***target_server_groups***'**  
 Uma lista separada por vírgulas de grupos de servidores de destino aos quais o trabalho especificado será aplicado. *target_server_groups* é **nvarchar (2048)**, com um padrão NULL.  
  
 [ **@target_servers=** ] **'***target_servers***'**  
 Uma lista separada por vírgulas de servidores de destino aos quais o trabalho especificado será aplicado. *target_servers*é **nvarchar (2048)**, com um padrão NULL.  
  
 [  **@operation=** ] **'***operação***'**  
 Se o trabalho especificado deve ser aplicado aos ou removidos dos servidores de destino ou grupos de servidores de destino especificados. *operação*é **varchar(7)**, com um padrão APPLY. As operações válidas são **aplicar** e **remover**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_apply_job_to_targets** fornece uma maneira fácil de aplicar (ou remover) um trabalho de vários servidores de destino e é uma alternativa à chamada **sp_add_jobserver** (ou **sp_delete_jobserver**) uma vez para cada servidor de destino necessário.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função fixa de servidor pode executar este procedimento.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir aplica o trabalho `Backup Customer Information` criado anteriormente a todos os servidores de destino do grupo `Servers Maintaining Customer Information`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_apply_job_to_targets  
    @job_name = N'Backup Customer Information',  
    @target_server_groups = N'Servers Maintaining Customer Information',   
    @operation = N'APPLY' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_add_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_remove_job_from_targets &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-remove-job-from-targets-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
