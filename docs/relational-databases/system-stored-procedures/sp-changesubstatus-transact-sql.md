---
title: sp_changesubstatus (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_changesubstatus
- sp_changesubstatus_TSQL
helpviewer_keywords: sp_changesubstatus
ms.assetid: 9370e47a-d128-4f15-9224-1c3642770c39
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9fb31421c8f9398e259b41f652d13a5ff8d565b5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spchangesubstatus-transact-sql"></a>sp_changesubstatus (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera o status de um Assinante existente. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, com um padrão de  **%** . Se *publicação* não for especificado, todas as publicações são afetadas.  
  
 [  **@article=**] **'***artigo***'**  
 É o nome do artigo. Deve ser exclusivo para a publicação. *artigo* é **sysname**, com um padrão de  **%** . Se *artigo* não for especificado, todos os artigos são afetados.  
  
 [  **@subscriber=**] **'***assinante***'**  
 É o nome do Assinante do qual alterar o status. *assinante* é **sysname**, com um padrão de  **%** . Se *assinante* não for especificado, status é alterado para todos os assinantes para o artigo especificado.  
  
 [  **@status =**] **'***status***'**  
 É o status da assinatura no **syssubscriptions** tabela. *status* é **sysname**, sem padrão e pode ser um destes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**ativo**|O Assinante está sincronizado e recebendo dados.|  
|**inativo**|Entrada de assinante existe sem uma assinatura.|  
|**assinado**|O Assinante está solicitando dados, mas ainda não está sincronizado.|  
  
 [  **@previous_status=**] **'***previous_status***'**  
 É o status anterior da assinatura. *previous_status* é **sysname**, com um padrão NULL. Esse parâmetro permite que você altere qualquer assinatura atualmente com esse status, permitindo que as funções de grupo em um conjunto específico de assinaturas (por exemplo, definindo ativa todas as assinaturas de volta para **inscrito**).  
  
 [  **@destination_db=**] **'***destination_db***'**  
 É o nome do banco de dados de destino. *destination_db* é **sysname**, com um padrão de  **%** .  
  
 [  **@frequency_type=**] *frequency_type*  
 É a frequência de agendamento da tarefa de distribuição. *frequency_type* é **int**, com um padrão NULL.  
  
 [  **@frequency_interval=**] *frequency_interval*  
 É o valor a ser aplicado à frequência definida *frequency_type*. *frequency_interval* é **int**, com um padrão NULL.  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 É a data da tarefa de distribuição. Esse parâmetro é usado quando *frequency_type* é definido como 32 (mensal relativo). *frequency_relative_interval* é **int**, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|First|  
|**2**|Segundo|  
|**4**|Terceiro|  
|**8**|Quarto|  
|**16**|Last|  
|NULL (padrão)||  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 É o fator de recorrência usado por *frequency_type*. *frequency_recurrence_factor* é **int**, com um padrão NULL.  
  
 [  **@frequency_subday=**] *frequency_subday*  
 É a frequência, em minutos, de reagendamento durante o período definido. *frequency_subday* é **int**, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**4**|Minuto|  
|**8**|Hora|  
|NULL (padrão)||  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 É o intervalo de *frequency_subday*. *frequency_subday_interval* é **int**, com um padrão NULL.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 É a hora do dia do primeiro agendamento da tarefa de distribuição, formatada como HHMMSS. *active_start_time_of_day* é **int**, com um padrão NULL.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 É a hora do dia do último agendamento da tarefa de distribuição, formatada como HHMMSS. *active_end_time_of_day* é **int**, com um padrão NULL.  
  
 [  **@active_start_date=**] *active_start_date*  
 É a data do primeiro agendamento da tarefa de distribuição, formatada como AAAAMMDD. *active_start_date* é **int**, com um padrão NULL.  
  
 [  **@active_end_date=**] *active_end_date*  
 É a data do último agendamento da tarefa de distribuição, formatada como AAAAMMDD. *active_end_date* é **int**, com um padrão NULL.  
  
 [  **@optional_command_line=**] **'***optional_command_line***'**  
 É um prompt de comando opcional. *optional_command_line* é **nvarchar (4000)**, com um padrão NULL.  
  
 [  **@distribution_jobid=**] *distribution_jobid*  
 É a ID de trabalho do Distribution Agent no Distribuidor para a assinatura, ao alterar o status da assinatura de inativo para ativo. Em outros casos, não é definida. Se mais de um Distribution Agent estiver envolvido em uma única chamada para esse procedimento armazenado, o resultado não será definido. *distribution_jobid* é **binário (16)**, com um padrão NULL.  
  
 [  **@from_auto_sync=**] *from_auto_sync*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@ignore_distributor=**] *ignore_distributor*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@offloadagent=** ] *remote_agent_activation*  
 > [!NOTE]  
>  A ativação do agente remoto foi preterida e não tem mais suporte. Esse parâmetro tem suporte somente para manter a compatibilidade com versões anteriores de scripts. Configuração *remote_agent_activation* para um valor diferente de **0** gera um erro.  
  
 [  **@offloadserver=** ] **'***remote_agent_server_name***'**  
 > [!NOTE]  
>  A ativação do agente remoto foi preterida e não tem mais suporte. Esse parâmetro tem suporte somente para manter a compatibilidade com versões anteriores de scripts. Configuração *remote_agent_server_name* como qualquer valor não NULL gerará um erro.  
  
 [  **@dts_package_name** =] **'***dts_package_name***'**  
 Especifica o nome do pacote DTS (Data Transformation Services). *dts_package_name* é um **sysname**, com um padrão NULL. Por exemplo, para um pacote denominado **DTSPub_Package** você especificaria `@dts_package_name = N'DTSPub_Package'`.  
  
 [  **@dts_package_password** =] **'***dts_package_password***'**  
 Especifica a senha no pacote. *dts_package_password* é **sysname** com um padrão NULL, que especifica que a propriedade de senha deve ser alterada.  
  
> [!NOTE]  
>  Um pacote DTS deve ter uma senha.  
  
 [  **@dts_package_location** =] *dts_package_location*  
 Especifica o local do pacote. *dts_package_location* é um **int**, com um padrão de **0**. Se **0**, o local do pacote é no distribuidor. Se **1**, o local do pacote é no assinante. O local do pacote pode ser **distribuidor** ou **assinante**.  
  
 [  **@skipobjectactivation** =] *skipobjectactivation*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@distribution_job_name=** ] **'***distribution_job_name***'**  
 É o nome do trabalho de distribuição. *distribution_job_name* é **sysname**, com um padrão NULL.  
  
 [  **@publisher** =] **'***publicador***'**  
 Especifica um não[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador. *publicador* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  *publicador* não deve ser usado ao alterar as propriedades de artigo em uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changesubstatus** é usado em replicação de instantâneo e replicação transacional.  
  
 **sp_changesubstatus** altera o status do assinante no **syssubscriptions** tabela com o status alterado. Se necessário, ele atualiza o status do artigo no **sysarticles** tabela para indicar ativo ou inativo. Se necessário, ele define o sinalizador de replicação ativado ou desativado **sysobjects** tabela para a tabela replicada.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função fixa de servidor **db_owner** função fixa de banco de dados ou o criador da assinatura pode executar **sp_changesubstatus**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_addsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_dropsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
