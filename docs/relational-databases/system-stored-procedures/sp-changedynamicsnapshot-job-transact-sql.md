---
description: sp_changedynamicsnapshot_job (Transact-SQL)
title: sp_changedynamicsnapshot_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedynamicsnapshot_job
- sp_changedynamicsnapshot_job_TSQL
helpviewer_keywords:
- sp_changedynamicsnapshot_job
ms.assetid: ea0dacd2-a5fd-42f4-88dd-7d289b0ae017
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 10bc612a0dc2598c973f6a6d2e3db26b5e0d69ca
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536683"
---
# <a name="sp_changedynamicsnapshot_job-transact-sql"></a>sp_changedynamicsnapshot_job (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Modifica o trabalho do agente que gera o instantâneo para uma assinatura de uma publicação com um filtro de linha com parâmetros. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publication = ] 'publication'` É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'` É o nome do trabalho de instantâneo que está sendo alterado. *dynamic_snapshot_jobname*é **sysname**, com o valor padrão de N '% '. Se *dynamic_snapshot_jobid* for especificado, você deverá usar o valor padrão para *dynamic_snapshot_jobname*.  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'` É a ID do trabalho de instantâneo que está sendo alterado. *dynamic_snapshot_jobid* é **uniqueidentifier**, com o valor padrão de NULL. Se *dynamic_snapshot_jobname*for especificado, você deverá usar o valor padrão para *dynamic_snapshot_jobid*.  
  
`[ @frequency_type = ] frequency_type` É a frequência com a qual agendar o agente. *frequency_type* é **int**e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Sob demanda|  
|**4**|Diariamente|  
|**8**|Semanalmente|  
|**16**|Mensalmente|  
|**32**|Relativo ao mês|  
|**64**|Iniciar automaticamente|  
|**128**|Recorrente|  
|NULL (padrão)||  
  
`[ @frequency_interval = ] frequency_interval` Os dias em que o agente é executado. *frequency_interval* é **int**e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Sunday|  
|**2**|Monday|  
|**3**|Terça-feira|  
|**4**|Quarta-feira|  
|**5**|Quinta-feira|  
|**6**|Friday|  
|**7**|Sábado|  
|**8**|Dia|  
|**9**|Dias da semana|  
|**10**|Dias de fim de semana|  
|NULL (padrão)||  
  
`[ @frequency_subday = ] frequency_subday` É a frequência de reagendar durante o período definido. *frequency_subday* é **int**e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**4**|Minuto|  
|**8**|Hora|  
|NULL (padrão)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` É o intervalo para *frequency_subday*. *frequency_subday_interval* é **int**, com um padrão de NULL.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` É a data em que a Agente de Mesclagem é executada. Esse parâmetro é usado quando *frequency_type* é definido como **32** (relativo mensal). *frequency_relative_interval* é **int**e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Primeiro|  
|**2**|Segundo|  
|**4**|Terceiro|  
|**8**|Quarto|  
|**16**|Último|  
|NULL (padrão)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` É o fator de recorrência usado pelo *frequency_type*. *frequency_recurrence_factor* é **int**, com um padrão de NULL.  
  
`[ @active_start_date = ] active_start_date` É a data em que o Agente de Mesclagem é agendado pela primeira vez, formatado como AAAAMMDD. *active_start_date* é **int**, com um padrão de NULL.  
  
`[ @active_end_date = ] active_end_date` É a data em que a Agente de Mesclagem para de ser agendada, formatada como AAAAMMDD. *active_end_date* é **int**, com um padrão de NULL.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` É a hora do dia em que o Agente de Mesclagem é agendado pela primeira vez, formatado como HHMMSS. *active_start_time_of_day* é **int**, com um padrão de NULL.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` É a hora do dia em que a Agente de Mesclagem para de ser agendada, formatada como HHMMSS. *active_end_time_of_day* é **int**, com um padrão de NULL.  
  
`[ @job_login = ] 'job_login'` É a [!INCLUDE[msCoName](../../includes/msconame-md.md)] conta do Windows na qual o agente de instantâneo é executado ao gerar o instantâneo para uma assinatura usando um filtro de linha com parâmetros. *job_login* é **nvarchar (257)**, com um valor padrão de NULL.  
  
`[ @job_password = ] 'job_password'` É a senha para a conta do Windows na qual o Agente de Instantâneo é executado ao gerar o instantâneo para uma assinatura usando um filtro de linha com parâmetros. *job_password* é **nvarchar (257)**, com um valor padrão de NULL.  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changedynamicsnapshot_job** é usado na replicação de mesclagem para publicações com filtros de linha com parâmetros.  
  
 Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_changedynamicsnapshot_job**.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e modificar configurações de segurança de replicação](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
  
