---
title: sp_helpdynamicsnapshot_job (Transact-SQL) | Microsoft Docs
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
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 17a7d69869e9879d485f1a8cac107836a5984a44
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpdynamicsnapshotjob-transact-sql"></a>sp_helpdynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre trabalhos de agente que geram instantâneos de dados filtrados. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpdynamicsnapshot_job [ [ @publication = ] 'publication' ]   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]  
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication =** ] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, com um padrão de **%**, que retorna informações sobre todos os trabalhos de instantâneo de dados filtrados correspondentes especificado *dynamic_ snapshot_jobid*e *dynamic_snapshot_jobname*para todas as publicações.  
  
 [  **@dynamic_snapshot_jobname =** ] **'***dynamic_snapshot_jobname***'**  
 É o nome de um trabalho de instantâneo de dados filtrados. *dynamic_snapshot_jobname*é **sysname**, com padrão de **%**', que retorna todos os trabalhos dinâmicos de uma publicação com especificado *dynamic_ snapshot_jobid*. Se um nome de trabalho não tiver sido explicitamente especificado quando o trabalho foi criado, o nome do trabalho terá o seguinte formato:  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
 [  **@dynamic_snapshot_jobid =** ] **'***dynamic_snapshot_jobid***'**  
 É um identificador de um trabalho de instantâneo de dados filtrados. *dynamic_snapshot_jobid*é **uniqueidentifier**, com padrão de NULL, que retorna todos os trabalhos de instantâneo que correspondem à cadeia *dynamic_snapshot_jobname*.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**id**|**Int**|Identifica o trabalho de instantâneo de dados filtrado.|  
|**job_name**|**sysname**|Nome do trabalho de instantâneo de dados filtrado.|  
|**job_id**|**uniqueidentifier**|Identifica o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no distribuidor.|  
|**dynamic_filter_login**|**sysname**|Valor usado para avaliar o [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) função em um filtro de linha com parâmetros definido para a publicação.|  
|**dynamic_filter_hostname**|**sysname**|Valor usado para avaliar o [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) função em um filtro de linha com parâmetros definido para a publicação.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|Caminho para a pasta onde os arquivos de instantâneo são lidos se um filtro de linha com parâmetros for usado.|  
|**frequency_type**|**Int**|É a frequência de agendamento para execução do agente, que pode ser um dos valores a seguir.<br /><br /> **1** = uma vez<br /><br /> **2** = sob demanda<br /><br /> **4** = diariamente<br /><br /> **8** = semanalmente<br /><br /> **16** = mensalmente<br /><br /> **32** = relativo ao mês<br /><br /> **64** = iniciar automaticamente<br /><br /> **128** = recorrente|  
|**frequency_interval**|**Int**|Os dias de execução do agente, que pode ter um destes valores.<br /><br /> **1** = domingo<br /><br /> **2** = segunda-feira<br /><br /> **3** = terça-feira<br /><br /> **4** = quarta-feira<br /><br /> **5** = quinta-feira<br /><br /> **6** = sexta-feira<br /><br /> **7** = sábado<br /><br /> **8** = dia<br /><br /> **9** = dias da semana<br /><br /> **10** = semana|  
|**frequency_subday_type**|**Int**|É o tipo que define a frequência na qual o agente é executado quando *frequency_type* é **4** (diariamente), e pode ser um destes valores.<br /><br /> **1** = na hora especificada<br /><br /> **2** = segundos<br /><br /> **4** = minutos<br /><br /> **8** = horas|  
|**frequency_subday_interval**|**Int**|Número de intervalos de *frequency_subday_type* que ocorre entre execuções programadas do agente.|  
|**frequency_relative_interval**|**Int**|É a que o agente é executado em um determinado mês quando *frequency_type* é **32** (mensal relativo), e pode ser um destes valores.<br /><br /> **1** = primeiro<br /><br /> **2** = segundo<br /><br /> **4** = terceiro<br /><br /> **8** = quarto<br /><br /> **16** = último|  
|**frequency_recurrence_factor**|**Int**|Número de semanas ou meses entre execuções programadas do agente.|  
|**active_start_date**|**Int**|Data do primeiro agendamento de execução do agente, formatada como YYYYMMDD.|  
|**active_end_date**|**Int**|Data do último agendamento de execução do agente, formatada como YYYYMMDD.|  
|**active_start_time**|**Int**|Hora do primeiro agendamento de execução do agente, formatada como HHMMSS.|  
|**active_end_time**|**Int**|Hora do último agendamento de execução do agente, formatada como HHMMSS.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_helpdynamicsnapshot_job** é usado em replicação de mesclagem.  
  
 Se todos os valores de parâmetro padrão forem usados, informações sobre todos os trabalhos de instantâneo de dados particionados serão retornadas.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa, o **db_owner** fixo de função de banco de dados e a lista de acesso da publicação para a publicação pode executar **sp_helpdynamicsnapshot_job**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
