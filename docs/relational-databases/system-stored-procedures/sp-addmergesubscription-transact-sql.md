---
description: sp_addmergesubscription (Transact-SQL)
title: sp_addmergesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergesubscription_TSQL
- sp_addmergesubscription
helpviewer_keywords:
- sp_addmergesubscription
ms.assetid: a191d817-0132-49ff-93ca-76f13e609b38
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 197715e613e35e71068723fe90f2643e2373817e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489571"
---
# <a name="sp_addmergesubscription-transact-sql"></a>sp_addmergesubscription (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Cria uma assinatura push ou pull. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publication = ] 'publication'` É o nome da publicação. a *publicação* é **sysname**, sem padrão. A publicação já deve existir.  
  
`[ @subscriber = ] 'subscriber'` É o nome do Assinante. o *assinante* é **sysname**, com um padrão de NULL.  
  
`[ @subscriber_db = ] 'subscriber_db'` É o nome do banco de dados de assinatura. *subscriber_db*é **sysname**, com um padrão de NULL.  
  
`[ @subscription_type = ] 'subscription_type'` É o tipo de assinatura. *subscription_type*é **nvarchar (15)**, com um padrão de push. Se for **Push**, uma assinatura push será adicionada e o agente de mesclagem será adicionado ao distribuidor. Se efetuar **pull**, uma assinatura pull será adicionada sem adicionar um agente de mesclagem no distribuidor.  
  
> [!NOTE]  
>  Assinaturas anônimas não precisam usar esse procedimento armazenado.  
  
`[ @subscriber_type = ] 'subscriber_type'` É o tipo de assinante. *subscriber_type*é **nvarchar (15)** e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**local** (padrão)|Assinante conhecido somente pelo Publicador.|  
|**geral**|Assinante conhecido por todos os servidores.|  
  
 No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores, assinaturas locais são referidas como assinaturas de cliente e assinaturas globais são referidas como assinaturas de servidor.  
  
`[ @subscription_priority = ] subscription_priority` É um número que indica a prioridade da assinatura. *subscription_priority*é **real**, com um padrão de NULL. Para assinaturas locais e anônimas, a prioridade é 0.0. Para assinaturas globais, a prioridade deve ser menos que 100.0.  
  
`[ @sync_type = ] 'sync_type'` É o tipo de sincronização de assinatura. *sync_type*é **nvarchar (15)**, com um padrão de **automático**. Pode ser **automático** ou **nenhum**. Se **automático**, o esquema e os dados iniciais para tabelas publicadas serão transferidos para o assinante primeiro. Se não **houver nenhum**, supõe-se que o Assinante já tem o esquema e os dados iniciais para tabelas publicadas. Tabelas de sistema e dados sempre são transferidos.  
  
> [!NOTE]  
>  É recomendável não especificar um valor de **nenhum**.  
  
`[ @frequency_type = ] frequency_type` É um valor que indica quando o Agente de Mesclagem será executado. *frequency_type* é **int**e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**4**|Diariamente|  
|**8**|Semanalmente|  
|**10**|Mensal|  
|**20**|Mensalmente, relativo ao intervalo de frequência|  
|**40**|Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent inicia|  
|NULL (padrão)||  
  
`[ @frequency_interval = ] frequency_interval` O dia ou os dias em que o Agente de Mesclagem é executado. *frequency_interval* é **int**e pode ser um dos valores a seguir.  
  
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
  
`[ @frequency_relative_interval = ] frequency_relative_interval` É a ocorrência de mesclagem agendada do intervalo de frequência em cada mês. *frequency_relative_interval* é **int**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Primeiro|  
|**2**|Segundo|  
|**4**|Terceiro|  
|**8**|Quarto|  
|**16**|Último|  
|NULL (padrão)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` É o fator de recorrência usado pelo *frequency_type*. *frequency_recurrence_factor*é **int**, com um padrão de NULL.  
  
`[ @frequency_subday = ] frequency_subday` É a unidade para *frequency_subday_interval*. *frequency_subday* é **int**e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**4**|Minuto|  
|**8**|Hora|  
|NULL (padrão)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` É a frequência de *frequency_subday* ocorrer entre cada mesclagem. *frequency_subday_interval* é **int**, com um padrão de NULL.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` É a hora do dia em que o Agente de Mesclagem é agendado pela primeira vez, formatado como HHMMSS. *active_start_time_of_day* é **int**, com um padrão de NULL.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` É a hora do dia em que a Agente de Mesclagem para de ser agendada, formatada como HHMMSS. *active_end_time_of_day* é **int**, com um padrão de NULL.  
  
