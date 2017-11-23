---
title: sp_addpullsubscription_agent (Transact-SQL) | Microsoft Docs
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
- sp_addpullsubscription_agent
- sp_addpullsubscription_agent_TSQL
helpviewer_keywords: sp_addpullsubscription_agent
ms.assetid: b9c2eaed-6d2d-4b78-ae9b-73633133180b
caps.latest.revision: "44"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9e13ce0bc7be6b2e21a30f13a3cf7cc299d00295
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spaddpullsubscriptionagent-transact-sql"></a>sp_addpullsubscription_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona um novo trabalho agendado de agente usado para sincronizar uma assinatura pull com uma publicação transacional. Esse procedimento armazenado é executado no assinante no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addpullsubscription_agent [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db' ]  
        , [ @publication = ] 'publication'  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]  
    [ , [ @subscriber_login = ] 'subscriber_login' ]  
    [ , [ @subscriber_password = ] 'subscriber_password' ]  
    [ , [ @distributor = ] 'distributor' ]  
    [ , [ @distribution_db = ] 'distribution_db' ]  
    [ , [ @distributor_security_mode = ] distributor_security_mode ]  
    [ , [ @distributor_login = ] 'distributor_login' ]  
    [ , [ @distributor_password = ] 'distributor_password' ]  
    [ , [ @optional_command_line = ] 'optional_command_line' ]  
    [ , [ @frequency_type = ] frequency_type ]  
    [ , [ @frequency_interval = ] frequency_interval ]  
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]  
    [ , [ @frequency_subda y= ] frequency_subday ]  
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]  
    [ , [ @active_start_date = ] active_start_date ]  
    [ , [ @active_end_date = ] active_end_date ]  
    [ , [ @distribution_jobid = ] distribution_jobid OUTPUT ]  
    [ , [ @encrypted_distributor_password = ] encrypted_distributor_password ]  
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]  
    [ , [ @ftp_address = ] 'ftp_address' ]  
    [ , [ @ftp_port = ] ftp_port ]  
    [ , [ @ftp_login = ] 'ftp_login' ]  
    [ , [ @ftp_password = ] 'ftp_password' ]  
    [ , [ @alt_snapshot_folder = ] 'alternate_snapshot_folder' ]  
    [ , [ @working_directory = ] 'working_directory' ]  
    [ , [ @use_ftp = ] 'use_ftp' ]  
    [ , [ @publication_type = ] publication_type ]  
    [ , [ @dts_package_name = ] 'dts_package_name' ]  
    [ , [ @dts_package_password = ] 'dts_package_password' ]  
    [ , [ @dts_package_location = ] 'dts_package_location' ]  
    [ , [ @reserved = ] 'reserved' ]  
    [ , [ @offloadagent = ] 'remote_agent_activation' ]  
    [ , [ @offloadserver = ] 'remote_agent_server_name']  
    [ , [ @job_name = ] 'job_name' ]  
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=**] **'***publicador***'**  
 É o nome do Publicador. *publicador* é **sysname**, sem padrão.  
  
 [  **@publisher_db=**] **'***publisher_db'*  
 É o nome do banco de dados Publicador. *publisher_db* é **sysname**, com um valor padrão de NULL. *publisher_db* é ignorado por Publicadores Oracle.  
  
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, sem padrão.  
  
 [  **@subscriber=**] **'***assinante***'**  
 É o nome do Assinante. *assinante* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts.  
  
 [  **@subscriber_db=**] **'***subscriber_db***'**  
 É o nome do banco de dados de assinatura. *subscriber_db* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts.  
  
 [  **@subscriber_security_mode=**] *subscriber_security_mode*  
 É o modo de segurança a ser usado ao conectar-se a um Assinante na sincronização. *subscriber_security_mode* é **int,** com um padrão NULL. **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. **1** Especifica autenticação do Windows.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. O Agente de Distribuição sempre conecta ao Assinante local usando a Autenticação do Windows. Se um valor diferente de NULL ou **1** é especificado para esse parâmetro, uma mensagem de aviso será retornada.  
  
 [  **@subscriber_login =**] **'***subscriber_login***'**  
 É o logon do assinante a ser usado ao se conectar a um assinante na sincronização. *subscriber_login* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. Se for especificado um valor para esse parâmetro, uma mensagem de aviso é exibida, mas o valor será ignorado.  
  
 [  **@subscriber_password=**] **'***subscriber_password***'**  
 É a senha de Assinante. *subscriber_password* é necessária se *subscriber_security_mode* é definido como **0**. *subscriber_password* é **sysname**, com um padrão NULL. Se uma senha de assinante for usada, será criptografada automaticamente.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. Se for especificado um valor para esse parâmetro, uma mensagem de aviso é exibida, mas o valor será ignorado.  
  
 [  **@distributor=**] **'***distribuidor***'**  
 É o nome do distribuidor. *distribuidor* é **sysname**, com um padrão do valor especificado por *publicador*.  
  
 [  **@distribution_db=**] **'***distribution_db***'**  
 É o nome do banco de dados de distribuição. *distribution_db* é **sysname**, com um valor padrão de NULL.  
  
 [  **@distributor_security_mode=**] *distributor_security_mode*  
 É o modo de segurança a ser usado ao conectar-se a um Distribuidor na sincronização. *distributor_security_mode* é **int**, com um padrão de **1**. **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. **1** Especifica autenticação do Windows.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@distributor_login=**] **'***distributor_login***'**  
 É o logon do Distribuidor a ser usado ao conectar-se a um Distribuidor na sincronização. *distributor_login* é necessária se *distributor_security_mode* é definido como **0**. *distributor_login* é **sysname**, com um padrão NULL.  
  
 [  **@distributor_password =**] **'***distributor_password***'**  
 É a senha do Distribuidor. *distributor_password* é necessária se *distributor_security_mode* é definido como **0**. *distributor_password* é **sysname**, com um padrão NULL.  
  
