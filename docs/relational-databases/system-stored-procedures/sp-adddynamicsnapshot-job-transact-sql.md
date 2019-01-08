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
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 79412d81e0a16443f3fec515d1d866c3aff1804c
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52771218"
---
# <a name="spadddynamicsnapshotjob-transact-sql"></a>sp_adddynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria um trabalho de agente que gera um instantâneo de dados filtrado para uma publicação com filtros de linha com parâmetros. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador. Esse procedimento armazenado é usado por um administrador para criar trabalhos de instantâneo de dados manualmente filtrados para Assinantes.  
  
> [!NOTE]  
>  Para que um trabalho de instantâneo de dados filtrados seja criado, um trabalho de instantâneo padrão para a publicação deve existir.  
  
 Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
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
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação à qual o trabalho de instantâneo de dados filtrados está sendo adicionado. *publicação* está **sysname**, sem padrão.  
  
 [ **@suser_sname**=] **'***suser_sname***'**  
 É o valor usado ao criar um instantâneo de dados filtrados para uma assinatura filtrada pelo valor da [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) função no assinante. *suser_sname* está **sysname**, sem padrão. *suser_sname* deve ser NULL se essa função não é usada para filtrar dinamicamente a publicação.  
  
 [ **@host_name**=] **'***host_name***'**  
 É o valor usado ao criar um instantâneo de dados filtrados para uma assinatura filtrada pelo valor da [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) função no assinante. *HOST_NAME* está **sysname**, sem padrão. *HOST_NAME* deve ser NULL se essa função não é usada para filtrar dinamicamente a publicação.  
  
 [ **@dynamic_snapshot_jobname**=] **'***dynamic_snapshot_jobname***'**  
 É o nome do trabalho de instantâneo de dados filtrados criado. *dynamic_snapshot_jobname* está **sysname**, com padrão de NULL, e é um parâmetro OUTPUT opcional. Se especificado, *dynamic_snapshot_jobname* deve resolver para um trabalho único no distribuidor. Se não for especificado, um nome de trabalho será automaticamente gerado e retornado no conjunto de resultados, onde o nome será criado como segue:  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
> [!NOTE]  
>  Ao gerar o nome do trabalho de instantâneo dinâmico, você pode truncar o nome do trabalho de instantâneo padrão.  
  
 [ **@dynamic_snapshot_jobid**=] **'***dynamic_snapshot_jobid***'**  
 É um identificador do trabalho de instantâneo de dados filtrados criado. *dynamic_snapshot_jobid* está **uniqueidentifier**, com padrão de NULL, e é um parâmetro OUTPUT opcional.  
  
 [  **@frequency_type=**] *frequency_type*  
 É a frequência do agendamento do trabalho de instantâneo de dados filtrados. *frequency_type* está **int**, e pode ser um destes valores.  
  
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
  
 [  **@frequency_interval =** ] *frequency_interval*  
 É o período (medido em dias) quando o trabalho de instantâneo de dados filtrados é executado. *frequency_interval* está **int**, com um valor padrão de 1 e depende do valor de *frequency_type*.  
  
|Valor de *frequency_type*|Efeito em *frequency_interval*|  
|--------------------------------|-------------------------------------|  
|**1**|*frequency_interval* não é usado.|  
|**4** (padrão)|Cada *frequency_interval* dias, com um padrão de diariamente.|  
|**8**|*frequency_interval* é um ou mais dos seguintes (combinado com um [ &#124; &#40;OR bit a bit&#41; &#40;Transact-SQL&#41; ](../../t-sql/language-elements/bitwise-or-transact-sql.md) operador lógico):<br /><br /> **1** = domingo &#124; **2** = segunda-feira &#124; **4** = terça-feira &#124; **8** = quarta-feira &#124; **16** = Quinta-feira &#124; **32** = sexta-feira &#124; **64** = sábado|  
|**16**|Sobre o *frequency_interval* dia do mês.|  
|**32**|*frequency_interval* é um dos seguintes:<br /><br /> **1** = domingo &#124; **2** = segunda-feira &#124; **3** = terça-feira &#124; **4** = quarta-feira &#124; **5** = Quinta-feira &#124; **6** = sexta-feira &#124; **7** = sábado &#124; **8** = dia &#124; **9** = dia da semana &#124; **10** = dia de fim de semana|  
|**64**|*frequency_interval* não é usado.|  
|**128**|*frequency_interval* não é usado.|  
  
 [  **@frequency_subday=**] *frequency_subday*  
 Especifica as unidades para *frequency_subday_interval*. *frequency_subday* está **int**, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**4** (padrão)|Minuto|  
|**8**|Hora|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 É o número de *frequency_subday* períodos que ocorrem entre cada execução do trabalho. *frequency_subday_interval* está **int**, com um padrão de 5.  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 É a ocorrência do trabalho de instantâneo de dados filtrado em cada mês. Esse parâmetro é usado quando *frequency_type* é definido como **32** (mensal relativo). *frequency_relative_interval* está **int**, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1** (padrão)|First|  
|**2**|Segundo|  
|**4**|Terceiro|  
|**8**|Quarto|  
|**16**|Last|  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 É o fator de recorrência usado pelo *frequency_type*. *frequency_recurrence_factor* está **int**, com um padrão de 0.  
  
 [  **@active_start_date=**] *active_start_date*  
 É a data do primeiro agendamento do trabalho de instantâneo de dados filtrados, formatada como AAAAMMDD. *active_start_date* está **int**, com um padrão NULL.  
  
 [  **@active_end_date=**] *active_end_date*  
 É a data do último agendamento do trabalho de instantâneo de dados filtrados, formatada como AAAAMMDD. *active_end_date* está **int**, com um padrão NULL.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 É a hora do dia do primeiro agendamento do trabalho de instantâneo de dados filtrados, formatada como HHMMSS. *active_start_time_of_day* está **int**, com um padrão NULL.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 A hora do dia quando o trabalho for interrompido de instantâneo os dados filtrados está sendo agendada, formatada como HHMMSS. *active_end_time_of_day* está **int**, com um padrão NULL.  
  
## <a name="result-set"></a>Conjunto de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identifica o trabalho de instantâneo de dados filtrados na [MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md) tabela do sistema.|  
|**dynamic_snapshot_jobname**|**sysname**|Nome do trabalho de instantâneo de dados filtrado.|  
|**dynamic_snapshot_jobid**|**uniqueidentifier**|Identifica exclusivamente o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no distribuidor.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_adddynamicsnapshot_job** é usado em replicação de mesclagem para publicações que usam um filtro com parâmetros.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/sp-adddynamicsnapshot-jo_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou o **db_owner** banco de dados fixa podem executar **sp_adddynamicsnapshot_job**.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um instantâneo para uma publicação de mesclagem com filtros com parâmetros](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [sp_dropdynamicsnapshot_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdynamicsnapshot-job-transact-sql.md)   
 [sp_helpdynamicsnapshot_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdynamicsnapshot-job-transact-sql.md)  
  
  
