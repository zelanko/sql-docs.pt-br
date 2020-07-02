---
title: sp_addpublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpublication_TSQL
- sp_addpublication
helpviewer_keywords:
- sp_addpublication
ms.assetid: c7167ed1-2b7e-4824-b82b-65f4667c4407
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: be04cfff11e30baf2212401bd07b9ca74782ca14
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85786219"
---
# <a name="sp_addpublication-transact-sql"></a>sp_addpublication (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Cria uma publicação de instantâneo ou transacional. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addpublication [ @publication = ] 'publication'  
    [ , [ @taskid = ] tasked ]  
    [ , [ @restricted = ] 'restricted' ]  
    [ , [ @sync_method = ] 'sync_method' ]  
    [ , [ @repl_freq = ] 'repl_freq' ]  
    [ , [ @description = ] 'description' ]  
    [ , [ @status = ] 'status' ]  
    [ , [ @independent_agent = ] 'independent_agent' ]  
    [ , [ @immediate_sync = ] 'immediate_sync' ]  
    [ , [ @enabled_for_internet = ] 'enabled_for_internet' ]  
    [ , [ @allow_push = ] 'allow_push'  
    [ , [ @allow_pull = ] 'allow_pull' ]  
    [ , [ @allow_anonymous = ] 'allow_anonymous' ]  
    [ , [ @allow_sync_tran = ] 'allow_sync_tran' ]  
    [ , [ @autogen_sync_procs = ] 'autogen_sync_procs' ]  
    [ , [ @retention = ] retention ]  
    [ , [ @allow_queued_tran= ] 'allow_queued_updating' ]  
    [ , [ @snapshot_in_defaultfolder= ] 'snapshot_in_default_folder' ]  
    [ , [ @alt_snapshot_folder= ] 'alternate_snapshot_folder' ]  
    [ , [ @pre_snapshot_script= ] 'pre_snapshot_script' ]  
    [ , [ @post_snapshot_script= ] 'post_snapshot_script' ]  
    [ , [ @compress_snapshot= ] 'compress_snapshot' ]  
    [ , [ @ftp_address = ] 'ftp_address' ]  
    [ , [ @ftp_port= ] ftp_port ]  
    [ , [ @ftp_subdirectory = ] 'ftp_subdirectory' ]  
    [ , [ @ftp_login = ] 'ftp_login' ]  
    [ , [ @ftp_password = ] 'ftp_password' ]  
    [ , [ @allow_dts = ] 'allow_dts' ]  
    [ , [ @allow_subscription_copy = ] 'allow_subscription_copy' ]  
    [ , [ @conflict_policy = ] 'conflict_policy' ]  
    [ , [ @centralized_conflicts = ] 'centralized_conflicts' ]   
    [ , [ @conflict_retention = ] conflict_retention ]  
    [ , [ @queue_type = ] 'queue_type' ]  
    [ , [ @add_to_active_directory = ] 'add_to_active_directory' ]  
    [ , [ @logreader_job_name = ] 'logreader_agent_name' ]  
    [ , [ @qreader_job_name = ] 'queue_reader_agent_name' ]  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @allow_initialize_from_backup = ] 'allow_initialize_from_backup' ]  
    [ , [ @replicate_ddl = ] replicate_ddl ]  
    [ , [ @enabled_for_p2p = ] 'enabled_for_p2p' ]  
    [ , [ @publish_local_changes_only = ] 'publish_local_changes_only' ]  
    [ , [ @enabled_for_het_sub = ] 'enabled_for_het_sub' ]  
    [ , [ @p2p_conflictdetection = ] 'p2p_conflictdetection' ]  
    [ , [ @p2p_originator_id = ] p2p_originator_id  
    [ , [ @p2p_continue_onconflict = ] 'p2p_continue_onconflict'  
    [ , [ @allow_partition_switch = ] 'allow_partition_switch'  
    [ , [ @replicate_partition_switch = ]'replicate_partition_switch'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ \@publication = ] 'publication'`É o nome da publicação a ser criada. a *publicação* é **sysname**, sem padrão. O nome deve ser exclusivo no banco de dados.  
  
`[ \@taskid = ] taskid`Com suporte somente para compatibilidade com versões anteriores; Use [sp_addpublication_snapshot &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md).  
  
`[ \@restricted = ] 'restricted'`Com suporte somente para compatibilidade com versões anteriores; Use *default_access*.  
  
`[ \@sync_method = ] _'sync_method'`É o modo de sincronização. *sync_method* é **nvarchar (13)** e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**native**|Produz saída de programa de cópia em massa em modo nativo de todas as tabelas. *Não há suporte para Publicadores Oracle*.|  
|**espaço**|Produz saída de programa de cópia em massa em modo de caractere de todas as tabelas. _Para um Publicador Oracle, o_ **caractere** _é válido somente para replicação de instantâneo_.|  
|**simultâneas**|Produz saída de programa de cópia em massa em modo nativo de todas as tabelas, mas não bloqueia as tabelas durante o instantâneo. Com suporte somente para publicações transacionais. *Não há suporte para Publicadores Oracle*.|  
|**concurrent_c**|Produz saída de programa de cópia em massa em modo de caractere de todas as tabelas, mas não bloqueia as tabelas durante o instantâneo. Com suporte somente para publicações transacionais.|  
|**instantâneo do banco de dados**|Produz saída de programa de cópia em massa em modo nativo de todas as tabelas de um instantâneo do banco de dados. Os instantâneos do banco de dados não estão disponíveis em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).|  
|**database snapshot character**|Produz saída de programa de cópia em massa em modo de caractere de todas as tabelas de um instantâneo de banco de dados. Os instantâneos do banco de dados não estão disponíveis em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).|  
|NULL (padrão)|O padrão é **nativo** para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicadores. Para não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores, o padrão é **caractere** quando o valor de *repl_freq* é **instantâneo** e para **concurrent_c** para todos os outros casos.|  
  
`[ \@repl_freq = ] 'repl_freq'`É o tipo de frequência de replicação, *repl_freq* é **nvarchar (10)** e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**contínuo** (padrão)|O Publicador fornece saída de todas as transações com base em log. Para não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores, isso requer que *sync_method* seja definido como **concurrent_c**.|  
|**instantânea**|O Publicador só produz eventos de sincronização agendados. Para não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores, isso requer que *sync_method* seja definido como **caractere**.|  
  
`[ \@description = ] 'description'`É uma descrição opcional para a publicação. a *Descrição* é **nvarchar (255)**, com um padrão de NULL.  
  
`[ \@status = ] 'status'`Especifica se os dados da publicação estão disponíveis. *status* é **nvarchar (8)** e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**active**|O dados da publicação estão imediatamente disponíveis para os Assinantes.|  
|**inativo** (padrão)|Os dados da publicação não estão disponíveis aos Assinantes quando a publicação é criada pela primeira vez (eles podem assinar, mas as assinaturas não são processadas).|  
  
 *Não há suporte para Publicadores Oracle*.  
  
`[ \@independent_agent = ] 'independent_agent'`Especifica se há um Agente de Distribuição autônomo para esta publicação. *independent_agent* é **nvarchar (5)**, com um padrão de false. Se for **true**, haverá um agente de distribuição autônomo para essa publicação. Se **for false**, a publicação usará um agente de distribuição compartilhado, e cada par de banco de dados/assinante do Publicador terá um único agente compartilhado.  
  
`[ \@immediate_sync = ] 'immediate_synchronization'`Especifica se os arquivos de sincronização para a publicação são criados cada vez que o Agente de Instantâneo é executado. *immediate_synchronization* é **nvarchar (5)**, com um padrão de false. Se **for true**, os arquivos de sincronização serão criados ou recriados sempre que o agente de instantâneo for executado. Assinantes podem obter arquivos de sincronização imediatamente se o Snapshot Agent for concluído antes da assinatura ser criada. Novas assinaturas obtêm os arquivos de sincronização mais novos gerados pela execução mais recente do Agente de Instantâneo. *independent_agent* deve ser **true** para que *immediate_synchronization* seja **verdadeiro**. Se **for false**, os arquivos de sincronização serão criados somente se houver novas assinaturas. Você deve chamar [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) para cada assinatura ao adicionar incrementalmente um novo artigo a uma publicação existente. Assinantes não podem receber arquivos de sincronização após a assinatura até que os Snapshot Agents sejam iniciados e concluídos.  
  
`[ \@enabled_for_internet = ] 'enabled_for_internet'`Especifica se a publicação está habilitada para a Internet e determina se o FTP (File Transfer Protocol) pode ser usado para transferir os arquivos de instantâneo para um assinante. *enabled_for_internet* é **nvarchar (5)**, com um padrão de false. Se **for true**, os arquivos de sincronização da publicação serão colocados no diretório C:\Program Files\Microsoft SQL Server\MSSQL\MSSQL.x\Repldata\Ftp O usuário deve criar o diretório Ftp.  
  
`[ \@allow_push = ] 'allow_push'`Especifica se as assinaturas push podem ser criadas para a publicação fornecida. *allow_push* é **nvarchar (5)**, com um padrão true, que permite assinaturas push na publicação.  
  
`[ \@allow_pull = ] 'allow_pull'`Especifica se as assinaturas pull podem ser criadas para a publicação fornecida. *allow_pull* é **nvarchar (5)**, com um padrão de false. Se **for false**, as assinaturas pull não serão permitidas na publicação.  
  
`[ \@allow_anonymous = ] 'allow_anonymous'`Especifica se assinaturas anônimas podem ser criadas para a publicação fornecida. *allow_anonymous* é **nvarchar (5)**, com um padrão de false. Se **for true**, *immediate_synchronization* também deverá ser definido como **true**. Se **for false**, não serão permitidas assinaturas anônimas na publicação.  
  
`[ \@allow_sync_tran = ] 'allow_sync_tran'`Especifica se as assinaturas de atualização imediata são permitidas na publicação. *allow_sync_tran* é **nvarchar (5)**, com um padrão de false. **true** *não tem suporte para Publicadores Oracle*.  
  
`[ \@autogen_sync_procs = ] 'autogen_sync_procs'`Especifica se o procedimento armazenado de sincronização para assinaturas de atualização é gerado no Publicador. *autogen_sync_procs* é **nvarchar (5)** e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**true**|Definido automaticamente quando assinaturas de atualização estão habilitadas.|  
|**false**|Definido automaticamente quando assinaturas de atualização não estão habilitadas ou para Publicadores Oracle.|  
|NULL (padrão)|O padrão é **verdadeiro** quando as assinaturas de atualização estão habilitadas e para **falso** quando as assinaturas de atualização não estão habilitadas.|  
  
> [!NOTE]  
>  O valor fornecido pelo usuário para *autogen_sync_procs*será substituído dependendo dos valores especificados para *allow_queued_tran* e *allow_sync_tran*.  
  
`[ \@retention = ] retention`É o período de retenção em horas para a atividade de assinatura. a *retenção* é **int**, com um padrão de 336 horas. Se uma assinatura não estiver ativa dentro do período de retenção, expirará e será removida. O valor pode ser maior que o período de retenção de máximo do banco de dados de distribuição usado pelo Publicador. Se **0**, as assinaturas conhecidas para a publicação nunca expirarão e serão removidas pelo agente de limpeza de assinatura expirada.  
  
`[ \@allow_queued_tran = ] 'allow_queued_updating'`Habilita ou desabilita o enfileiramento de alterações no Assinante até que elas possam ser aplicadas no Publicador. *allow_queued_updating* é **nvarchar (5)** com um padrão de false. Se **for false**, as alterações no Assinante não serão enfileiradas. **true** *não tem suporte para Publicadores Oracle*.  
  
`[ \@snapshot_in_defaultfolder = ] 'snapshot_in_default_folder'`Especifica se os arquivos de instantâneo são armazenados na pasta padrão. *snapshot_in_default_folder* é **nvarchar (5)** com um padrão de true. Se **for true**, os arquivos de instantâneo poderão ser encontrados na pasta padrão. Se **for false**, os arquivos de instantâneo foram armazenados no local alternativo especificado pelo *alternate_snapshot_folder*. Locais alternativos podem ficar em outro servidor, em uma unidade de rede, ou uma mídia removível (como um CD-ROM ou disco removível). Você também pode salvar os arquivos de instantâneo em um site de FTP para ser recuperado pelo Assinante posteriormente Observe que esse parâmetro pode ser verdadeiro e ainda ter um local no parâmetro ** \@ alt_snapshot_folder** . Essa combinação especifica que os arquivos de instantâneo serão armazenados nos locais padrão e alternativos.  
  
`[ \@alt_snapshot_folder = ] 'alternate_snapshot_folder'`Especifica o local da pasta alternativa para o instantâneo. *alternate_snapshot_folder* é **nvarchar (255)** com um padrão de NULL.  
  
`[ \@pre_snapshot_script = ] 'pre_snapshot_script'`Especifica um ponteiro para um local de arquivo **. SQL** . *pre_snapshot_script* é **nvarchar (255),** com um padrão de NULL. O Agente de Distribuição executará o script pré-instantâneo antes de executar qualquer script de objeto replicado, ao aplicar um instantâneo no Assinante. O script é executado no contexto de segurança usado pelo Distribution Agente na conexão com o banco de dados de assinatura.  
  
`[ \@post_snapshot_script = ] 'post_snapshot_script'`Especifica um ponteiro para um local de arquivo **. SQL** . *post_snapshot_script* é **nvarchar (255)**, com um padrão de NULL. O Agente de Distribuição executará o script pós-instantâneo depois que todos os outros scripts de objeto replicado tentam sido aplicados durante uma sincronização inicial. O script é executado no contexto de segurança usado pelo Distribution Agente na conexão com o banco de dados de assinatura.  
  
`[ \@compress_snapshot = ] 'compress_snapshot'`Especifica que o instantâneo gravado no local de ** \@ alt_snapshot_folder** deve ser compactado no [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato CAB. *compress_snapshot* é **nvarchar (5)**, com um padrão de false. **false** especifica que o instantâneo não será compactado; **true** especifica que o instantâneo será compactado. Arquivos de instantâneo maiores de 2 gigabytes (GB) não podem ser compactados. Arquivos de instantâneo compactados são descompactados no local onde o Distribution Agent é executado; assinaturas pull são geralmente usadas com instantâneos compactados para que os arquivos sejam descompactados no Assinante. O instantâneo na pasta padrão não pode ser compactado.  
  
`[ \@ftp_address = ] 'ftp_address'`É o endereço de rede do serviço FTP para o distribuidor. *ftp_address* é **sysname**, com um padrão de NULL. Especifica onde os arquivos de instantâneo de publicação ficam localizados para serem captados pelo Agente de Distribuição ou por um Assinante. Como essa propriedade é armazenada para cada publicação, cada publicação pode ter um *ftp_address*diferente. A publicação deve oferecer suporte à propagação de instantâneos por meio de FTP.  
  
`[ \@ftp_port = ] ftp_port`É o número da porta do serviço FTP para o distribuidor. *ftp_port* é **int**, com um padrão de 21. Especifica onde os arquivos de instantâneo de publicação ficam localizados para serem captados pelo Distribution Agent ou por um Assinante. Como essa propriedade é armazenada para cada publicação, cada publicação pode ter sua própria *ftp_port*.  
  
`[ \@ftp_subdirectory = ] 'ftp_subdirectory'`Especifica onde os arquivos de instantâneo estarão disponíveis para o Agente de Distribuição ou Agente de Mesclagem de assinante a serem coletados se a publicação der suporte à propagação de instantâneos usando FTP. *ftp_subdirectory* é **nvarchar (255)**, com um padrão de NULL. Como essa propriedade é armazenada para cada publicação, cada publicação pode ter sua própria *ftp_subdirctory* ou optar por não ter subdiretório, indicado com um valor nulo.  
  
`[ \@ftp_login = ] 'ftp_login'`É o nome de usuário usado para se conectar ao serviço FTP. *ftp_login* é **sysname**, com um padrão de anônimo.  
  
`[ \@ftp_password = ] 'ftp_password'`É a senha de usuário usada para se conectar ao serviço FTP. *ftp_password* é **sysname**, com um padrão de NULL.  
  
`[ \@allow_dts = ] 'allow_dts'`Especifica que a publicação permite transformações de dados. Você pode especificar um pacote DTS ao criar uma assinatura. *allow_transformable_subscriptions* é **nvarchar (5)** com um padrão de false, que não permite transformações Dts. Quando *allow_dts* for true, *sync_method* deverá ser definido como **caractere** ou **concurrent_c**.  
  
 **true** *não tem suporte para Publicadores Oracle*.  
  
`[ \@allow_subscription_copy = ] 'allow_subscription_copy'`Habilita ou desabilita a capacidade de copiar os bancos de dados de assinatura que assinam essa publicação. *allow_subscription_copy* é**nvarchar (5)**, com um padrão de false.  
  
`[ \@conflict_policy = ] 'conflict_policy'`Especifica a política de resolução de conflitos seguida quando a opção de assinante de atualização em fila é usada. *conflict_policy* é **nvarchar (100)** com um padrão de NULL e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**pub wins**|O Publicador vence o conflito.|  
|**sub reinit**|Reinicialize a assinatura.|  
|**sub wins**|O Assinante vence o conflito.|  
|NULL (padrão)|Se for NULL e a publicação for uma publicação de instantâneo, a política padrão se tornará **sub reinicialização**. Se NULL e a publicação não for uma publicação de instantâneo, o padrão se tornará **pub**.|  
  
 *Não há suporte para Publicadores Oracle*.  
  
`[ \@centralized_conflicts = ] 'centralized_conflicts'`Especifica se registros de conflito são armazenados no Publicador. *centralized_conflicts* é **nvarchar (5)**, com um padrão de true. Se **for true**, os registros de conflito serão armazenados no Publicador. Se **for false**, os registros de conflito serão armazenados no Publicador e no Assinante que causou o conflito. *Não há suporte para Publicadores Oracle*.  
  
`[ \@conflict_retention = ] conflict_retention`Especifica o período de retenção de conflito, em dias. Esse é o período de tempo em que os metadados de conflito são armazenados para replicação transacional ponto a ponto e assinaturas de atualização enfileiradas. *conflict_retention* é **int**, com um padrão de 14. *Não há suporte para Publicadores Oracle*.  
  
`[ \@queue_type = ] 'queue_type'`Especifica qual tipo de fila é usado. *queue_type* é **nvarchar (10)**, com um padrão de NULL, e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**SQL**|Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para armazenar transações.|  
|NULL (padrão)|O padrão é **SQL**, que especifica o uso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para armazenar transações.|  
  
> [!NOTE]  
>  O suporte para uso do Serviço de Enfileiramento de Mensagens da [!INCLUDE[msCoName](../../includes/msconame-md.md)] foi descontinuado. A especificação de um valor de **MSMQ** resultará em um aviso e a replicação definirá automaticamente o valor como **SQL**.  
  
 *Não há suporte para Publicadores Oracle*.  
  
`[ \@add_to_active_directory = ] 'add\to_active_directory'`Esse parâmetro foi preterido e só tem suporte para a compatibilidade com versões anteriores de scripts. Você não pode mais adicionar informações de publicação ao [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory.  
  
`[ \@logreader_job_name = ] 'logreader_agent_name'`É o nome de um trabalho de agente existente. *logreader_agent_name* é **sysname**, com um valor padrão de NULL. Esse parâmetro só é especificado quando o Log Reader Agent usa um trabalho existente em vez de um novo trabalho que está sendo criado.  
  
`[ \@qreader_job_name = ] 'queue_reader_agent_name'`É o nome de um trabalho de agente existente. *queue_reader_agent_name* é **sysname**, com um valor padrão de NULL. Esse parâmetro só é especificado quando o Queue Reader Agent usa um trabalho existente em vez de um novo trabalho que está sendo criado.  
  
`[ \@publisher = ] 'publisher'`Especifica um não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o *Publicador* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  o *Publicador* não deve ser usado ao adicionar uma publicação a um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador.  
  
`[ \@allow_initialize_from_backup = ] 'allow_initialize_from_backup'`Indica se os assinantes podem inicializar uma assinatura para esta publicação a partir de um backup em vez de um instantâneo inicial. *allow_initialize_from_backup* é **nvarchar (5)** e pode ser um destes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**true**|Habilita inicialização de um backup.|  
|**false**|Desabilita inicialização de um backup.|  
|NULL (padrão)|O padrão é **true** para uma publicação em uma topologia de replicação ponto a ponto e **false** para todas as outras publicações.|  
  
 Para obter mais informações, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
> [!WARNING]  
>  Para evitar perder dados do assinante, ao usar **sp_addpublication** com `@allow_initialize_from_backup = N'true'`, sempre use `@immediate_sync = N'true'`.  
  
`[ \@replicate_ddl = ] replicate_ddl`Indica se a replicação do esquema tem suporte para a publicação. *replicate_ddl* é **int**, com um padrão de **1** para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicadores e **0** para não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicadores. **1** indica que as instruções DDL (linguagem de definição de dados) executadas no Publicador são replicadas e **0** indica que as instruções DDL não são replicadas. *Replicação de esquema não tem suporte para Publicadores Oracle.* Para obter mais informações, consulte [Make Schema Changes on Publication Databases](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md) (Fazer alterações de esquema em bancos de dados de publicação).  
  
 O parâmetro * \@ replicate_ddl* é respeitado quando uma instrução DDL adiciona uma coluna. O parâmetro * \@ replicate_ddl* é ignorado quando uma instrução DDL altera ou descarta uma coluna pelos seguintes motivos.  
  
-   Quando uma coluna é removida, sysarticlecolumns deve ser atualizado para impedir que novas instruções DML incluam a coluna removida que causaria falha no agente de distribuição. O parâmetro * \@ replicate_ddl* é ignorado porque a replicação sempre deve replicar a alteração de esquema.  
  
-   Quando uma coluna é alterada, o tipo de dados de origem ou nulidade podem ter sido alterados, fazendo as instruções DML conterem um valor que pode não ser compatível com a tabela no assinante. Estas instruções DML podem causar falha no agente de distribuição. O parâmetro * \@ replicate_ddl* é ignorado porque a replicação sempre deve replicar a alteração de esquema.  
  
-   Quando uma instrução DDL adiciona uma nova coluna, sysarticlecolumns não inclui a nova coluna. Instruções DML não tentarão replicar dados para a nova coluna. O parâmetro é honrado porque replicar ou não replicar o DDL são aceitáveis.  
  
`[ \@enabled_for_p2p = ] 'enabled_for_p2p'`Permite que a publicação seja usada em uma topologia de replicação ponto a ponto. *enabled_for_p2p* é **nvarchar (5)**, com um padrão de false. **verdadeiro** indica que a publicação dá suporte à replicação ponto a ponto. Ao definir *enabled_for_p2p* como **true**, as seguintes restrições se aplicam:  
  
-   *allow_anonymous* deve ser **false**.  
  
-   *allow_dts* deve ser **false**.  
  
-   *allow_initialize_from_backup* deve ser **true**.  
  
-   *allow_queued_tran* deve ser **false**.  
  
-   *allow_sync_tran* deve ser **false**.  
  
-   *conflict_policy* deve ser **false**.  
  
-   *independent_agent* deve ser **true**.  
  
-   *repl_freq* deve ser **contínua**.  
  
-   *replicate_ddl* deve ser **1**.  
  
 Para obter mais informações, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
`[ \@publish_local_changes_only = ] 'publish_local_changes_only'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ \@enabled_for_het_sub = ] 'enabled_for_het_sub'`Permite que a publicação dê suporte a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes não. *enabled_for_het_sub* é **nvarchar (5)** com um valor padrão de false. Um valor de **true** significa que a publicação dá suporte a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes não. Quando *enabled_for_het_sub* é **true**, as seguintes restrições se aplicam:  
  
-   *allow_initialize_from_backup* deve ser **false**.  
  
-   *allow_push* deve ser **true**.  
  
-   *allow_queued_tran* deve ser **false**.  
  
-   *allow_subscription_copy* deve ser **false**.  
  
-   *allow_sync_tran* deve ser **false**.  
  
-   *autogen_sync_procs* deve ser **false**.  
  
-   *conflict_policy* deve ser nulo.  
  
-   *enabled_for_internet* deve ser **false**.  
  
-   *enabled_for_p2p* deve ser **false**.  
  
-   *ftp_address* deve ser nulo.  
  
-   *ftp_subdirectory* deve ser nulo.  
  
-   *ftp_password* deve ser nulo.  
  
-   *pre_snapshot_script* deve ser nulo.  
  
-   *post_snapshot_script* deve ser nulo.  
  
-   *replicate_ddl* deve ser 0.  
  
-   *qreader_job_name* deve ser nulo.  
  
-   *queue_type* deve ser nulo.  
  
-   *sync_method* não pode ser **nativo** ou **simultâneo**.  
  
 Para obter mais informações, consulte [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
`[ \@p2p_conflictdetection = ] 'p2p_conflictdetection'`Permite que o Agente de Distribuição detecte conflitos se a publicação estiver habilitada para replicação ponto a ponto. *p2p_conflictdetection* é **nvarchar (5)** com um valor padrão de true. Para obter mais informações, consulte [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
`[ \@p2p_originator_id = ] p2p_originator_id`Especifica uma ID para um nó em uma topologia ponto a ponto. *p2p_originator_id* é **int**, com um padrão de NULL. Essa ID será usada para detecção de conflitos se *p2p_conflictdetection* estiver definida como true. Especifica uma ID positiva, diferente de zero, que nunca foi usada na topologia. Para obter uma lista de IDs que já foram usadas, execute [sp_help_peerconflictdetection](../../relational-databases/system-stored-procedures/sp-help-peerconflictdetection-transact-sql.md).  
  
`[ \@p2p_continue_onconflict = ] 'p2p_continue_onconflict'`Determina se o Agente de Distribuição continuará a processar as alterações depois que um conflito for detectado. *p2p_continue_onconflict* é **nvarchar (5)** com um valor padrão de false.  
  
> [!CAUTION]  
>  Recomendamos que você use o valor padrão de FALSE. Quando essa opção é definida como TRUE, o Distribution Agent tenta convergir os dados na topologia aplicando a linha conflitante do nó que tem a ID de origem mais alta. Esse método não garante convergência. Verifique se a topologia está consistente depois que um conflito é detectado. Para obter mais informações, consulte “Controlando conflitos” em [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
  
`[ \@allow_partition_switch = ] 'allow_partition_switch'`Especifica se ALTER TABLE... As instruções SWITCH podem ser executadas no banco de dados publicado. *allow_partition_switch* é **nvarchar (5)** com um valor padrão de false. Para obter mais informações, consulte [Replicar tabelas e índices particionados](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).  
  
`[ \@replicate_partition_switch = ] 'replicate_partition_switch'`Especifica se ALTER TABLE... As instruções SWITCH executadas no banco de dados publicado devem ser replicadas para os assinantes. *replicate_partition_switch* é **nvarchar (5)** com um valor padrão de false. Essa opção só será válida se *allow_partition_switch* estiver definida como true.  

## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addpublication** é usado na replicação de instantâneo e na replicação transacional.  
  
 Se existirem várias publicações que publiquem o mesmo objeto de banco de dados, somente as publicações com um *replicate_ddl* valor de **1** REPLICARÃO as instruções ALTER TABLE, ALTER View, ALTER PROCEDURE, ALTER FUNCTION e ALTER TRIGGER DDL. No entanto, uma instrução ALTER TABLE DROP COLUMN DDL será replicada por todas as publicações que estão publicando a coluna cancelada.  
  
 Com a replicação DDL habilitada (*replicate_ddl*  =  **1**) para uma publicação, a fim de fazer alterações de DDL não replicadas na publicação, [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) deve primeiro ser executado para definir *replicate_ddl* como **0**. Depois que as instruções DDL de não replicação forem emitidas, [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) poderá ser executado novamente para ativar novamente a replicação DDL.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-transa_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_addpublication**. Os logons de autenticação do Windows devem ter uma conta de usuário no banco de dados que representa a conta de usuário do Windows. Uma conta de usuário que representa um grupo do Windows não é suficiente.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_addlogreader_agent](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addpublication_snapshot](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_droppublication](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helppublication](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)   
 [Publicar objetos de banco de dados e](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
