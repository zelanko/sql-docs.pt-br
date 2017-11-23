---
title: sp_addpushsubscription_agent (Transact-SQL) | Microsoft Docs
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
- sp_addpushsubscription_agent_TSQL
- sp_addpushsubscription_agent
helpviewer_keywords: sp_addpushsubscription_agent
ms.assetid: 1fdd2052-50d8-4318-8aa7-fc635d5cad18
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3ea57cd5bbcb264b38efc4fecf63153f56ba7e92
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spaddpushsubscriptionagent-transact-sql"></a>sp_addpushsubscription_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona um novo trabalho agendado de agente usado para sincronizar uma assinatura push com uma publicação transacional. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
> [!IMPORTANT]  
>  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@publication =**] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, sem padrão.  
  
 [  **@subscriber =**] **'***assinante***'**  
 É o nome do Assinante. *assinante* é **sysname**, com um padrão NULL.  
  
 [  **@subscriber_db =**] **'***subscriber_db***'**  
 É o nome do banco de dados de assinatura. *subscriber_db* é **sysname**, com um padrão NULL. Para um assinante não SQL Server, especifique um valor de **(destino padrão)** para *subscriber_db*.  
  
 [  **@subscriber_security_mode =**] *subscriber_security_mode*  
 É o modo de segurança a ser usado ao conectar-se a um Assinante na sincronização. *subscriber_security_mode* é **int**, com um padrão de 1. **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. **1** Especifica autenticação do Windows.  
  
> [!IMPORTANT]  
>  Para assinaturas de atualização enfileiradas, use Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conexões com Assinantes, e especifique uma conta diferente para conexão com cada assinante. Para todas as outras assinaturas, use a Autenticação do Windows.  
  
 [  **@subscriber_login =**] **'***subscriber_login***'**  
 É o logon do Assinante a ser usado ao conectar-se a um Assinante na sincronização. *subscriber_login* é **sysname**, com um padrão NULL.  
  
 [  **@subscriber_password =**] **'***subscriber_password***'**  
 É a senha de Assinante. *subscriber_password* é necessária se *subscriber_security_mode* é definido como **0**. *subscriber_password* é **sysname**, com um padrão NULL. Se uma senha de assinante for usada, será criptografada automaticamente.  
  
> [!IMPORTANT]  
>  Não use uma senha em branco. Use uma senha forte. Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
 [  **@job_login =** ] **'***job_login***'**  
 É o logon da conta do Windows na qual o agente é executado. *job_login* é **nvarchar (257)**, com um valor padrão de NULL. Essa conta do Windows é sempre usada para conexões do agente com o Distribuidor e para conexões com o Assinante ao usar a autenticação integrada do Windows.  
  
 [  **@job_password =** ] **'***job_password***'**  
 É a senha da conta do Windows na qual o agente é executado. *job_password* é **sysname**, sem padrão.  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
 [  **@job_name =** ] **'***job_name***'**  
 É o nome de um trabalho de agente existente. *job_name* é **sysname**, com um valor padrão de NULL. Esse parâmetro só é especificado quando a assinatura será sincronizada usando um trabalho existente em vez de um trabalho recém-criado (o padrão). Se você não for um membro do **sysadmin** função de servidor fixa, você deve especificar *job_login* e *job_password* quando você especifica *job_name*.  
  
 [  **@frequency_type =** ] *frequency_type*  
 É a frequência de agendamento do Agente de Distribuição. *frequency_type* é **int**, e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Sob Demanda|  
|**4**|Diariamente|  
|**8**|Semanalmente|  
|**16**|Mensalmente|  
|**32**|Relativo ao mês|  
|**64** (padrão)|Iniciar automaticamente|  
|**128**|Recorrente|  
  
> [!NOTE]  
>  Especificando um valor de **64** faz com que o agente de distribuição executado no modo contínuo. Isso corresponde à configuração de **-contínua** parâmetro para o agente. Para obter mais informações, consulte [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md).  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 É o valor a ser aplicado à frequência definida *frequency_type*. *frequency_interval* é **int**, com um padrão de 1.  
  
 [  **@frequency_relative_interval =** ] *frequency_relative_interval*  
 É a data do Distribution Agent. Esse parâmetro é usado quando *frequency_type* é definido como **32** (mensal relativo). *frequency_relative_interval* é **int**, e pode ser um dos valores a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|**1** (padrão)|First|  
|**2**|Segundo|  
|**4**|Terceiro|  
|**8**|Quarto|  
|**16**|Last|  
  
 [  **@frequency_recurrence_factor =** ] *frequency_recurrence_factor*  
 É o fator de recorrência usado por *frequency_type*. *frequency_recurrence_factor* é **int**, com um padrão de 0.  
  
 [  **@frequency_subday =** ] *frequency_subday*  
 É a frequência de reagendamento durante o período definido. *frequency_subday* é **int**, e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**4** (padrão)|Minuto|  
