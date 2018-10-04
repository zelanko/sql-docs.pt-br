---
title: sp_addmergepullsubscription_agent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepullsubscription_agent
- sp_addmergepullsubscription_agent_TSQL
helpviewer_keywords:
- sp_addmergepullsubscription_agent
ms.assetid: a2f4b086-078d-49b5-8971-8a1e3f6a6feb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: da16887ff7debf09e69fc72cf464f5838cf6ddc7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47749734"
---
# <a name="spaddmergepullsubscriptionagent-transact-sql"></a>sp_addmergepullsubscription_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona um novo trabalho de agente para agendar a sincronização de uma assinatura pull com uma publicação de mesclagem. Esse procedimento armazenado é executado no assinante, no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addmergepullsubscription_agent [ [ @name = ] 'name' ]   
        , [ @publisher = ] 'publisher'   
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication =] 'publication'   
    [ , [ @publisher_security_mod e= ] publisher_security_mode ]   
    [ , [ @publisher_login = ] 'publisher_login' ]   
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @publisher_encrypted_password = ] publisher_encrypted_password ]   
    [ , [ @subscriber = ] 'subscriber' ]   
    [ , [ @subscriber_db = ] 'subscriber_db' ]   
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]   
    [ , [ @subscriber_login = ] 'subscriber_login' ]   
    [ , [ @subscriber_password= ] 'subscriber_password' ]   
    [ , [ @distributor = ] 'distributor' ]   
    [ , [ @distributor_security_mode = ] distributor_security_mode ]   
    [ , [ @distributor_login = ] 'distributor_login' ]   
    [ , [ @distributor_password = ] 'distributor_password' ]   
    [ , [ @encrypted_password = ] encrypted_password ]   
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
    [ , [ @merge_jobid = ] merge_jobid ]   
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]   
    [ , [ @ftp_address = ] 'ftp_address' ]   
    [ , [ @ftp_port = ] ftp_port ]   
    [ , [ @ftp_login = ] 'ftp_login' ]   
    [ , [ @ftp_password = ] 'ftp_password' ]    
    [ , [ @alt_snapshot_folder = ] 'alternate_snapshot_folder' ]   
    [ , [ @working_directory = ] 'working_directory' ]   
    [ , [ @use_ftp = ] 'use_ftp' ]   
    [ , [ @reserved = ] 'reserved' ]   
    [ , [ @use_interactive_resolver = ] 'use_interactive_resolver' ]   
    [ , [ @offloadagent = ] 'remote_agent_activation' ]   
    [ , [ @offloadserver = ] 'remote_agent_server_name']   
    [ , [ @job_name = ] 'job_name' ]   
    [ , [ @dynamic_snapshot_location = ] 'dynamic_snapshot_location' ]  
    [ , [ @use_web_sync = ] use_web_sync ]  
        [ , [ @internet_url = ] 'internet_url' ]  
    [ , [ @internet_login = ] 'internet_login' ]  
        [ , [ @internet_password = ] 'internet_password' ]  
    [ , [ @internet_security_mode = ] internet_security_mode ]  
        [ , [ @internet_timeout = ] internet_timeout ]  
    [ , [ @hostname = ] 'hostname' ]  
        [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@name =** ] **'***nome***'**  
 É o nome do agente. *nome da* está **sysname**, com um padrão NULL.  
  
 [  **@publisher =** ] **'***publisher***'**  
 É o nome do servidor do Publicador. *Publisher* está **sysname**, sem padrão.  
  
 [  **@publisher_db =** ] **'***publisher_db***'**  
 É o nome do banco de dados Publicador. *publisher_db* está **sysname**, sem padrão.  
  
 [  **@publication =** ] **'***publicação***'**  
 É o nome da publicação. *publicação* está **sysname**, sem padrão.  
  
 [  **@publisher_security_mode =** ] *publisher_security_mode*  
 É o modo de segurança a ser usado ao se conectar a um Publicador na sincronização. *publisher_security_mode* está **int**, com um padrão de 1. Se **0**, especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. Se **1**, especifica a autenticação do Windows.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@publisher_login =** ] **'***publisher_login***'**  
 É o logon a ser usado na conexão com um Publicador durante a sincronização. *publisher_login* está **sysname**, com um padrão NULL.  
  
 [  **@publisher_password =** ] **'***publisher_password***'**  
 É a senha usada ao conectar-se ao Publicador. *publisher_password* está **sysname**, com um padrão NULL.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
 [  **@publisher_encrypted_password =** ]*publisher_encrypted_password*  
 Definindo *publisher_encrypted_password* não é mais suportada. Tentativa de definir isso **bits** parâmetro **1** resultará em erro.  
  
 [  **@subscriber =** ] **'***assinante***'**  
 É o nome do Assinante. *assinante* está **sysname**, com um padrão NULL.  
  
 [  **@subscriber_db =** ] **'***subscriber_db***'**  
 É o nome do banco de dados de assinatura. *subscriber_db* está **sysname**, com um padrão NULL.  
  
 [  **@subscriber_security_mode =** ] *subscriber_security_mode*  
 É o modo de segurança a ser usado ao conectar-se a um Assinante na sincronização. *subscriber_security_mode* está **int**, com um padrão de 1. Se **0**, especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. Se **1**, especifica a autenticação do Windows.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. O Agente de Mesclagem sempre conecta ao Assinante local usando a Autenticação do Windows. Se um valor for especificado para esse parâmetro, uma mensagem de aviso será retornada, mas o valor será ignorado.  
  
 [  **@subscriber_login =** ] **'***subscriber_login***'**  
 É o logon do Assinante a ser usado ao conectar-se a um Assinante na sincronização. *subscriber_login* será necessária se *subscriber_security_mode* é definido como **0**. *subscriber_login* está **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. Se um valor for especificado para esse parâmetro, uma mensagem de aviso será retornada, mas o valor será ignorado.  
  
 [  **@subscriber_password =** ] **'***subscriber_password***'**  
 É a senha do Assinante para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *subscriber_password* será necessária se *subscriber_security_mode* é definido como **0**. *subscriber_password* está **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. Se um valor for especificado para esse parâmetro, uma mensagem de aviso será retornada, mas o valor será ignorado.  
  
 [  **@distributor =** ] **'***distribuidor***'**  
 É o nome do distribuidor. *distribuidor* está **sysname**, com um padrão de *publisher*; ou seja, o publicador é também o distribuidor.  
  
 [  **@distributor_security_mode =** ] *distributor_security_mode*  
 É o modo de segurança a ser usado ao conectar-se a um Distribuidor na sincronização. *distributor_security_mode* está **int**, com um padrão de 0. **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. **1** Especifica a autenticação do Windows.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@distributor_login =** ] **'***distributor_login***'**  
 É o logon do Distribuidor a ser usado ao conectar-se a um Distribuidor na sincronização. *distributor_login* será necessária se *distributor_security_mode* é definido como **0**. *distributor_login* está **sysname**, com um padrão NULL.  
  
 [  **@distributor_password =** ] **'***distributor_password***'**  
 É a senha do Distribuidor. *distributor_password* será necessária se *distributor_security_mode* é definido como **0**. *distributor_password* está **sysname**, com um padrão NULL.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
 [  **@encrypted_password =** ] *encrypted_password*  
 Definindo *encrypted_password* não é mais suportada. Tentativa de definir isso **bits** parâmetro **1** resultará em erro.  
  
 [  **@frequency_type =** ] *frequency_type*  
 É a frequência do agendamento do Agente de Mesclagem. *frequency_type* está **int**, e pode ser um dos valores a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Sob Demanda|  
