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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 36759d2c90e29c0a019d8bd294a0c7e621c8d468
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891551"
---
# <a name="sp_post_msx_operation-transact-sql"></a>sp_post_msx_operation (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Insere operações (linhas) na tabela do sistema **sysdownloadlist** para que os servidores de destino baixem e executem.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @operation = ] 'operation'`O tipo de operação para a operação postada. a *operação*é **varchar (64)**, sem padrão. As operações válidas dependem do *object_type*.  
  
|Tipo de objeto|Operação|  
|-----------------|---------------|  
|**TRABALHO**|INSERT<br /><br /> UPDATE<br /><br /> Delete (excluir)<br /><br /> START<br /><br /> STOP|  
|**SERVIDOR**|RE-ENLIST<br /><br /> DEFECT<br /><br /> SYNC-TIME<br /><br /> SET-POLL|  
|**AGENDAMENTO**|INSERT<br /><br /> UPDATE<br /><br /> Delete (excluir)|  
  
`[ @object_type = ] 'object'`O tipo de objeto para o qual uma operação deve ser postada. Os tipos válidos são **trabalho**, **servidor**e **agendamento**. o *objeto* é **varchar (64)**, com um padrão de **trabalho**.  
  
`[ @job_id = ] job_id`O número de identificação do trabalho ao qual a operação se aplica. *job_id* é **uniqueidentifier**, sem padrão. **0x00** indica todos os trabalhos. Se *Object* for **SERVER**, o *job_id*não será necessário.  
  
`[ @specific_target_server = ] 'target_server'`O nome do servidor de destino para o qual a operação especificada se aplica. Se *job_id* for especificado, mas *target_server* não for especificado, as operações serão lançadas para todos os servidores de trabalho do trabalho. *target_server* é **nvarchar (30)**, com um padrão de NULL.  
  
`[ @value = ] value`O intervalo de sondagem, em segundos. *value* é **int**, com um padrão NULL. Especifique esse parâmetro somente se a *operação* for **set-Poll**.  
  
`[ @schedule_uid = ] schedule_uid`O identificador exclusivo para o agendamento ao qual a operação se aplica. *schedule_uid* é **uniqueidentifier**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 **sp_post_msx_operation** deve ser executado do banco de dados **msdb** .  
  
 **sp_post_msx_operation** sempre pode ser chamado com segurança porque determina primeiro se o servidor atual é um agente de Microsoft SQL Server multisservidor e, em caso afirmativo, se o *objeto*é um trabalho multisservidor.  
  
 Depois que uma operação foi postada, ela aparece na tabela **sysdownloadlist** . Depois que um trabalho for criado e postado, as alterações subsequentes desse trabalho também deverão ser comunicadas aos servidores de destino (TSX). Isto também é realizado usando a lista de carregamento.  
  
 É altamente recomendável que a lista de carregamento seja gerenciada com o uso do SQL Server Management Studio. Para obter mais informações, consulte [Exibir ou modificar trabalhos](../../ssms/agent/view-or-modify-jobs.md).  
  
## <a name="permissions"></a>Permissões  
 Para executar esse procedimento armazenado, os usuários devem receber a função de servidor fixa **sysadmin** .  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_add_jobserver](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_job](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_jobserver](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_targetserver](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_resync_targetserver](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_start_job](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_stop_job](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_update_job](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_update_operator](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