|**8**|Hora|  
  
 [  **@frequency_subday_interval =** ] *frequency_subday_interval*  
 É o intervalo de *frequency_subday*. *frequency_subday_interval* é **int**, com um padrão de 5.  
  
 [  **@active_start_time_of_day =** ] *active_start_time_of_day*  
 É a hora do dia do primeiro agendamento do Agente de Distribuição, formatada como HHMMSS. *active_start_time_of_day* é **int**, com um padrão de 0.  
  
 [  **@active_end_time_of_day =** ] *active_end_time_of_day*  
 É a hora do dia do último agendamento do Agente de Distribuição, formatada como HHMMSS. *active_end_time_of_day* é **int**, com um padrão de 235959.  
  
 [  **@active_start_date =** ] *active_start_date*  
 É a data do primeiro agendamento do Agente de Distribuição, formatada como AAAAMMDD. *active_start_date* é **int**, com um padrão de 0.  
  
 [  **@active_end_date =** ] *active_end_date*  
 É a data do último agendamento do Agente de Distribuição, formatada como AAAAMMDD. *active_end_date* é **int**, com um padrão de 99991231.  
  
 [  **@dts_package_name =** ] **'***dts_package_name***'**  
 Especifica o nome do pacote DTS (Data Transformation Services). *dts_package_name* é um **sysname** com um padrão NULL. Por exemplo, para especificar um nome de pacote de `DTSPub_Package`, o parâmetro seria `@dts_package_name = N'DTSPub_Package'`.  
  
 [  **@dts_package_password =** ] **'***dts_package_password***'**  
 Especifica a senha necessária para executar o pacote. *dts_package_password* é **sysname** com um padrão NULL.  
  
> [!NOTE]  
>  Você deve especificar uma senha se *dts_package_name* for especificado.  
  
 [  **@dts_package_location =** ] **'***dts_package_location***'**  
 Especifica o local do pacote. *dts_package_location* é um **nvarchar (12)**, com um padrão de DISTRIBUIDOR. O local do pacote pode ser **distribuidor** ou **assinante**.  
  
 [  **@enabled_for_syncmgr =** ] **'***enabled_for_syncmgr***'**  
 Se a assinatura pode ser sincronizada por meio de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Gerenciador de sincronização. *enabled_for_syncmgr* é **nvarchar (5)**, com um padrão de FALSE. Se **false**, a assinatura não está registrada com o Gerenciador de sincronização. Se **true**, a assinatura será registrada com o Gerenciador de sincronização e será sincronizada sem iniciar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 [  **@distribution_job_name =** ] **'***distribution_job_name***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@publisher =** ] **'***publicador***'**  
 É o nome do Publicador. *publicador* é **sysname**, com um valor padrão de NULL.  
  
 [  **@subscriber_provider=** ] **'***subscriber_provider***'**  
 É o PROGID (identificador programático) exclusivo com o qual o provedor OLE DB para a fonte de dados não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é registrado. *subscriber_provider* é **sysname**, com o valor padrão de NULL. *subscriber_provider* deve ser exclusivo para o provedor OLE DB instalado no distribuidor. *subscriber_provider* só tem suporte para não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes.  
  
 [  **@subscriber_datasrc=** ] **'***subscriber_datasrc***'**  
 É o nome da fonte de dados conforme entendido pelo provedor OLE DB. *subscriber_datasrc* é **nvarchar (4000)**, com um valor padrão de NULL. *subscriber_datasrc* é passado como a propriedade DBPROP_INIT_DATASOURCE para inicializar o provedor OLE DB. *subscriber_datasrc* só tem suporte para não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes.  
  
 [  **@subscriber_location=** ] **'***subscriber_location***'**  
 É o local do banco de dados conforme entendido pelo provedor OLE DB. *subscriber_location* é **nvarchar (4000)**, com um valor padrão de NULL. *subscriber_location* é passado como a propriedade DBPROP_INIT_LOCATION para inicializar o provedor OLE DB. *subscriber_location* só tem suporte para não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes.  
  
 [  **@subscriber_provider_string=** ] **'***subscriber_provider_string***'**  
 É a cadeia de conexão específica ao provedor OLE DB que identifica a fonte de dados. *subscriber_provider_string* é **nvarchar (4000)**, com um valor padrão de NULL. *subscriber_provider_string* é passado para IDataInitialize ou definido como a propriedade DBPROP_INIT_PROVIDERSTRING para inicializar o provedor OLE DB. *subscriber_provider_string* só tem suporte para não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes.  
  
 [  **@subscriber_catalog=** ] **'***subscriber_catalog***'**  
 É o catálogo a ser usado ao fazer uma conexão com o provedor OLE DB. *subscriber_catalog* é **sysname**, com o valor padrão de NULL. *subscriber_catalog* é passado como a propriedade DBPROP_INIT_CATALOG para inicializar o provedor OLE DB. *subscriber_catalog* só tem suporte para não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addpushsubscription_agent** é usado em replicação de instantâneo e replicação transacional.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../relational-databases/replication/codesnippet/tsql/sp-addpushsubscription-a_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_addpushsubscription_agent**.  
  
## <a name="see-also"></a>Consulte também  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Criar uma assinatura para um assinante não SQL Server](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Assinar Publicações](../../relational-databases/replication/subscribe-to-publications.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_addsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_changesubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md)   
 [sp_dropsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
