---
title: sp_addmergepullsubscription_agent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepullsubscription_agent
- sp_addmergepullsubscription_agent_TSQL
helpviewer_keywords:
- sp_addmergepullsubscription_agent
ms.assetid: a2f4b086-078d-49b5-8971-8a1e3f6a6feb
author: stevestein
ms.author: sstein
ms.openlocfilehash: 07cc514d615c86a90dcf37fbd4748c3ab1776f06
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528970"
---
# <a name="sp_addmergepullsubscription_agent-transact-sql"></a>sp_addmergepullsubscription_agent (Transact-SQL)

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Adiciona um novo trabalho de agente para agendar a sincronização de uma assinatura pull com uma publicação de mesclagem. Este procedimento armazenado é executado no Assinante no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @name = ] 'name'`É o nome do agente. *nome* é **sysname,** com um padrão de NULL.  
  
`[ @publisher = ] 'publisher'`É o nome do servidor Publisher. *editor* é **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'`É o nome do banco de dados do Publisher. *publisher_db* **é sysname,** sem padrão.  
  
`[ @publication = ] 'publication'`É o nome da publicação. *publicação* é **sysname**, sem padrão.  
  
`[ @publisher_security_mode = ] publisher_security_mode`É o modo de segurança a ser usado ao conectar-se a um Publisher ao sincronizar. *publisher_security_mode* é **int**, com um padrão de 1. Se **0,** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificar autenticação. Se **1,** especificar a autenticação do Windows.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'`É o login a ser usado ao se conectar a um Publisher ao sincronizar. *publisher_login* **é sysname,** com um padrão de NULL.  
  
`[ @publisher_password = ] 'publisher_password'`É a senha usada ao se conectar ao Editor. *publisher_password* **é sysname,** com um padrão de NULL.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] Quando possível, solicite que os usuários insiram as credenciais de segurança em runtime. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
`[ @publisher_encrypted_password = ]publisher_encrypted_password`A *configuração publisher_encrypted_password* não é mais suportada. Tentar definir este parâmetro **de bit** **si** 000 um erro resultará em um erro.  
  
`[ @subscriber = ] 'subscriber'`É o nome do Assinante. *assinante* é **sysname**, com um padrão de NULL.  
  
`[ @subscriber_db = ] 'subscriber_db'`É o nome do banco de dados de assinatura. *subscriber_db* **é sysname,** com um padrão de NULL.  
  
`[ @subscriber_security_mode = ] subscriber_security_mode`É o modo de segurança a ser usado ao se conectar a um Assinante ao sincronizar. *subscriber_security_mode* é **int**, com um padrão de 1. Se **0,** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificar autenticação. Se **1,** especificar a autenticação do Windows.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. O Agente de Mesclagem sempre conecta ao Assinante local usando a Autenticação do Windows. Se um valor for especificado para esse parâmetro, uma mensagem de aviso será retornada, mas o valor será ignorado.  
  
`[ @subscriber_login = ] 'subscriber_login'`É o login do Assinante para usar ao se conectar a um Assinante ao sincronizar. *subscriber_login* é necessário se *subscriber_security_mode* estiver definido como **0**. *subscriber_login* **é sysname,** com um padrão de NULL.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. Se um valor for especificado para esse parâmetro, uma mensagem de aviso será retornada, mas o valor será ignorado.  
  
`[ @subscriber_password = ] 'subscriber_password'`É a senha [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Assinante para Autenticação. *subscriber_password* é necessário se *subscriber_security_mode* estiver definido como **0**. *subscriber_password* **é sysname,** com um padrão de NULL.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. Se um valor for especificado para esse parâmetro, uma mensagem de aviso será retornada, mas o valor será ignorado.  
  
`[ @distributor = ] 'distributor'`É o nome do Distribuidor. *distribuidor* é **sysname,** com um padrão de *editor;* ou seja, o Editor também é o Distribuidor.  
  
`[ @distributor_security_mode = ] distributor_security_mode`É o modo de segurança a ser usado ao se conectar a um Distribuidor ao sincronizar. *distributor_security_mode* é **int**, com um padrão de 0. **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. **1** especifica a autenticação do Windows.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @distributor_login = ] 'distributor_login'`O login do Distribuidor deve ser usado ao se conectar a um Distribuidor ao sincronizar. *distributor_login* é necessário se *distributor_security_mode* estiver definido como **0**. *distributor_login* **é sysname,** com um padrão de NULL.  
  
`[ @distributor_password = ] 'distributor_password'`É a senha do Distribuidor. *distributor_password* é necessário se *distributor_security_mode* estiver definido como **0**. *distributor_password* **é sysname,** com um padrão de NULL.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] Quando possível, solicite que os usuários insiram as credenciais de segurança em runtime. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
`[ @encrypted_password = ] encrypted_password`A *configuração encrypted_password* não é mais suportada. Tentar definir este parâmetro **de bit** **si** 000 um erro resultará em um erro.  
  
`[ @frequency_type = ] frequency_type`É a freqüência com a qual agendar o Agente de Fusão. *frequency_type* é **int**, e pode ser um dos seguintes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Sob demanda|  
|**4**|Diário|  
|**8**|Semanal|  
|**16**|Mensal|  
|**32**|Relativo ao mês|  
|**64**|Iniciar automaticamente|  
|**128**|Recorrente|  
|NULL (padrão)||  
  
> [!NOTE]  
>  Especificar um valor de **64** faz com que o Agente de Mesclagem seja executado no modo contínuo. Isso corresponde à definição do parâmetro **-Contínuo** para o agente. Para obter mais informações, consulte [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md).  
  
`[ @frequency_interval = ] frequency_interval`O dia ou dia que o Agente de Fusão executa. *frequency_interval* é **int**, e pode ser um desses valores.  
  
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
  
`[ @frequency_relative_interval = ] frequency_relative_interval`É a data do Agente de Fusão. Este parâmetro é usado quando *frequency_type* é definido como **32** (relativo mensal). *frequency_relative_interval* é **int**, e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Primeiro|  
|**2**|Segundo|  
|**4**|Terceiro|  
|**8**|Quarto|  
|**16**|Último|  
|NULL (padrão)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`É o fator de recorrência usado por *frequency_type*. *frequency_recurrence_factor* é **int**, com um padrão de NULL.  
  