|**4**|Diariamente|  
|**8**|Semanalmente|  
|**16**|Mensalmente|  
|**32**|Relativo ao mês|  
|**64**|Iniciar automaticamente|  
|**128**|Recorrente|  
|NULL (padrão)||  
  
> [!NOTE]  
>  Especificando um valor de **64** faz com que o Merge Agent para executar em modo contínuo. Isso corresponde à configuração de **-contínua** parâmetro para o agente. Para obter mais informações, consulte [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md).  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 O dia ou dias em que o Agente de Mesclagem é executado. *frequency_interval* está **int**, e pode ser um destes valores.  
  
|Valor|Description|  
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
  
 [  **@frequency_relative_interval =** ] *frequency_relative_interval*  
 É a data do Agente de Mesclagem. Esse parâmetro é usado quando *frequency_type* é definido como **32** (mensal relativo). *frequency_relative_interval* está **int**, e pode ser um destes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**1**|First|  
|**2**|Segundo|  
|**4**|Terceiro|  
|**8**|Quarto|  
|**16**|Last|  
|NULL (padrão)||  
  
 [  **@frequency_recurrence_factor =** ] *frequency_recurrence_factor*  
 É o fator de recorrência usado pelo *frequency_type*. *frequency_recurrence_factor* está **int**, com um padrão NULL.  
  
 [  **@frequency_subday =** ] *frequency_subday*  
 É a frequência de reagendamento durante o período definido. *frequency_subday* está **int**, e pode ser um destes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**4**|Minuto|  
