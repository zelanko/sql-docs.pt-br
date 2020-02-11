---
title: sp_addpushsubscription_agent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpushsubscription_agent_TSQL
- sp_addpushsubscription_agent
helpviewer_keywords:
- sp_addpushsubscription_agent
ms.assetid: 1fdd2052-50d8-4318-8aa7-fc635d5cad18
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8073d51fb4376acbdc19724422f6ef7543e3c403
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68894038"
---
# <a name="sp_addpushsubscription_agent-transact-sql"></a>sp_addpushsubscription_agent (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Adiciona um novo trabalho agendado de agente usado para sincronizar uma assinatura push com uma publicação transacional. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
> [!IMPORTANT]  
>  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addpushsubscription_agent [ @publication= ] 'publication'  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]  
    [ , [ @subscriber_login = ] 'subscriber_login' ]  
    [ , [ @subscriber_password = ] 'subscriber_password' ]  
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
    [ , [ @dts_package_name = ] 'dts_package_name' ]  
    [ , [ @dts_package_password = ] 'dts_package_password' ]  
    [ , [ @dts_package_location = ] 'dts_package_location' ]  
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]  
    [ , [ @distribution_job_name = ] 'distribution_job_name' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @subscriber_provider = ] 'subscriber_provider' ]   
    [ , [ @subscriber_datasrc = ] 'subscriber_datasrc' ]   
    [ , [ @subscriber_location = ] 'subscriber_location' ]  
    [ , [ @subscriber_provider_string = ] 'subscriber_provider_string' ]   
    [ , [ @subscriber_catalog = ] 'subscriber_catalog' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @subscriber = ] 'subscriber'`É o nome da instância do assinante ou o nome do ouvinte do AG se o banco de dados do assinante for um grupo de disponibilidade. o *assinante* é **sysname**, com um padrão de NULL. 
  
`[ @subscriber_db = ] 'subscriber_db'`É o nome do banco de dados de assinatura. *subscriber_db* é **sysname**, com um padrão de NULL. Para um assinante não SQL Server, especifique um valor de **(destino padrão)** para *subscriber_db*.  
  
`[ @subscriber_security_mode = ] subscriber_security_mode`É o modo de segurança a ser usado ao se conectar a um assinante ao sincronizar. *subscriber_security_mode* é **int**, com um padrão de 1. **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a autenticação. **1** especifica a autenticação do Windows.  
  
> [!IMPORTANT]  
>  Para assinaturas de atualização enfileiradas, use Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conexões com Assinantes, e especifique uma conta diferente para conexão com cada assinante. Para todas as outras assinaturas, use a Autenticação do Windows.  
  
`[ @subscriber_login = ] 'subscriber_login'`É o logon do assinante a ser usado ao se conectar a um assinante ao sincronizar. *subscriber_login* é **sysname**, com um padrão de NULL.  
  
`[ @subscriber_password = ] 'subscriber_password'`É a senha do Assinante. *subscriber_password* será necessário se *subscriber_security_mode* for definido como **0**. *subscriber_password* é **sysname**, com um padrão de NULL. Se uma senha de assinante for usada, será criptografada automaticamente.  
  
> [!IMPORTANT]  
>  Não use uma senha em branco. Use uma senha forte. Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
`[ @job_login = ] 'job_login'`É o logon da conta sob a qual o agente é executado. Em Instância Gerenciada do Banco de Dados SQL do Azure use uma conta de SQL Server. *job_login* é **nvarchar (257)**, com um valor padrão de NULL. Essa conta do Windows é sempre usada para conexões do agente com o Distribuidor e para conexões com o Assinante ao usar a autenticação integrada do Windows.  
  
`[ @job_password = ] 'job_password'`É a senha para a conta na qual o agente é executado. *job_password* é **sysname**, sem padrão.  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
`[ @job_name = ] 'job_name'`É o nome de um trabalho de agente existente. *job_name* é **sysname**, com um valor padrão de NULL. Esse parâmetro só é especificado quando a assinatura for sincronizada usando um trabalho existente em vez de um trabalho recém-criado (o padrão). Se você não for membro da função de servidor fixa **sysadmin** , deverá especificar *job_login* e *job_password* ao especificar *job_name*.  
  
`[ @frequency_type = ] frequency_type`É a frequência com a qual agendar a Agente de Distribuição. *frequency_type* é **int**e pode ser um dos valores a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Sob demanda|  
|**quatro**|Diário|  
|**8**|Semanalmente|  
|**16**|Mensal|  
|**32**|Relativo ao mês|  
|**64** (padrão)|Iniciar automaticamente|  
|**128**|Recorrente|  
  
> [!NOTE]  
>  A especificação de um valor de **64** faz com que a agente de distribuição seja executada no modo contínuo. Isso corresponde à definição do parâmetro **-Continuous** para o agente. Para obter mais informações, consulte [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md).  
  
`[ @frequency_interval = ] frequency_interval`É o valor a ser aplicado à frequência definida por *frequency_type*. *frequency_interval* é **int**, com um padrão de 1.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`É a data da Agente de Distribuição. Esse parâmetro é usado quando *frequency_type* é definido como **32** (relativo mensal). *frequency_relative_interval* é **int**e pode ser um dos valores a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**1** (padrão)|Primeiro|  
|**2**|Segundo|  
|**quatro**|Terceiro|  
|**8**|Quarto|  
|**16**|Último|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`É o fator de recorrência usado pelo *frequency_type*. *frequency_recurrence_factor* é **int**, com um padrão de 0.  
  
`[ @frequency_subday = ] frequency_subday`É a frequência de reagendar durante o período definido. *frequency_subday* é **int**e pode ser um dos valores a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**4** (padrão)|Minuto|  
|**8**|Hora|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`É o intervalo para *frequency_subday*. *frequency_subday_interval* é **int**, com um padrão de 5.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`É a hora do dia em que o Agente de Distribuição é agendado pela primeira vez, formatado como HHMMSS. *active_start_time_of_day* é **int**, com um padrão de 0.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`É a hora do dia em que a Agente de Distribuição para de ser agendada, formatada como HHMMSS. *active_end_time_of_day* é **int**, com um padrão de 235959.  
  
