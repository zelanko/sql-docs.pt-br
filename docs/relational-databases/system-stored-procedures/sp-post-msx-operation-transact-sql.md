---
title: sp_post_msx_operation (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_post_msx_operation
- sp_post_msx_operation_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_post_msx_operation
ms.assetid: 085deef8-2709-4da9-bb97-9ab32effdacf
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1774a033e119f14e89a0f5fe141dd99ee0453ec9
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sppostmsxoperation-transact-sql"></a>sp_post_msx_operation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Insere operações (linhas) do **sysdownloadlist** tabela do sistema para servidores de destino baixar e executar.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@operation =**] **'***operação***'**  
 O tipo da operação postada. *operação*é **varchar(64)**, sem padrão. Operações válidas dependem *object_type*.  
  
|Tipo de objeto|Operação|  
|-----------------|---------------|  
|**TRABALHO**|INSERT<br /><br /> UPDATE<br /><br /> DELETE<br /><br /> START<br /><br /> STOP|  
|**SERVIDOR**|RE-ENLIST<br /><br /> DEFECT<br /><br /> SYNC-TIME<br /><br /> SET-POLL|  
|**AGENDA**|INSERT<br /><br /> UPDATE<br /><br /> DELETE|  
  
 [  **@object_type =**] **'***objeto***'**  
 O tipo de objeto para o qual uma operação será postada. Os tipos válidos são **trabalho**, **servidor**, e **AGENDA**. *objeto* é **varchar(64)**, com um padrão de **trabalho**.  
  
 [  **@job_id =**] *job_id*  
 O número de identificação do trabalho ao qual a operação se aplica. *job_id* é **uniqueidentifier**, sem padrão. **0x00** indica todos os trabalhos. Se *objeto* é **servidor**, em seguida, *job_id*não é necessária.  
  
 [  **@specific_target_server =**] **'***target_server***'**  
 O nome do servidor de destino ao qual a operação especificada se aplica. Se *job_id* for especificado, mas *target_server* não for especificado, as operações serão postadas para todos os servidores de trabalho do trabalho. *target_server* é **nvarchar (30)**, com um padrão NULL.  
  
 [  **@value =**] *valor*  
 O intervalo de sondagem, em segundos. *value* é **int**, com um padrão NULL. Especifique esse parâmetro somente se *operação* é **SET-POLL**.  
  
 [  **@schedule_uid=** ] *schedule_uid*  
 O identificador exclusivo da agenda à qual a operação se aplica. *schedule_uid* é **uniqueidentifier**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Comentários  
 **sp_post_msx_operation** deve ser executado a partir de **msdb** banco de dados.  
  
 **sp_post_msx_operation** sempre pode ser chamado com segurança porque ele primeiro determina se o servidor atual é um Microsoft SQL Server Agent multisservidor e, nesse caso, se *objeto*é um trabalho multisservidor.  
  
 Depois que uma operação foi postada, ele aparece no **sysdownloadlist** tabela. Depois que um trabalho for criado e postado, as alterações subsequentes desse trabalho também deverão ser comunicadas aos servidores de destino (TSX). Isto também é realizado usando a lista de carregamento.  
  
 É altamente recomendável que a lista de carregamento seja gerenciada com o uso do SQL Server Management Studio. Para obter mais informações, consulte [exibir ou modificar trabalhos](http://msdn.microsoft.com/library/57f649b8-190c-4304-abd7-7ca5297deab7).  
  
## <a name="permissions"></a>Permissões  
 Para executar esse procedimento armazenado, os usuários devem ter o **sysadmin** função de servidor fixa.  
  
## <a name="see-also"></a>Consulte também  
 [sp_add_jobserver &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_job &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_delete_jobserver &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_delete_targetserver &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [sp_resync_targetserver &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)   
 [sp_start_job &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [sp_stop_job &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [sp_update_job &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [sp_update_operator &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