`[ @frequency_subday = ] frequency_subday`É a frequência de reagendar durante o período definido. *frequency_subday* é **int**, e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**4**|Minuto|  
|**8**|Hora|  
|NULL (padrão)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`É o intervalo para *frequency_subday*. *frequency_subday_interval* é **int**, com um padrão de NULL.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`É a hora do dia em que o Agente de Mesclagem é programado pela primeira vez, formatado como HHMMSS. *active_start_time_of_day* é **int**, com um padrão de NULL.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`É a hora do dia em que o Agente de Mesclagem deixa de ser programado, formatado como HHMMSS. *active_end_time_of_day* é **int**, com um padrão de NULL.  
  
`[ @active_start_date = ] active_start_date`É a data em que o Agente de Mesclagem é agendado pela primeira vez, formatado como YYYYMMDD. *active_start_date* é **int**, com um padrão de NULL.  
  
`[ @active_end_date = ] active_end_date`É a data em que o Agente de Mesclagem deixa de ser agendado, formatado como YYYYMMDD. *active_end_date* é **int**, com um padrão de NULL.  
  
`[ @optional_command_line = ] 'optional_command_line'`É um prompt de comando opcional fornecido ao Agente de Mesclagem. *optional_command_line* é **nvarchar(255)**, com um padrão de ' '. Pode ser usado para fornecer parâmetros adicionais ao Agente de Mesclagem, como no exemplo seguinte que aumenta o tempo limite de consulta padrão para `600` segundos:  
  
```  
@optional_command_line = N'-QueryTimeOut 600'  
```  
  
`[ @merge_jobid = ] merge_jobid`É o parâmetro de saída para o ID de trabalho. *merge_jobid* é **binário(16)**, com um padrão de NULL.  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'`Especifica se a assinatura pode ser sincronizada através do Windows Synchronization Manager. *enabled_for_syncmgr* é **nvarchar(5)**, com um padrão de FALSE. Se **for falsa,** a assinatura não será registrada no Synchronization Manager. Se **for verdade,** a assinatura é registrada no Synchronization [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Manager e pode ser sincronizada sem iniciar .  
  
`[ @ftp_address = ] 'ftp_address'`Apenas para retrocompatibilidade.  
  
`[ @ftp_port = ] ftp_port`Apenas para retrocompatibilidade.  
  
`[ @ftp_login = ] 'ftp_login'`Apenas para retrocompatibilidade.  
  
`[ @ftp_password = ] 'ftp_password'`Apenas para retrocompatibilidade.  
  
`[ @alt_snapshot_folder = ] 'alternate_snapshot_folder'`Especifica o local a partir do qual pegar os arquivos de instantâneo. *alternate_snapshot_folder* é **nvarchar(255)**, com um padrão de NULL. Se for NULL, os arquivos de instantâneo serão retirados do local padrão especificado pelo Publicador.  
  
`[ @working_directory = ] 'working_directory'`É o nome do diretório de trabalho usado para armazenar temporariamente dados e arquivos de esquema para a publicação quando o FTP é usado para transferir arquivos de snapshot. *working_directory* é **nvarchar(255)**, com um padrão de NULL.  
  
`[ @use_ftp = ] 'use_ftp'`Especifica o uso de FTP em vez do protocolo típico para recuperar instantâneos. *use_ftp* é **nvarchar(5)**, com um padrão de FALSE.  
  
`[ @reserved = ] 'reserved'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @use_interactive_resolver = ] 'use_interactive_resolver' ]`Usa solução interativa para resolver conflitos para todos os artigos que permitem resolução interativa. *use_interactive_resolver* é **nvarchar(5)**, com um padrão de FALSE.  
  
`[ @offloadagent = ] 'remote_agent_activation'`
 > [!NOTE]  
>  A ativação do agente remoto foi preterida e não tem mais suporte. Esse parâmetro tem suporte somente para manter a compatibilidade com versões anteriores de scripts. Definir *remote_agent_activation* para um valor diferente de **falso** gerará um erro.  
  
`[ @offloadserver = ] 'remote_agent_server_name'`
 > [!NOTE]  
>  A ativação do agente remoto foi preterida e não tem mais suporte. Esse parâmetro tem suporte somente para manter a compatibilidade com versões anteriores de scripts. A *configuração remote_agent_server_name* para qualquer valor não NULA gerará um erro.  
  
`[ @job_name = ] 'job_name' ]`É o nome de um trabalho de agente existente. *job_name* **é sysname,** com um valor padrão de NULL. Esse parâmetro só é especificado quando a assinatura será sincronizada usando um trabalho existente em vez de um trabalho recém-criado (o padrão). Se você não é um membro da função servidor fixo **sysadmin,** você deve especificar *job_login* e *job_password* quando você *especificar job_name*.  
  
`[ @dynamic_snapshot_location = ] 'dynamic_snapshot_location' ]`O caminho para a pasta onde os arquivos de snapshot serão lidos se um instantâneo de dados filtrado for usado. *dynamic_snapshot_location* é **nvarchar(260)**, com um padrão de NULL. Para obter mais informações, consulte [Filtros de linha com parâmetros](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
`[ @use_web_sync = ] use_web_sync`Indica que a sincronização da Web está ativada. *use_web_sync* é **bit**, com um padrão de 0. **1** especifica que a assinatura pull pode ser sincronizada pela internet usando HTTP.  
  
`[ @internet_url = ] 'internet_url'`É a localização do ouvinte de replicação (REPLISAPI. DLL) para sincronização da Web. *internet_url* é **nvarchar(260)**, com um padrão de NULL. *internet_url* é uma URL totalmente `http://server.domain.com/directory/replisapi.dll`qualificada, no formato . Se o servidor for configurado para ouvir em uma porta diferente da porta 80, o número da porta também deverá ser fornecido no formato `http://server.domain.com:portnumber/directory/replisapi.dll`, onde `portnumber` representa a porta.  
  
`[ @internet_login = ] 'internet_login'`É o login que o Agente de Mesclagem usa ao se conectar ao servidor Web que está hospedando a sincronização da Web usando http basic authentication. *internet_login* **é sysname,** com um padrão de NULL.  
  
`[ @internet_password = ] 'internet_password'`É a senha que o Agente de Mesclagem usa ao se conectar ao servidor Web que está hospedando a sincronização da Web usando http basic authentication. *internet_password* é **nvarchar(524)**, com um valor padrão de NULL.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
`[ @internet_security_mode = ] internet_security_mode`É o método de autenticação usado pelo Agente de Mesclagem ao se conectar ao servidor Web durante a sincronização da Web usando HTTPS. *internet_security_mode* é **int** e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Autenticação Básica é usada.|  
|**1** (padrão)|Autenticação Integrada do Windows é usada.|  
  
> [!NOTE]  
>  Recomendamos o uso da Autenticação Básica com sincronização da Web. Para usar a sincronização da Web, você deve fazer uma conexão TLS com o servidor Web. Para obter mais informações, consulte [Configurar sincronização da Web](../../relational-databases/replication/configure-web-synchronization.md).  
  
`[ @internet_timeout = ] internet_timeout`É o tempo, em segundos, antes de uma solicitação de sincronização da Web expirar. *internet_timeout* é **int,** com um padrão de **300** segundos.  
  
`[ @hostname = ] 'hostname'`Substitui o valor de HOST_NAME() quando esta função é usada na cláusula WHERE de um filtro parametrizado. *hostname* é **sysname**, com um padrão de NULL.  
  
`[ @job_login = ] 'job_login'`É o login da conta do Windows sob a qual o agente é executado. *job_login* é **nvarchar(257)**, sem padrão. Essa conta do Windows é sempre usada para conexões do agente com o Assinante e para conexões com o Distribuidor e o Publicador ao usar a Autenticação Integrada do Windows.  
  
`[ @job_password = ] 'job_password'`É a senha da conta do Windows sob a qual o agente é executado. *job_password* é **sysname,** sem padrão.  
  
> [!IMPORTANT]  
>  Não armazene informações de autenticação em arquivos de script. Para melhor segurança, nomes de logon e senhas devem ser fornecidos em runtime.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addmergepullsubscription_agent** é usado na replicação de mesclagem e usa funcionalidade semelhante à [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md).  
  
 Para obter um exemplo de como especificar corretamente as configurações de segurança ao executar **sp_addmergepullsubscription_agent,** consulte [Criar uma assinatura pull](../../relational-databases/replication/create-a-pull-subscription.md).  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_1_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros da função servidor fixo **sysadmin** ou **db_owner** função de banco de dados fixo podem executar **sp_addmergepullsubscription_agent**.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar uma assinatura pull](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Inscreva-se em Publicações](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription &#40;&#41;transact-SQL de sp_addmergepullsubscription](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;&#41;Transact-SQL da sp_dropmergepullsubscription](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
