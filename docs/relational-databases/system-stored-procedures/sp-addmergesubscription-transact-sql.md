---
title: sp_addmergesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_addmergesubscription_TSQL
- sp_addmergesubscription
helpviewer_keywords:
- sp_addmergesubscription
ms.assetid: a191d817-0132-49ff-93ca-76f13e609b38
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 56355da01ed689279680d595b6b0733b2fc26413
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spaddmergesubscription-transact-sql"></a>sp_addmergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria uma assinatura push ou pull. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addmergesubscription [ @publication= ] 'publication'  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db= ] 'subscriber_db' ]  
    [ , [ @subscription_type= ] 'subscription_type' ]  
    [ , [ @subscriber_type= ] 'subscriber_type' ]  
    [ , [ @subscription_priority= ] subscription_priority ]  
    [ , [ @sync_type= ] 'sync_type' ]  
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @optional_command_line= ] 'optional_command_line' ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @enabled_for_syncmgr= ] 'enabled_for_syncmgr' ]  
    [ , [ @offloadagent= ] remote_agent_activation]  
    [ , [ @offloadserver= ] 'remote_agent_server_name' ]  
    [ , [ @use_interactive_resolver= ] 'use_interactive_resolver' ]  
    [ , [ @merge_job_name= ] 'merge_job_name' ]  
    [ , [ @hostname = ] 'hostname'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, sem padrão. A publicação já deve existir.  
  
 [  **@subscriber =**] **'***assinante***'**  
 É o nome do Assinante. *assinante* é **sysname**, com um padrão NULL.  
  
 [  **@subscriber_db=**] **'***subscriber_db***'**  
 É o nome do banco de dados de assinatura. *subscriber_db*é **sysname**, com um padrão NULL.  
  
 [  **@subscription_type=**] **'***subscription_type***'**  
 É o tipo de assinatura. *subscription_type*é **nvarchar (15)**, com um padrão PUSH. Se **push**, uma assinatura push será adicionada e o Merge Agent é adicionado ao distribuidor. Se **pull**, uma assinatura pull será adicionada sem adicionar um agente de mesclagem no distribuidor.  
  
> [!NOTE]  
>  Assinaturas anônimas não precisam usar esse procedimento armazenado.  
  
 [  **@subscriber_type=**] **'***subscriber_type***'**  
 É o tipo de assinante. *subscriber_type*é **nvarchar (15)**, e pode ser um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**local** (padrão)|Assinante conhecido somente pelo Publicador.|  
|**Global**|Assinante conhecido por todos os servidores.|  
  
 No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores, assinaturas locais são referidas como assinaturas de cliente e assinaturas globais são referidas como assinaturas de servidor.  
  
 [  **@subscription_priority=**] *subscription_priority*  
 É um número que indica a prioridade da assinatura. *subscription_priority*é **real**, com um padrão NULL. Para assinaturas locais e anônimas, a prioridade é 0.0. Para assinaturas globais, a prioridade deve ser menos que 100.0.  
  
 [  **@sync_type=**] **'***sync_type***'**  
 É o tipo de sincronização da assinatura. *sync_type*é **nvarchar (15)**, com um padrão de **automática**. Pode ser **automático** ou **nenhum**. Se **automáticas**, o esquema e os dados iniciais para tabelas publicadas são transferidos para o assinante primeiro. Se **nenhum**, presume-se o assinante já tem o esquema e os dados iniciais para tabelas publicadas. Tabelas de sistema e dados sempre são transferidos.  
  
> [!NOTE]  
>  É recomendável não especificar um valor de **nenhum**.  
  
 [  **@frequency_type=**] *frequency_type*  
 É um valor que indica quando o Agente de Mesclagem será executado. *frequency_type* é **int**, e pode ser um dos valores a seguir.  
  
|Value|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**4**|Diariamente|  
|**8**|Semanalmente|  
|**10**|Mensalmente|  
|**20**|Mensalmente, relativo ao intervalo de frequência|  
|**40**|Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent inicia|  
|NULL (padrão)||  
  
 [  **@frequency_interval=**] *frequency_interval*  
 O dia ou dias em que o Agente de Mesclagem é executado. *frequency_interval* é **int**, e pode ser um dos valores a seguir.  
  
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
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 É a ocorrência da mesclagem agendada do intervalo de frequência em cada mês. *frequency_relative_interval* é **int**, e pode ser um destes valores.  
  
|Value|Descrição|  
|-----------|-----------------|  
|**1**|First|  
|**2**|Segundo|  
|**4**|Terceiro|  
|**8**|Quarto|  
|**16**|Last|  
|NULL (padrão)||  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 É o fator de recorrência usado por *frequency_type*. *frequency_recurrence_factor*é **int**, com um padrão NULL.  
  
 [  **@frequency_subday=**] *frequency_subday*  
 É a unidade para *frequency_subday_interval*. *frequency_subday* é **int**, e pode ser um dos valores a seguir.  
  
|Value|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**4**|Minuto|  
|**8**|Hora|  
|NULL (padrão)||  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 É a frequência para *frequency_subday* devem ocorrer entre cada mesclagem. *frequency_subday_interval* é **int**, com um padrão NULL.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 É a hora do dia do primeiro agendamento do Agente de Mesclagem, formatada como HHMMSS. *active_start_time_of_day* é **int**, com um padrão NULL.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 É a hora do dia do último agendamento do Agente de Mesclagem, formatada como HHMMSS. *active_end_time_of_day* é **int**, com um padrão NULL.  
  
 [  **@active_start_date=**] *active_start_date*  
 É a data do primeiro agendamento do Agente de Mesclagem, formatada como AAAAMMDD. *active_start_date* é **int**, com um padrão NULL.  
  
 [  **@active_end_date=**] *active_end_date*  
 É a data do último agendamento do Agente de Mesclagem, formatada como AAAAMMDD. *active_end_date* é **int**, com um padrão NULL.  
  
 [  **@optional_command_line=**] **'***optional_command_line***'**  
 É o prompt de comando opcional a ser executado. *optional_command_line*é **nvarchar (4000)**, com um padrão NULL. Esse parâmetro é usado para adicionar um comando que captura a saída e a salva em um arquivo ou para especificar um arquivo de configuração ou atributo.  
  
 [  **@description=**] **'***descrição***'**  
 É uma descrição breve dessa assinatura de mesclagem. *Descrição*é **nvarchar (255)**, com um padrão NULL. Esse valor é exibido pelo Replication Monitor no **nome amigável** coluna, que pode ser usada para classificar as assinaturas para uma publicação monitorada.  
  
 [  **@enabled_for_syncmgr=**] **'***enabled_for_syncmgr***'**  
 Especifica se a assinatura pode ser sincronizada pelo Gerenciador de Sincronização do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. *enabled_for_syncmgr* é **nvarchar (5)**, com um padrão de FALSE. Se **false**, a assinatura não está registrada com o Gerenciador de sincronização. Se **true**, a assinatura será registrada com o Gerenciador de sincronização e será sincronizada sem iniciar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 [  **@offloadagent=** ] *remote_agent_activation*  
 Especifica que o agente pode ser ativado remotamente. *remote_agent_activation* é **bit** com um padrão de **0**.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e só é mantido para compatibilidade com versões anteriores.  
  
 [  **@offloadserver=** ] **'***remote_agent_server_name***'**  
 Especifica o nome da rede de servidor a ser usado para ativação de agente remota. *remote_agent_server_name*é **sysname**, com um padrão NULL.  
  
 [  **@use_interactive_resolver=** ] **'***use_interactive_resolver***'**  
 Permite resolver conflitos interativamente para todos os artigos que permitem resolução interativa. *use_interactive_resolver* é **nvarchar (5)**, com um padrão de FALSE.  
  
 [  **@merge_job_name=** ] **'***merge_job_name***'**  
 O *@merge_job_name* parâmetro é preterido e não pode ser definido. *merge_job_name* é **sysname**, com um padrão NULL.  
  
 [ **@hostname**=] **'***hostname***'**  
 Substitui o valor retornado por [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) quando essa função é usada na cláusula WHERE de um filtro com parâmetros. *nome do host* é **sysname**, com um padrão NULL.  
  
> [!IMPORTANT]  
>  Por motivos de desempenho, recomendamos que não sejam aplicadas funções a nomes de colunas em cláusulas de filtro de linha com parâmetros, como `LEFT([MyColumn]) = SUSER_SNAME()`. Se você usar [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) em uma cláusula de filtro e substituir o valor HOST_NAME, talvez seja necessário converter tipos de dados usando [converter](../../t-sql/functions/cast-and-convert-transact-sql.md). Para obter mais informações sobre práticas recomendadas para esse caso, consulte a seção "Substituindo o valor de HOST_NAME()" no tópico [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_addmergesubscription** é usado em replicação de mesclagem.  
  
 Quando **sp_addmergesubscription** é executado por um membro do **sysadmin** função de servidor fixa para criar uma assinatura push, o trabalho do Merge Agent é implicitamente criado e é executado sob o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent conta de serviço. É recomendável que você execute [sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md) e especifique as credenciais de uma conta do Windows diferente, específica de agente para **@job_login** e **@job_password**. Para obter mais informações, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergesubscription-_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_addmergesubscription**.  
  
## <a name="see-also"></a>Consulte também  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Criar uma assinatura pull](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Resolução interativa de conflitos](../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)   
 [Assinar Publicações](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_changemergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