`[ @active_start_date = ] active_start_date`É a data em que o Agente de Distribuição é agendado pela primeira vez, formatado como AAAAMMDD. *active_start_date* é **int**, com um padrão de 0.  
  
`[ @active_end_date = ] active_end_date`É a data em que a Agente de Distribuição para de ser agendada, formatada como AAAAMMDD. *active_end_date* é **int**, com um padrão de 99991231.  
  
`[ @dts_package_name = ] 'dts_package_name'`Especifica o nome do pacote DTS (Data Transformation Services). *dts_package_name* é um **sysname** com um padrão de NULL. Por exemplo, para especificar um nome de pacote `DTSPub_Package`de, o parâmetro seria `@dts_package_name = N'DTSPub_Package'`.  
  
`[ @dts_package_password = ] 'dts_package_password'`Especifica a senha necessária para executar o pacote. *dts_package_password* é **sysname** com um padrão de NULL.  
  
> [!NOTE]  
>  Você deve especificar uma senha se *dts_package_name* for especificado.  
  
`[ @dts_package_location = ] 'dts_package_location'`Especifica o local do pacote. *dts_package_location* é um **nvarchar (12)**, com um padrão de distribuidor. O local do pacote pode ser **distribuidor** ou **assinante**.  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'`É se a assinatura pode ser sincronizada [!INCLUDE[msCoName](../../includes/msconame-md.md)] por meio do Gerenciador de sincronização. *enabled_for_syncmgr* é **nvarchar (5)**, com um padrão de false. Se for **false**, a assinatura não será registrada com o Gerenciador de sincronização. Se for **true**, a assinatura será registrada com o Gerenciador de sincronização e poderá [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ser sincronizada sem iniciar.  
  
`[ @distribution_job_name = ] 'distribution_job_name'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @publisher = ] 'publisher'`É o nome do Publicador. o *Publicador* é **sysname**, com um valor padrão de NULL.  
  
`[ @subscriber_provider = ] 'subscriber_provider'`É o identificador de programação (PROGID) exclusivo com o qual o provedor de OLE DB para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a fonte de dados não está registrado. *subscriber_provider* é **sysname**, com o valor padrão de NULL. *subscriber_provider* deve ser exclusivo para o provedor de OLE DB instalado no distribuidor. Só há suporte para *subscriber_provider* para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes não.  
  
`[ @subscriber_datasrc = ] 'subscriber_datasrc'`É o nome da fonte de dados como compreendido pelo provedor de OLE DB. *subscriber_datasrc* é **nvarchar (4000)**, com um valor padrão de NULL. *subscriber_datasrc* é passado como a propriedade DBPROP_INIT_DATASOURCE para inicializar o provedor de OLE DB. Só há suporte para *subscriber_datasrc* para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes não.  
  
`[ @subscriber_location = ] 'subscriber_location'`É o local do banco de dados como compreendido pelo provedor de OLE DB. *subscriber_location* é **nvarchar (4000)**, com um valor padrão de NULL. *subscriber_location* é passado como a propriedade DBPROP_INIT_LOCATION para inicializar o provedor de OLE DB. Só há suporte para *subscriber_location* para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes não.  
  
`[ @subscriber_provider_string = ] 'subscriber_provider_string'`É a OLE DB cadeia de conexão específica do provedor que identifica a fonte de dados. *subscriber_provider_string* é **nvarchar (4000)**, com um valor padrão de NULL. *subscriber_provider_string* é passado para IDataInitialize ou definido como a propriedade DBPROP_INIT_PROVIDERSTRING para inicializar o provedor de OLE DB. Só há suporte para *subscriber_provider_string* para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes não.  
  
`[ @subscriber_catalog = ] 'subscriber_catalog'`É o catálogo a ser usado ao estabelecer uma conexão com o provedor de OLE DB. *subscriber_catalog* é **sysname**, com o valor padrão de NULL. *subscriber_catalog* é passado como a propriedade DBPROP_INIT_CATALOG para inicializar o provedor de OLE DB. Só há suporte para *subscriber_catalog* para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes não.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addpushsubscription_agent** é usado na replicação de instantâneo e na replicação transacional.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../relational-databases/replication/codesnippet/tsql/sp-addpushsubscription-a_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_addpushsubscription_agent**.  
  
## <a name="see-also"></a>Consulte Também  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Criar uma assinatura para um assinante não SQL Server](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropsubscription](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
