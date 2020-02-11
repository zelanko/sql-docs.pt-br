---
title: sp_helpdynamicsnapshot_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdynamicsnapshot_TSQL
- sp_helpdynamicsnapshot_job_TSQL
- job_TSQL
- helpdynamicsnapshot
- job
- sp_helpdynamicsnapshot
- sp_helpdynamicsnapshot_job
- helpdynamicsnapshot_TSQL
helpviewer_keywords:
- sp_helpdynamicsnapshot_job
ms.assetid: d6dfdf26-f874-495f-a8a6-8780699646d7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 55d7ad0dfd941102cfeb6661e65980f980fa8b2d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68770983"
---
# <a name="sp_helpdynamicsnapshot_job-transact-sql"></a>sp_helpdynamicsnapshot_job (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Retorna informações sobre trabalhos de agente que geram instantâneos de dados filtrados. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpdynamicsnapshot_job [ [ @publication = ] 'publication' ]   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]  
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, com um padrão **%** de, que retorna informações sobre todos os trabalhos de instantâneo de dados filtrados que correspondem ao *dynamic_snapshot_jobid*especificado e *dynamic_snapshot_jobname*para todas as publicações.  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'`É o nome de um trabalho de instantâneo de dados filtrado. *dynamic_snapshot_jobname*é **sysname**, com o padrão **%**', que retorna todos os trabalhos dinâmicos para uma publicação com o *dynamic_snapshot_jobid*especificado. Se um nome de trabalho não tiver sido explicitamente especificado quando o trabalho foi criado, o nome do trabalho terá o seguinte formato:  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'`É um identificador para um trabalho de instantâneo de dados filtrado. *dynamic_snapshot_jobid*é **uniqueidentifier**, com o padrão NULL, que retorna todos os trabalhos de instantâneo que correspondem ao *dynamic_snapshot_jobname*especificado.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**sessão**|**int**|Identifica o trabalho de instantâneo de dados filtrado.|  
|**job_name**|**sysname**|Nome do trabalho de instantâneo de dados filtrado.|  
|**job_id**|**uniqueidentifier**|Identifica o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabalho do agente no distribuidor.|  
|**dynamic_filter_login**|**sysname**|Valor usado para avaliar a função [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) em um filtro de linha com parâmetros definido para a publicação.|  
|**dynamic_filter_hostname**|**sysname**|Valor usado para avaliar a função [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) em um filtro de linha com parâmetros definido para a publicação.|  
|**dynamic_snapshot_location**|**nvarchar (255)**|Caminho para a pasta onde os arquivos de instantâneo são lidos se um filtro de linha com parâmetros for usado.|  
|**frequency_type**|**int**|É a frequência de agendamento para execução do agente, que pode ser um dos valores a seguir.<br /><br /> **1** = uma vez<br /><br /> **2** = sob demanda<br /><br /> **4** = diariamente<br /><br /> **8** = semanalmente<br /><br /> **16** = mensalmente<br /><br /> **32** = relativo mensal<br /><br /> **64** = inicialização automática<br /><br /> **128** = recorrente|  
|**frequency_interval**|**int**|Os dias de execução do agente, que pode ter um destes valores.<br /><br /> **1** = domingo<br /><br /> **2** = segunda-feira<br /><br /> **3** = terça-feira<br /><br /> **4** = quarta-feira<br /><br /> **5** = quinta-feira<br /><br /> **6** = sexta-feira<br /><br /> **7** = sábado<br /><br /> **8** = dia<br /><br /> **9** = dias da semana<br /><br /> **10** = dias de semana|  
|**frequency_subday_type**|**int**|É o tipo que define a frequência com que o agente é executado quando *frequency_type* é **4** (diariamente) e pode ser um desses valores.<br /><br /> **1** = na hora especificada<br /><br /> **2** = segundos<br /><br /> **4** = minutos<br /><br /> **8** = horas|  
|**frequency_subday_interval**|**int**|Número de intervalos de *frequency_subday_type* que ocorrem entre a execução agendada do agente.|  
|**frequency_relative_interval**|**int**|É a semana em que o agente é executado em um determinado mês quando *frequency_type* é **32** (relativo mensal) e pode ser um desses valores.<br /><br /> **1** = primeiro<br /><br /> **2** = segundo<br /><br /> **4** = terceiro<br /><br /> **8** = quarto<br /><br /> **16** = última|  
|**frequency_recurrence_factor**|**int**|Número de semanas ou meses entre execuções programadas do agente.|  
|**active_start_date**|**int**|Data do primeiro agendamento de execução do agente, formatada como YYYYMMDD.|  
|**active_end_date**|**int**|Data do último agendamento de execução do agente, formatada como YYYYMMDD.|  
|**active_start_time**|**int**|Hora do primeiro agendamento de execução do agente, formatada como HHMMSS.|  
|**active_end_time**|**int**|Hora do último agendamento de execução do agente, formatada como HHMMSS.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpdynamicsnapshot_job** é usado na replicação de mesclagem.  
  
 Se todos os valores de parâmetro padrão forem usados, informações sobre todos os trabalhos de instantâneo de dados particionados serão retornadas.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** , a função de banco de dados fixa **db_owner** e a lista de acesso à publicação da publicação podem ser executados **sp_helpdynamicsnapshot_job**.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
