---
description: sp_addmergepushsubscription_agent (Transact-SQL)
title: sp_addmergepushsubscription_agent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepushsubscription_agent_TSQL
- sp_addmergepushsubscription_agent
helpviewer_keywords:
- sp_addmergepushsubscription_agent
ms.assetid: 808a1925-be46-4999-8d69-b3a83010ec81
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c1b441a47237d09cce422996f592076c879572c4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489583"
---
# <a name="sp_addmergepushsubscription_agent-transact-sql"></a>sp_addmergepushsubscription_agent (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Adiciona um novo trabalho de agente para agendar sincronização de uma assinatura push para uma publicação de mesclagem. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
> [!IMPORTANT]  
>  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addmergepushsubscription_agent [ @publication =] 'publication'   
    [ , [ @subscriber = ] 'subscriber' ]   
    [ , [ @subscriber_db = ] 'subscriber_db' ]   
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]   
    [ , [ @subscriber_login = ] 'subscriber_login' ]   
    [ , [ @subscriber_password = ] 'subscriber_password' ]   
    [ , [ @publisher_security_mode = ] publisher_security_mode ]   
    [ , [ @publisher_login = ] 'publisher_login' ]   
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
    [ , [ @job_name = ] 'job_name' ]   
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
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @subscriber = ] 'subscriber'` É o nome do Assinante. o *assinante* é **sysname**, com um padrão de NULL.  
  
`[ @subscriber_db = ] 'subscriber_db'` É o nome do banco de dados de assinatura. *subscriber_db* é **sysname**, com um padrão de NULL.  
  
`[ @subscriber_security_mode = ] subscriber_security_mode` É o modo de segurança a ser usado ao se conectar a um assinante ao sincronizar. *subscriber_security_mode* é **int**, com um padrão de 1. Se **0**, especifica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. Se **1**, especifica a autenticação do Windows.  
  
`[ @subscriber_login = ] 'subscriber_login'` É o logon do assinante a ser usado ao se conectar a um assinante ao sincronizar. *subscriber_login* será necessário se *subscriber_security_mode* for definido como **0**. *subscriber_login* é **sysname**, com um padrão de NULL.  
  
`[ @subscriber_password = ] 'subscriber_password'` É a senha do assinante para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. *subscriber_password* será necessário se *subscriber_security_mode* for definido como **0**. *subscriber_password* é **sysname**, com um padrão de NULL. Se uma senha de assinante for usada, será criptografada automaticamente.  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
`[ @publisher_security_mode = ] publisher_security_mode` É o modo de segurança a ser usado ao se conectar a um Publicador durante a sincronização. *publisher_security_mode* é **int**, com um padrão de 1. Se **0**, especifica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. Se **1**, especifica a autenticação do Windows.  
  
`[ @publisher_login = ] 'publisher_login'` É o logon a ser usado ao se conectar a um Publicador durante a sincronização. *publisher_login* é **sysname**, com um padrão de NULL.  
  
`[ @publisher_password = ] 'publisher_password'` É a senha usada ao conectar-se ao Publicador. *publisher_password* é **sysname**, com um padrão de NULL.  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
`[ @job_login = ] 'job_login'` É o logon da conta do Windows na qual o agente é executado. *job_login* é **nvarchar (257)**, com um valor padrão de NULL. Essa conta do Windows é sempre usada para conexões do agente com o Distribuidor e para conexões com o Assinante e o Publicador ao usar a autenticação integrada do Windows.  
  
`[ @job_password = ] 'job_password'` É a senha para a conta do Windows na qual o agente é executado. *job_password* é **sysname**, sem padrão.  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
`[ @job_name = ] 'job_name'` É o nome de um trabalho de agente existente. *job_name* é **sysname**, com um valor padrão de NULL. Esse parâmetro só é especificado quando a assinatura é sincronizada usando um trabalho existente em vez de um trabalho recém-criado (o padrão). Se você não for membro da função de servidor fixa **sysadmin** , deverá especificar *job_login* e *job_password* ao especificar *job_name*.  
  
`[ @frequency_type = ] frequency_type` É a frequência com a qual agendar a Agente de Mesclagem. *frequency_type* é **int**e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Sob demanda|  
|**4**|Diariamente|  
|**8**|Semanalmente|  
|**16**|Mensal|  
|**32**|Relativo ao mês|  
|**64**|Iniciar automaticamente|  
|**128**|Recorrente|  
|NULL (padrão)||  
  
> [!NOTE]  
>  A especificação de um valor de **64** faz com que a agente de mesclagem seja executada no modo contínuo. Isso corresponde à definição do parâmetro **-Continuous** para o agente. Para obter mais informações, consulte [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md).  
  
`[ @frequency_interval = ] frequency_interval` Os dias em que o Agente de Mesclagem é executado. *frequency_interval* é **int**e pode ser um dos valores a seguir.  
  
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
  
`[ @frequency_relative_interval = ] frequency_relative_interval` É a data da Agente de Mesclagem. Esse parâmetro é usado quando *frequency_type* é definido como **32** (relativo mensal). *frequency_relative_interval* é **int**e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Primeiro|  
|**2**|Segundo|  
|**4**|Terceiro|  
|**8**|Quarto|  
|**16**|Último|  
|NULL (padrão)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` É o fator de recorrência usado pelo *frequency_type*. *frequency_recurrence_factor* é **int**, com um padrão de NULL.  
  
`[ @frequency_subday = ] frequency_subday` É a frequência de reagendar durante o período definido. *frequency_subday* é **int**e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**4**|Minuto|  
|**8**|Hora|  
|NULL (padrão)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` É o intervalo para *frequency_subday*. *frequency_subday_interval* é **int**, com um padrão de NULL.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` É a hora do dia em que o Agente de Mesclagem é agendado pela primeira vez, formatado como HHMMSS. *active_start_time_of_day* é **int**, com um padrão de NULL.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` É a hora do dia em que a Agente de Mesclagem para de ser agendada, formatada como HHMMSS. *active_end_time_of_day* é **int**, com um padrão de NULL.  
  
`[ @active_start_date = ] active_start_date` É a data em que o Agente de Mesclagem é agendado pela primeira vez, formatado como AAAAMMDD. *active_start_date* é **int**, com um padrão de NULL.  
  
`[ @active_end_date = ] active_end_date` É a data em que a Agente de Mesclagem para de ser agendada, formatada como AAAAMMDD. *active_end_date* é **int**, com um padrão de NULL.  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'` Especifica se a assinatura pode ser sincronizada por meio do Gerenciador de sincronização do Windows. *enabled_for_syncmgr* é **nvarchar (5)**, com um padrão de false. Se for **false**, a assinatura não será registrada com o Gerenciador de sincronização. Se for **true**, a assinatura será registrada com o Gerenciador de sincronização e poderá ser sincronizada sem iniciar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addmergepushsubscription_agent** é usado na replicação de mesclagem e usa uma funcionalidade semelhante à [sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md).  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepushsubscript_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_addmergepushsubscription_agent**.  
  
## <a name="see-also"></a>Consulte Também  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [&#41;&#40;Transact-SQL de sp_addmergesubscription ](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changemergesubscription ](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropmergesubscription ](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpmergesubscription ](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
