---
title: sp_changesubstatus (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changesubstatus
- sp_changesubstatus_TSQL
helpviewer_keywords:
- sp_changesubstatus
ms.assetid: 9370e47a-d128-4f15-9224-1c3642770c39
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2daa7d007783434e0994846e41300c31b3e35162
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771356"
---
# <a name="sp_changesubstatus-transact-sql"></a>sp_changesubstatus (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Altera o status de um Assinante existente. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changesubstatus [ [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
    [ , [ @subscriber = ] 'subscriber' ]  
        , [ @status = ] 'status'  
    [ , [ @previous_status = ] 'previous_status' ]  
    [ , [ @destination_db = ] 'destination_db' ]  
    [ , [ @frequency_type = ] frequency_type ]  
    [ , [ @frequency_interval = ] frequency_interval ]  
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday = ] frequency_subday ]  
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]  
    [ , [ @active_start_date = ] active_start_date ]  
    [ , [ @active_end_date = ] active_end_date ]  
    [ , [ @optional_command_line = ] 'optional_command_line' ]  
    [ , [ @distribution_jobid = ] distribution_jobid ]  
    [ , [ @from_auto_sync = ] from_auto_sync ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @offloadagent= ] remote_agent_activation ]  
    [ , [ @offloadserver= ] 'remote_agent_server_name' ]  
    [ , [ @dts_package_name= ] 'dts_package_name' ]  
    [ , [ @dts_package_password= ] 'dts_package_password' ]  
    [ , [ @dts_package_location= ] dts_package_location ]  
    [ , [ @skipobjectactivation = ] skipobjectactivation  
  [ , [ @distribution_job_name= ] 'distribution_job_name' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, com um padrão de **%** . Se a *publicação* não for especificada, todas as publicações serão afetadas.  
  
`[ @article = ] 'article'`É o nome do artigo. Deve ser exclusivo para a publicação. o *artigo* é **sysname**, com um padrão de **%** . Se o *artigo* não for especificado, todos os artigos serão afetados.  
  
`[ @subscriber = ] 'subscriber'`É o nome do assinante do qual alterar o status. o *assinante* é **sysname**, com um padrão de **%** . Se o *assinante* não for especificado, o status será alterado para todos os assinantes para o artigo especificado.  
  
`[ @status = ] 'status'`É o status da assinatura na tabela **syssubscriptions** . *status* é **sysname**, sem padrão, e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**active**|O Assinante está sincronizado e recebendo dados.|  
|**inactive**|Entrada de assinante existe sem uma assinatura.|  
|**assinado**|O Assinante está solicitando dados, mas ainda não está sincronizado.|  
  
`[ @previous_status = ] 'previous_status'`É o status anterior da assinatura. *previous_status* é **sysname**, com um padrão de NULL. Esse parâmetro permite que você altere todas as assinaturas que atualmente têm esse status, permitindo que funções de grupo em um conjunto específico de assinaturas (por exemplo, definindo todas as assinaturas ativas de volta para **assinadas**).  
  
`[ @destination_db = ] 'destination_db'`É o nome do banco de dados de destino. *destination_db* é **sysname**, com um padrão de **%** .  
  
`[ @frequency_type = ] frequency_type`É a frequência com a qual agendar a tarefa de distribuição. *frequency_type* é **int**, com um padrão de NULL.  
  
`[ @frequency_interval = ] frequency_interval`É o valor a ser aplicado à frequência definida por *frequency_type*. *frequency_interval* é **int**, com um padrão de NULL.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`É a data da tarefa de distribuição. Esse parâmetro é usado quando *frequency_type* é definido como 32 (relativo mensal). *frequency_relative_interval* é **int**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Primeiro|  
|**2**|Segundo|  
|**4**|Terceiro|  
|**8**|Quarto|  
|**16**|Último|  
|NULL (padrão)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`É o fator de recorrência usado pelo *frequency_type*. *frequency_recurrence_factor* é **int**, com um padrão de NULL.  
  
`[ @frequency_subday = ] frequency_subday`É a frequência, em minutos, para reagendar durante o período definido. *frequency_subday* é **int**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**4**|Minuto|  
|**8**|Hora|  
|NULL (padrão)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`É o intervalo para *frequency_subday*. *frequency_subday_interval* é **int**, com um padrão de NULL.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`É a hora do dia em que a tarefa de distribuição é agendada pela primeira vez, formatada como HHMMSS. *active_start_time_of_day* é **int**, com um padrão de NULL.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`É a hora do dia em que a tarefa de distribuição para de ser agendada, formatada como HHMMSS. *active_end_time_of_day* é **int**, com um padrão de NULL.  
  
`[ @active_start_date = ] active_start_date`É a data em que a tarefa de distribuição é agendada pela primeira vez, formatada como AAAAMMDD. *active_start_date* é **int**, com um padrão de NULL.  
  
`[ @active_end_date = ] active_end_date`É a data em que a tarefa de distribuição para de ser agendada, formatada como AAAAMMDD. *active_end_date* é **int**, com um padrão de NULL.  
  
`[ @optional_command_line = ] 'optional_command_line'`É um prompt de comando opcional. *optional_command_line* é **nvarchar (4000)**, com um padrão de NULL.  
  
`[ @distribution_jobid = ] distribution_jobid`É a ID do trabalho do Agente de Distribuição no distribuidor para a assinatura ao alterar o status da assinatura de inativo para ativo. Em outros casos, não é definida. Se mais de um Distribution Agent estiver envolvido em uma única chamada para esse procedimento armazenado, o resultado não será definido. *distribution_jobid* é **binary (16)**, com um padrão de NULL.  
  
`[ @from_auto_sync = ] from_auto_sync` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @ignore_distributor = ] ignore_distributor` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @offloadagent = ] remote_agent_activation`
 > [!NOTE]  
>  A ativação do agente remoto foi preterida e não tem mais suporte. Esse parâmetro tem suporte somente para manter a compatibilidade com versões anteriores de scripts. A configuração de *remote_agent_activation* com um valor diferente de **0** gera um erro.  
  
`[ @offloadserver = ] 'remote_agent_server_name'`
 > [!NOTE]  
>  A ativação do agente remoto foi preterida e não tem mais suporte. Esse parâmetro tem suporte somente para manter a compatibilidade com versões anteriores de scripts. A definição de *remote_agent_server_name* para qualquer valor não nulo gera um erro.  
  
`[ @dts_package_name = ] 'dts_package_name'`Especifica o nome do pacote DTS (Data Transformation Services). *dts_package_name* é um **sysname**, com um padrão de NULL. Por exemplo, para um pacote chamado **DTSPub_Package** você especificaria `@dts_package_name = N'DTSPub_Package'` .  
  
`[ @dts_package_password = ] 'dts_package_password'`Especifica a senha no pacote. *dts_package_password* é **sysname** com um padrão de NULL, que especifica que a propriedade password deve ser deixada inalterada.  
  
> [!NOTE]  
>  Um pacote DTS deve ter uma senha.  
  
`[ @dts_package_location = ] dts_package_location`Especifica o local do pacote. *dts_package_location* é um **int**, com um padrão de **0**. Se for **0**, o local do pacote estará no distribuidor. Se for **1**, o local do pacote será o Assinante. O local do pacote pode ser **distribuidor** ou **assinante**.  
  
`[ @skipobjectactivation = ] skipobjectactivation` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @distribution_job_name = ] 'distribution_job_name'`É o nome do trabalho de distribuição. *distribution_job_name* é **sysname**, com um padrão de NULL.  
  
`[ @publisher = ] 'publisher'`Especifica um não [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o *Publicador* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  o *Publicador* não deve ser usado ao alterar as propriedades do artigo em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changesubstatus** é usado na replicação de instantâneo e na replicação transacional.  
  
 **sp_changesubstatus** altera o status do Assinante na tabela **syssubscriptions** com o status alterado. Se necessário, ele atualiza o status do artigo na tabela **sysarticles** para indicar ativo ou inativo. Se necessário, ele define o sinalizador de replicação ativado ou desativado na tabela **sysobjects** para a tabela replicada.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** , **db_owner** função de banco de dados fixa ou o criador da assinatura podem executar **sp_changesubstatus**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropsubscription](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpdistributor](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