|**8**|Hora|  
|NULL (padrão)||  
  
 [  **@frequency_subday_interval =** ] *frequency_subday_interval*  
 É o intervalo de *frequency_subday*. *frequency_subday_interval* está **int**, com um padrão NULL.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 É a hora do dia do primeiro agendamento do Agente de Mesclagem, formatada como HHMMSS. *active_start_time_of_day* está **int**, com um padrão NULL.  
  
 [  **@active_end_time_of_day =** ] *active_end_time_of_day*  
 É a hora do dia do último agendamento do Agente de Mesclagem, formatada como HHMMSS. *active_end_time_of_day* está **int**, com um padrão NULL.  
  
 [  **@active_start_date =** ] *active_start_date*  
 É a data do primeiro agendamento do Agente de Mesclagem, formatada como AAAAMMDD. *active_start_date* está **int**, com um padrão NULL.  
  
 [  **@active_end_date =** ] *active_end_date*  
 É a data do último agendamento do Agente de Mesclagem, formatada como AAAAMMDD. *active_end_date* está **int**, com um padrão NULL.  
  
 [  **@optional_command_line =** ] **'***optional_command_line***'**  
 É um prompt de comando opcional fornecido ao Agente de Mesclagem. *optional_command_line* está **nvarchar (255)**, com um padrão de ' '. Pode ser usado para fornecer parâmetros adicionais ao Agente de Mesclagem, como no exemplo seguinte que aumenta o tempo limite de consulta padrão para `600` segundos:  
  
```  
@optional_command_line = N'-QueryTimeOut 600'  
```  
  
 [  **@merge_jobid =** ] *merge_jobid*  
 É o parâmetro de saída da ID do trabalho. *merge_jobid* está **binário (16)**, com um padrão NULL.  
  
 [  **@enabled_for_syncmgr =** ] **'***enabled_for_syncmgr***'**  
 Especifica se a assinatura pode ou não ser sincronizada pelo Gerenciador de Sincronização do Windows. *enabled_for_syncmgr* está **nvarchar (5)**, com um padrão de FALSE. Se **falsos**, a assinatura não está registrada com o Gerenciador de sincronização. Se **verdadeira**, a assinatura é registrada com o Gerenciador de sincronização e será sincronizada sem iniciar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 [  **@ftp_address =** ] **'***ftp_address***'**  
 Somente para compatibilidade com versões anteriores.  
  
 [  **@ftp_port =** ] *ftp_port*  
 Somente para compatibilidade com versões anteriores.  
  
 [  **@ftp_login =** ] **'***ftp_login***'**  
 Somente para compatibilidade com versões anteriores.  
  
 [  **@ftp_password =** ] **'***ftp_password***'**  
 Somente para compatibilidade com versões anteriores.  
  
 [  **@alt_snapshot_folder =** ] **'***alternate_snapshot_folder***'**  
 Especifica o local do qual retirar os arquivos de instantâneo. *alternate_snapshot_folder* está **nvarchar (255)**, com um padrão NULL. Se for NULL, os arquivos de instantâneo serão retirados do local padrão especificado pelo Publicador.  
  
 [  **@working_directory =** ] **'***working_directory***'**  
 É o nome do diretório de trabalho usado para armazenar dados e arquivos de esquema temporariamente para a publicação quando o FTP for usado para transferir arquivos de instantâneo. *working_directory* está **nvarchar (255)**, com um padrão NULL.  
  
 [  **@use_ftp =** ] **'***use_ftp***'**  
 Especifica o uso do FTP, em vez do protocolo típico para recuperar instantâneos. *use_ftp* está **nvarchar (5)**, com um padrão de FALSE.  
  
 [  **@reserved =** ] **'***reservado***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@use_interactive_resolver =** ] **'***use_interactive_resolver***'** ]  
 Usa o resolvedor interativo para resolver conflitos para todos os artigos que permitem resolução interativa. *use_interactive_resolver* está **nvarchar (5)**, com um padrão de FALSE.  
  
 [  **@offloadagent =** ] **'***remote_agent_activation***'**  
 > [!NOTE]  
>  A ativação do agente remoto foi preterida e não tem mais suporte. Esse parâmetro tem suporte somente para manter a compatibilidade com versões anteriores de scripts. Definindo *remote_agent_activation* com um valor diferente de **falso** irá gerar um erro.  
  
 [  **@offloadserver =** ] **'***remote_agent_server_name***'**  
 > [!NOTE]  
