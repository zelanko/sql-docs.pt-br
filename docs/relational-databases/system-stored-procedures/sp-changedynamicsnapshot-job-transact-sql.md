---
title: sp_changedynamicsnapshot_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_changedynamicsnapshot_job
- sp_changedynamicsnapshot_job_TSQL
helpviewer_keywords:
- sp_changedynamicsnapshot_job
ms.assetid: ea0dacd2-a5fd-42f4-88dd-7d289b0ae017
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2c31883e19d688dd7158ece061144ae7d44ccf30
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32992163"
---
# <a name="spchangedynamicsnapshotjob-transact-sql"></a>sp_changedynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica o trabalho do agente que gera o instantâneo para uma assinatura de uma publicação com um filtro de linha com parâmetros. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changedynamicsnapshot_job [ @publication = ] 'publication'  
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]  
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]  
    [ , [ @frequency_type = ] frequency_type ]   
    [ , [ @frequency_interval = ] frequency_interval ]   
    [ , [ @frequency_subday = ] frequency_subday ]   
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]   
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]   
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]   
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]   
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication =** ] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, sem padrão.  
  
 [  **@dynamic_snapshot_jobname =** ] **'***dynamic_snapshot_jobname***'**  
 É o nome do trabalho de instantâneo que está sendo alterado. *dynamic_snapshot_jobname*é **sysname**, com o valor padrão de n' %'. Se *dynamic_snapshot_jobid* for especificado, você deve usar o valor padrão para *dynamic_snapshot_jobname*.  
  
 [  **@dynamic_snapshot_jobid =** ] **'***dynamic_snapshot_jobid***'**  
 É a ID do trabalho de instantâneo que está sendo alterado. *dynamic_snapshot_jobid* é **uniqueidentifier**, com o valor padrão de NULL. Se *dynamic_snapshot_jobname*for especificado, você deve usar o valor padrão para *dynamic_snapshot_jobid*.  
  
 [  **@frequency_type =** ] *frequency_type*  
 É a frequência de agendamento do agente. *frequency_type* é **int**, e pode ser um dos valores a seguir.  
  
|Value|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Sob Demanda|  
|**4**|Diariamente|  
|**8**|Semanalmente|  
|**16**|Mensalmente|  
|**32**|Relativo ao mês|  
|**64**|Iniciar automaticamente|  
|**128**|Recorrente|  
|NULL (padrão)||  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 Os dias em que o agente é executado. *frequency_interval* é **int**, e pode ser um dos valores a seguir.  
  
|Value|Descrição|  
|-----------|-----------------|  
|**1**|Domingo|  
|**2**|Segunda-feira|  
|**3**|Terça-feira|  
|**4**|Quarta-feira|  
|**5**|Quinta-feira|  
|**6**|Sexta-feira|  
|**7**|Sábado|  
|**8**|Day|  
|**9**|Dias da semana|  
|**10**|Dias de fim de semana|  
|NULL (padrão)||  
  
 [  **@frequency_subday =** ] *frequency_subday*  
 É a frequência de reagendamento durante o período definido. *frequency_subday* é **int**, e pode ser um dos valores a seguir.  
  
|Value|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**4**|Minuto|  
|**8**|Hora|  
|NULL (padrão)||  
  
 [  **@frequency_subday_interval =** ] *frequency_subday_interval*  
 É o intervalo de *frequency_subday*. *frequency_subday_interval* é **int**, com um padrão NULL.  
  
 [  **@frequency_relative_interval =** ] *frequency_relative_interval*  
 É a data de execução do Agente de Mesclagem. Esse parâmetro é usado quando *frequency_type* é definido como **32** (mensal relativo). *frequency_relative_interval* é **int**, e pode ser um dos valores a seguir.  
  
|Value|Descrição|  
|-----------|-----------------|  
|**1**|First|  
|**2**|Segundo|  
|**4**|Terceiro|  
|**8**|Quarto|  
|**16**|Last|  
|NULL (padrão)||  
  
 [  **@frequency_recurrence_factor =** ] *frequency_recurrence_factor*  
 É o fator de recorrência usado por *frequency_type*. *frequency_recurrence_factor* é **int**, com um padrão NULL.  
  
 [  **@active_start_date =** ] *active_start_date*  
 É a data do primeiro agendamento do Agente de Mesclagem, formatada como AAAAMMDD. *active_start_date* é **int**, com um padrão NULL.  
  
 [  **@active_end_date =** ] *active_end_date*  
 É a data do último agendamento do Agente de Mesclagem, formatada como AAAAMMDD. *active_end_date* é **int**, com um padrão NULL.  
  
 [  **@active_start_time_of_day =** ] *active_start_time_of_day*  
 É a hora do dia do primeiro agendamento do Agente de Mesclagem, formatada como HHMMSS. *active_start_time_of_day* é **int**, com um padrão NULL.  
  
 [  **@active_end_time_of_day =** ] *active_end_time_of_day*  
 É a hora do dia do último agendamento do Agente de Mesclagem, formatada como HHMMSS. *active_end_time_of_day* é **int**, com um padrão NULL.  
  
 [  **@job_login=** ] **'***job_login***'**  
 É a conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows sob a qual o Agente de Instantâneo é executado ao gerar o instantâneo para uma assinatura usando um filtro de linha com parâmetros. *job_login* é **nvarchar (257)**, com um valor padrão de NULL.  
  
 [  **@job_password=** ] **'***job_password***'**  
 É a senha da conta do Windows na qual o Agente de Instantâneo é executado ao gerar o instantâneo para uma assinatura usando um filtro de linha com parâmetros. *job_password* é **nvarchar (257)**, com um valor padrão de NULL.  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_changedynamicsnapshot_job** é usado em replicação de mesclagem para publicações com filtros de linha com parâmetros.  
  
 Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_changedynamicsnapshot_job**.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar configurações de segurança de replicação](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  
