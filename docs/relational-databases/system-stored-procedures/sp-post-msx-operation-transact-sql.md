---
title: sp_post_msx_operation (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_post_msx_operation
- sp_post_msx_operation_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_post_msx_operation
ms.assetid: 085deef8-2709-4da9-bb97-9ab32effdacf
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f36ad40a2b16401218fe2a5927407464fe6ac11b
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536118"
---
# <a name="sppostmsxoperation-transact-sql"></a>sp_post_msx_operation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Insere operações (linhas) a **sysdownloadlist** tabela do sistema para servidores de destino baixar e executar.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_post_msx_operation  
     [ @operation = ] 'operation'  
     [ , [ @object_type = ] 'object' ]   
     { , [ @job_id = ] job_id }   
     [ , [ @specific_target_server = ] 'target_server' ]   
     [ , [ @value = ] value ]  
     [ , [ @schedule_uid = ] schedule_uid ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @operation = ] 'operation'` O tipo de operação para a operação postada. *operação*está **varchar(64)**, sem padrão. Operações válidas dependem *object_type*.  
  
|Tipo de objeto|Operação|  
|-----------------|---------------|  
|**JOB**|INSERT<br /><br /> UPDATE<br /><br /> DELETE<br /><br /> START<br /><br /> STOP|  
|**SERVER**|RE-ENLIST<br /><br /> DEFECT<br /><br /> SYNC-TIME<br /><br /> SET-POLL|  
|**AGENDA**|INSERT<br /><br /> UPDATE<br /><br /> DELETE|  
  
`[ @object_type = ] 'object'` O tipo de objeto para o qual uma operação post. Os tipos válidos são **trabalho**, **SERVER**, e **AGENDA**. *objeto* está **varchar(64)**, com um padrão de **trabalho**.  
  
`[ @job_id = ] job_id` O número de identificação do trabalho ao qual a operação se aplica. *job_id* está **uniqueidentifier**, sem padrão. **0x00** indica todos os trabalhos. Se *objeto* é **SERVER**, em seguida, *job_id*não é necessária.  
  
`[ @specific_target_server = ] 'target_server'` O nome do servidor de destino para o qual a operação especificada aplica-se. Se *job_id* for especificado, mas *target_server* não for especificado, as operações serão postadas para todos os servidores de trabalho do trabalho. *target_server* está **nvarchar (30)**, com um padrão NULL.  
  
`[ @value = ] value` O intervalo de sondagem, em segundos. *value* é **int**, com um padrão NULL. Especifique esse parâmetro somente se *operação* é **SET-POLL**.  
  
`[ @schedule_uid = ] schedule_uid` O identificador exclusivo da agenda à qual a operação se aplica. *schedule_uid* está **uniqueidentifier**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentários  
 **sp_post_msx_operation** deve ser executado a partir de **msdb** banco de dados.  
  
 **sp_post_msx_operation** sempre pode ser chamado com segurança porque ele primeiro determina se o servidor atual é um Microsoft SQL Server Agent multisservidor e, nesse caso, se *objeto*é um trabalho multisservidor.  
  
 Depois que uma operação tiver sido publicada, ele aparece na **sysdownloadlist** tabela. Depois que um trabalho for criado e postado, as alterações subsequentes desse trabalho também deverão ser comunicadas aos servidores de destino (TSX). Isto também é realizado usando a lista de carregamento.  
  
 É altamente recomendável que a lista de carregamento seja gerenciada com o uso do SQL Server Management Studio. Para obter mais informações, consulte [exibir ou modificar trabalhos](../../ssms/agent/view-or-modify-jobs.md).  
  
## <a name="permissions"></a>Permissões  
 Para executar esse procedimento armazenado, os usuários devem ter o **sysadmin** função de servidor fixa.  
  
## <a name="see-also"></a>Consulte também  
 [sp_add_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_delete_targetserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [sp_resync_targetserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)   
 [sp_start_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [sp_stop_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [sp_update_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