>  A ativação do agente remoto foi preterida e não tem mais suporte. Esse parâmetro tem suporte somente para manter a compatibilidade com versões anteriores de scripts. Definindo *remote_agent_server_name* como qualquer valor não NULL gerará um erro.  
  
 [  **@job_name =** ] **'***job_name***'** ]  
 É o nome de um trabalho de agente existente. *job_name* está **sysname**, com um valor padrão de NULL. Esse parâmetro só é especificado quando a assinatura será sincronizada usando um trabalho existente em vez de um trabalho recém-criado (o padrão). Se você não for um membro do **sysadmin** função de servidor fixa, você deve especificar *job_login* e *job_password* quando você especifica *job_name*.  
  
 [  **@dynamic_snapshot_location =** ] **'***dynamic_snapshot_location***'** ]  
 O caminho para a pasta onde os arquivos de instantâneo serão lidos se um instantâneo de dados filtrados deve ser usada. *dynamic_snapshot_location* está **nvarchar (260)**, com um padrão NULL. Para obter mais informações, consulte [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 [  **@use_web_sync =** ] *use_web_sync*  
 Indica que a sincronização da Web está habilitada. *use_web_sync* está **bit**, com um padrão de 0. **1** Especifica que a assinatura pull pode ser sincronizada pela internet usando HTTP.  
  
 [  **@internet_url =** ] **'***internet_url***'**  
 É o local do Replication Listener (REPLISAPI.DLL) para sincronização da Web. *internet_url* está **nvarchar (260)**, com um padrão NULL. *internet_url* é uma URL totalmente qualificada, no formato `http://server.domain.com/directory/replisapi.dll`. Se o servidor for configurado para ouvir em uma porta diferente da porta 80, o número da porta também deverá ser fornecido no formato `http://server.domain.com:portnumber/directory/replisapi.dll`, onde `portnumber` representa a porta.  
  
 [  **@internet_login =** ] **'***internet_login***'**  
 É o logon que o Agente de Mesclagem usa ao se conectar ao servidor da Web que está hospedando a sincronização da Web usando Autenticação Básica HTTP. *internet_login* está **sysname**, com um padrão NULL.  
  
 [  **@internet_password =** ] **'***internet_password***'**  
 É a senha que o Agente de Mesclagem usa ao se conectar ao servidor da Web que está hospedando a sincronização da Web usando Autenticação Básica HTTP. *internet_password* está **nvarchar(524)**, com um valor padrão de NULL.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 [  **@internet_security_mode =** ] *internet_security_mode*  
 É o método de autenticação usado pelo Agente de Mesclagem ao se conectar ao servidor da Web durante a sincronização da Web, usando HTTPS. *internet_security_mode* está **int** e pode ser um destes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**0**|Autenticação Básica é usada.|  
|**1** (padrão)|Autenticação Integrada do Windows é usada.|  
  
> [!NOTE]  
>  Recomendamos o uso da Autenticação Básica com sincronização da Web. Para usar sincronização da Web, você deve fazer uma conexão SSL ao servidor Web. Para obter mais informações, consulte [Configurar sincronização da Web](../../relational-databases/replication/configure-web-synchronization.md).  
  
 [  **@internet_timeout =** ] *internet_timeout*  
 É o período de tempo, em segundos, antes que uma solicitação de sincronização da Web expire. *internet_timeout* está **int**, com um padrão de **300** segundos.  
  
 [  **@hostname =** ] **'***nome do host***'**  
 Substitui o valor HOST_NAME() quando essa função é usada na cláusula WHERE de um filtro com parâmetros. *nome do host* está **sysname**, com um padrão NULL.  
  
 [  **@job_login =** ] **'***job_login***'**  
 É o logon da conta do Windows na qual o agente é executado. *job_login* está **nvarchar(257)**, sem padrão. Essa conta do Windows é sempre usada para conexões do agente com o Assinante e para conexões com o Distribuidor e o Publicador ao usar a Autenticação Integrada do Windows.  
  
 [  **@job_password =** ] **'***job_password***'**  
 É a senha da conta do Windows na qual o agente é executado. *job_password* está **sysname**, sem padrão.  
  
> [!IMPORTANT]  
>  Não armazene informações de autenticação em arquivos de script. Para melhor segurança, nomes de logon e senhas devem ser fornecidos em tempo de execução.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addmergepullsubscription_agent** é usado em replicação de mesclagem e usa funcionalidade semelhante a [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md).  
  
 Para obter um exemplo de como especificar as configurações de segurança corretamente ao executar **sp_addmergepullsubscription_agent**, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_1_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_addmergepullsubscription_agent**.  
  
## <a name="see-also"></a>Consulte também  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