> [!IMPORTANT]  
>  Não use uma senha em branco. Use uma senha forte. Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
 [  **@optional_command_line=**] **'***optional_command_line***'**  
 É um prompt de comando opcional fornecido ao Agente de Distribuição. Por exemplo, **- DefinitionFile** C:\Distdef.txt ou **- CommitBatchSize** 10. *optional_command_line* é **nvarchar (4000)**, com um padrão de cadeia de caracteres vazia.  
  
 [  **@frequency_type=**] *frequency_type*  
 É a frequência de agendamento do Agente de Distribuição. *frequency_type* é **int**, e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2** (padrão)|Sob Demanda|  
|**4**|Diariamente|  
|**8**|Semanalmente|  
|**16**|Mensalmente|  
|**32**|Relativo ao mês|  
|**64**|Iniciar automaticamente|  
|**128**|Recorrente|  
  
> [!NOTE]  
>  Especificando um valor de **64** faz com que o agente de distribuição executado no modo contínuo. Isso corresponde à configuração de **-contínua** parâmetro para o agente. Para obter mais informações, consulte [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md).  
  
 [  **@frequency_interval=**] *frequency_interval*  
 É o valor a ser aplicado à frequência definida *frequency_type*. *frequency_interval* é **int**, com um padrão de 1.  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 É a data do Distribution Agent. Esse parâmetro é usado quando *frequency_type* é definido como **32** (mensal relativo). *frequency_relative_interval* é **int**, e pode ser um dos valores a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|**1** (padrão)|First|  
|**2**|Segundo|  
|**4**|Terceiro|  
|**8**|Quarto|  
|**16**|Last|  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 É o fator de recorrência usado por *frequency_type*. *frequency_recurrence_factor* é **int**, com um padrão de **1**.  
  
 [  **@frequency_subday=**] *frequency_subday*  
 É a frequência de reagendamento durante o período definido. *frequency_subday* é **int**, e pode ser um dos valores a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|**1** (padrão)|Uma vez|  