`[ @active_start_date = ] active_start_date` É a data em que o Agente de Mesclagem é agendado pela primeira vez, formatado como AAAAMMDD. *active_start_date* é **int**, com um padrão de NULL.  
  
`[ @active_end_date = ] active_end_date` É a data em que a Agente de Mesclagem para de ser agendada, formatada como AAAAMMDD. *active_end_date* é **int**, com um padrão de NULL.  
  
`[ @optional_command_line = ] 'optional_command_line'` É o prompt de comando opcional a ser executado. *optional_command_line*é **nvarchar (4000)**, com um padrão de NULL. Esse parâmetro é usado para adicionar um comando que captura a saída e a salva em um arquivo ou para especificar um arquivo de configuração ou atributo.  
  
`[ @description = ] 'description'` É uma breve descrição dessa assinatura de mesclagem. a *Descrição*é **nvarchar (255)**, com um padrão de NULL. Esse valor é exibido pelo Replication Monitor na coluna **nome amigável** , que pode ser usado para classificar as assinaturas de uma publicação monitorada.  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'` Especifica se a assinatura pode ser sincronizada por meio do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Gerenciador de sincronização do Windows. *enabled_for_syncmgr* é **nvarchar (5)**, com um padrão de false. Se for **false**, a assinatura não será registrada com o Gerenciador de sincronização. Se for **true**, a assinatura será registrada com o Gerenciador de sincronização e poderá ser sincronizada sem iniciar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
`[ @offloadagent = ] remote_agent_activation` Especifica que o agente pode ser ativado remotamente. *remote_agent_activation* é **bit** com um padrão de **0**.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e só é mantido para compatibilidade com versões anteriores.  
  
`[ @offloadserver = ] 'remote_agent_server_name'` Especifica o nome de rede do servidor a ser usado para ativação de agente remoto. *remote_agent_server_name*é **sysname**, com um padrão de NULL.  
  
`[ @use_interactive_resolver = ] 'use_interactive_resolver'` Permite que conflitos sejam resolvidos interativamente para todos os artigos que permitem a resolução interativa. *use_interactive_resolver* é **nvarchar (5)**, com um padrão de false.  
  
`[ @merge_job_name = ] 'merge_job_name'`O parâmetro * \@ merge_job_name* foi preterido e não pode ser definido. *merge_job_name* é **sysname**, com um padrão de NULL.  
  
`[ @hostname = ] 'hostname'` Substitui o valor retornado por [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) quando essa função é usada na cláusula WHERE de um filtro com parâmetros. O *nome do host* é **sysname**, com um padrão de NULL.  
  
> [!IMPORTANT]  
>  Por motivos de desempenho, recomendamos que não sejam aplicadas funções a nomes de colunas em cláusulas de filtro de linha com parâmetros, como `LEFT([MyColumn]) = SUSER_SNAME()`. Se você usar [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) em uma cláusula de filtro e substituir o valor de HOST_NAME, poderá ser necessário converter os tipos de dados usando [Convert](../../t-sql/functions/cast-and-convert-transact-sql.md). Para obter mais informações sobre práticas recomendadas para esse caso, consulte a seção "Substituindo o valor de HOST_NAME()" no tópico [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addmergesubscription** é usado na replicação de mesclagem.  
  
 Quando **sp_addmergesubscription** é executado por um membro da função de servidor fixa **sysadmin** para criar uma assinatura push, o trabalho de agente de mesclagem é criado implicitamente e é executado na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de serviço do Agent. Recomendamos que você execute [sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md) e especifique as credenciais de uma conta diferente do Windows específica do agente para ** \@ job_login** e ** \@ job_password**. Para obter mais informações, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergesubscription-_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_addmergesubscription**.  
  
## <a name="see-also"></a>Consulte Também  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Resolução interativa de conflitos](../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [&#41;&#40;Transact-SQL de sp_changemergesubscription ](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropmergesubscription ](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpmergesubscription ](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
