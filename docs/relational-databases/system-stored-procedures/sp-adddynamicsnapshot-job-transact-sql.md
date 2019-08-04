---
title: sp_adddynamicsnapshot_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_adddynamicsnapshot_job
- sp_adddynamicsnapshot_job_TSQL
helpviewer_keywords:
- sp_adddynamicsnapshot_job
ms.assetid: ef50ccf6-e360-4e4b-91b9-6706b8fabefa
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 48f94f7fcf823a9ed9acc519e393369e44b45302
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771337"
---
# <a name="spadddynamicsnapshotjob-transact-sql"></a>sp_adddynamicsnapshot_job (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Cria um trabalho de agente que gera um instantâneo de dados filtrado para uma publicação com filtros de linha com parâmetros. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador. Esse procedimento armazenado é usado por um administrador para criar trabalhos de instantâneo de dados manualmente filtrados para Assinantes.  
  
> [!NOTE]  
>  Para que um trabalho de instantâneo de dados filtrados seja criado, um trabalho de instantâneo padrão para a publicação deve existir.  
  
 Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_adddynamicsnapshot_job [ @publication = ] 'publication'   
    [ , [ @suser_sname = ] 'suser_sname' ]   
    [ , [ @host_name = ] 'host_name' ]   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' OUTPUT ]   
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' OUTPUT ]   
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação à qual o trabalho de instantâneo de dados filtrado está sendo adicionado. a *publicação* é **sysname**, sem padrão.  
  
`[ @suser_sname = ] 'suser_sname'`É o valor usado ao criar um instantâneo de dados filtrados para uma assinatura que é filtrada pelo valor da função [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) no Assinante. *SUSER_SNAME* é **sysname**, sem padrão. *SUSER_SNAME* deve ser nulo se essa função não for usada para filtrar dinamicamente a publicação.  
  
`[ @host_name = ] 'host_name'`É o valor usado ao criar um instantâneo de dados filtrados para uma assinatura que é filtrada pelo valor da função [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) no Assinante. *HOST_NAME* é **sysname**, sem padrão. *HOST_NAME* deve ser NULL se essa função não for usada para filtrar dinamicamente a publicação.  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'`É o nome do trabalho de instantâneo de dados filtrado criado. *dynamic_snapshot_jobname* é **sysname**, com default de NULL, e é um parâmetro de saída opcional. Se especificado, *dynamic_snapshot_jobname* deverá resolver para um trabalho exclusivo no distribuidor. Se não for especificado, um nome de trabalho será automaticamente gerado e retornado no conjunto de resultados, onde o nome será criado como segue:  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
> [!NOTE]  
>  Ao gerar o nome do trabalho de instantâneo dinâmico, você pode truncar o nome do trabalho de instantâneo padrão.  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'`É um identificador para o trabalho de instantâneo de dados filtrado criado. *dynamic_snapshot_jobid* é **uniqueidentifier**, com padrão NULL, e é um parâmetro de saída opcional.  
  
`[ @frequency_type = ] frequency_type`É a frequência com a qual agendar o trabalho de instantâneo de dados filtrado. *frequency_type* é **int**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Sob Demanda|  
|**4** (padrão)|Diariamente|  
|**8**|Semanalmente|  
|**16**|Mensalmente|  
|**32**|Relativo ao mês|  
|**64**|Iniciar automaticamente|  
|**128**|Recorrente|  
  
`[ @frequency_interval = ] frequency_interval`É o período (medido em dias) quando o trabalho de instantâneo de dados filtrado é executado. *frequency_interval* é **int**, com um valor padrão de 1, e depende do valor de *frequency_type*.  
  
|Valor de *frequency_type*|Efeito em *frequency_interval*|  
|--------------------------------|-------------------------------------|  
|**1**|*frequency_interval* não é usado.|  
|**4** (padrão)|A cada *frequency_interval* dias, com um padrão de diariamente.|  
|**8**|*frequency_interval* é um ou mais dos itens a seguir (combinados com um operador lógico de [ &#124; &#40;Transact-&#41; &#40;&#41; SQL ou](../../t-sql/language-elements/bitwise-or-transact-sql.md) de bits):<br /><br /> **1** = domingo &#124; **2** = segunda-feira &#124; **4** = terça &#124; -feira **8** = quarta &#124; - &#124; feira **16** = quinta-feira **32** = sexta-feira &#124; **64** = sábado|  
|**16**|No dia *frequency_interval* do mês.|  
|**32**|*frequency_interval* é um dos seguintes:<br /><br /> **1** = domingo &#124; **2** = segunda-feira &#124; **3** = terça &#124; -feira **4** = quarta &#124; - &#124; feira **5** = &#124; quinta-feira **6** = sexta &#124; -feira **7** = sábado &#124; **8** = dia **9** = Weekday &#124; **10** = dia do fim de semana|  
|**64**|*frequency_interval* não é usado.|  
|**128**|*frequency_interval* não é usado.|  
  
`[ @frequency_subday = ] frequency_subday`Especifica as unidades para *frequency_subday_interval*. *frequency_subday* é **int**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**4** (padrão)|Minuto|  
|**8**|Hora|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`É o número de períodos de *frequency_subday* que ocorrem entre cada execução do trabalho. *frequency_subday_interval* é **int**, com um padrão de 5.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`É a ocorrência do trabalho de instantâneo de dados filtrados em cada mês. Esse parâmetro é usado quando *frequency_type* é definido como **32** (relativo mensal). *frequency_relative_interval* é **int**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1** (padrão)|First|  
|**2**|Segundo|  
|**4**|Terceiro|  
|**8**|Quarto|  
|**16**|Last|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`É o fator de recorrência usado pelo *frequency_type*. *frequency_recurrence_factor* é **int**, com um padrão de 0.  
  
`[ @active_start_date = ] active_start_date`É a data em que o trabalho de instantâneo de dados filtrado é agendado pela primeira vez, formatado como AAAAMMDD. *active_start_date* é **int**, com um padrão de NULL.  
  
`[ @active_end_date = ] active_end_date`É a data em que o trabalho de instantâneo de dados filtrado pára de ser agendado, formatado como AAAAMMDD. *active_end_date* é **int**, com um padrão de NULL.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`É a hora do dia em que o trabalho de instantâneo de dados filtrado é agendado pela primeira vez, formatado como HHMMSS. *active_start_time_of_day* é **int**, com um padrão de NULL.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`É a hora do dia em que o trabalho de instantâneo de dados filtrado pára de ser agendado, formatado como HHMMSS. *active_end_time_of_day* é **int**, com um padrão de NULL.  
  
## <a name="result-set"></a>Conjunto de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identifica o trabalho de instantâneo de dados filtrado na tabela do sistema [MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md) .|  
|**dynamic_snapshot_jobname**|**sysname**|Nome do trabalho de instantâneo de dados filtrado.|  
|**dynamic_snapshot_jobid**|**uniqueidentifier**|Identifica exclusivamente o trabalho [!INCLUDE[msCoName](../../includes/msconame-md.md)] do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente no distribuidor.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_adddynamicsnapshot_job** é usado na replicação de mesclagem para publicações que usam um filtro com parâmetros.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/sp-adddynamicsnapshot-jo_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou da função de banco de dados fixa **db_owner** podem executar **sp_adddynamicsnapshot_job**.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um instantâneo para uma publicação de mesclagem com filtros com parâmetros](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [sp_dropdynamicsnapshot_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdynamicsnapshot-job-transact-sql.md)   
 [sp_helpdynamicsnapshot_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdynamicsnapshot-job-transact-sql.md)  
  
  