|**2**|Segundo|  
|**4**|Minuto|  
|**8**|Hora|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 É o intervalo de *frequency_subday*. *frequency_subday_interval* é **int**, com um padrão de **1**.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 É a hora do dia do primeiro agendamento do Agente de Distribuição, formatada como HHMMSS. *active_start_time_of_day* é **int**, com um padrão de **0**.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 É a hora do dia do último agendamento do Agente de Distribuição, formatada como HHMMSS. *active_end_time_of_day* é **int**, com um padrão de **0**.  
  
 [  **@active_start_date=**] *active_start_date*  
 É a data do primeiro agendamento do Agente de Distribuição, formatada como AAAAMMDD. *active_start_date* é **int**, com um padrão de **0**.  
  
 [  **@active_end_date=**] *active_end_date*  
 É a data do último agendamento do Agente de Distribuição, formatada como AAAAMMDD. *active_end_date* é **int**, com um padrão de **0**.  
  
 [  **@distribution_jobid =**] *distribution_jobid***saída**  
 É a ID do Agente de Distribuição para este trabalho. *distribution_jobid* é **binário (16)**, com um padrão de NULL e é um parâmetro de saída.  
  
 [  **@encrypted_distributor_password=**] *encrypted_distributor_password*  
 Configuração *encrypted_distributor_password* não é mais suportada. Tentativa de definir isso **bit** parâmetro **1** resultará em erro.  
  
 [  **@enabled_for_syncmgr=**] **'***enabled_for_syncmgr***'**  
 Se a assinatura pode ser sincronizada por meio de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Gerenciador de sincronização. *enabled_for_syncmgr* é **nvarchar (5)**, com um padrão de FALSE. Se **false**, a assinatura não está registrada com o Gerenciador de sincronização. Se **true**, a assinatura será registrada com o Gerenciador de sincronização e será sincronizada sem iniciar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 [  **@ftp_address=**] **'***ftp_address***'**  
 Somente para compatibilidade com versões anteriores.  
  
 [  **@ftp_port=**] *ftp_port*  
 Somente para compatibilidade com versões anteriores.  
  
 [  **@ftp_login=**] **'***ftp_login***'**  
 Somente para compatibilidade com versões anteriores.  
  
 [  **@ftp_password=**] **'***ftp_password***'**  
 Somente para compatibilidade com versões anteriores.  
  
 [  **@alt_snapshot_folder=** ] **'***alternate_snapshot_folder'*  
 Especifica o local da pasta alternativa para o instantâneo. *alternate_snapshot_folder* é **nvarchar (255)**, com um padrão NULL.  
  
 [  **@working_directory** =] **'***working_director***'**  
 É o nome do diretório de trabalho usado para armazenar dados e arquivos de esquema para a publicação. *working_directory* é **nvarchar (255)**, com um padrão NULL. O nome deve ser especificado no formato UNC.  
  
 [  **@use_ftp** =] **'***use_ftp***'**  
 Especifica o uso do FTP em vez do protocolo regular para recuperar instantâneos. *use_ftp* é **nvarchar (5)**, com um padrão de FALSE.  
  
 [  **@publication_type** =] *publication_type*  
 Especifica o tipo de replicação da publicação. *publication_type* é um **tinyint** com um padrão de **0**. Se **0**, publicação é um tipo de transação. Se **1**, publicação é um tipo de instantâneo. Se **2**, publicação é um tipo de mesclagem.  
  
 [  **@dts_package_name** =] **'***dts_package_name***'**  
 Especifica o nome do pacote DTS. *dts_package_name* é um **sysname** com um padrão NULL. Por exemplo, para especificar um nome de pacote `DTSPub_Package`, o parâmetro seria `@dts_package_name = N'DTSPub_Package'`.  
  
 [  **@dts_package_password** =] **'***dts_package_password***'**  
 Especifica a senha no pacote, se houver um. *dts_package_password* é **sysname** com um padrão NULL, que significa que uma senha não está no pacote.  
  
> [!NOTE]  
>  Você deve especificar uma senha se *dts_package_name* for especificado.  
  
 [  **@dts_package_location** =] **'***dts_package_location***'**  
 Especifica o local do pacote. *dts_package_location* é um **nvarchar (12)**, com um padrão de **assinante**. O local do pacote pode ser **distribuidor** ou **assinante**.  
  
 [  **@reserved** =] **'***reservado***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@offloadagent** =] '*remote_agent_activation*'  
 > [!NOTE]  
>  A ativação do agente remoto foi preterida e não tem mais suporte. Esse parâmetro tem suporte somente para manter a compatibilidade com versões anteriores de scripts. Configuração *remote_agent_activation* para um valor diferente de **false** gerará um erro.  
  
 [  **@offloadserver** =] '*remote_agent_server_name*'  
 > [!NOTE]  
>  A ativação do agente remoto foi preterida e não tem mais suporte. Esse parâmetro tem suporte somente para manter a compatibilidade com versões anteriores de scripts. Configuração *remote_agent_server_name* como qualquer valor não NULL gerará um erro.  
  
 [  **@job_name** =] '*job_name*'  
 É o nome de um trabalho de agente existente. *job_name* é **sysname**, com um valor padrão de NULL. Esse parâmetro só é especificado quando a assinatura será sincronizada usando um trabalho existente em vez de um trabalho recém-criado (o padrão). Se você não for um membro do **sysadmin** função de servidor fixa, você deve especificar *job_login* e *job_password* quando você especifica *job_name*.  
  
 [  **@job_login** =] **'***job_login***'**  
 É o logon da conta do Windows na qual o agente é executado. *job_login* é **nvarchar (257)**, sem padrão. Essa conta do Windows sempre é usada para conexões doe agente com o Assinante.  
  
 [  **@job_password** =] **'***job_password***'**  
 É a senha da conta do Windows na qual o agente é executado. *job_password* é **sysname**, sem padrão.  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addpullsubscription_agent** é usado em replicação de instantâneo e replicação transacional.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addpullsubscription-a_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_addpullsubscription_agent**.  
  
## <a name="see-also"></a>Consulte também  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Assinar Publicações](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addpullsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_change_subscription_properties &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_droppullsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [sp_helppullsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
