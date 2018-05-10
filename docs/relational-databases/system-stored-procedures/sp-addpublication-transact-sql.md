---
title: sp_addpublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_addpublication_TSQL
- sp_addpublication
helpviewer_keywords:
- sp_addpublication
ms.assetid: c7167ed1-2b7e-4824-b82b-65f4667c4407
caps.latest.revision: 69
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 59fcdcebd8c8397de2669491d4ea18cb38cfc853
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spaddpublication-transact-sql"></a>sp_addpublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria uma publicação de instantâneo ou transacional. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação a ser criada. *publicação* é **sysname**, sem padrão. O nome deve ser exclusivo no banco de dados.  
  
 [  **@taskid=**] *taskid*  
 Suporte para compatibilidade com versões anteriores. Use [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md).  
  
 [  **@restricted=**] **'***restrito***'**  
 Suporte para compatibilidade com versões anteriores. Use *default_access*.  
  
 [  **@sync_method=**] *'sync_method *'**  
 É o modo de sincronização. *método sync_method* é **nvarchar(13)**, e pode ser um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**native**|Produz saída de programa de cópia em massa em modo nativo de todas as tabelas. *Não há suportada para editores Oracle*.|  
|**character**|Produz saída de programa de cópia em massa em modo de caractere de todas as tabelas. *Para um publicador Oracle,* **caracteres** *é válido somente para replicação de instantâneo*.|  
|**simultâneas**|Produz saída de programa de cópia em massa em modo nativo de todas as tabelas, mas não bloqueia as tabelas durante o instantâneo. Com suporte somente para publicações transacionais. *Não há suportada para editores Oracle*.|  
|**concurrent_c**|Produz saída de programa de cópia em massa em modo de caractere de todas as tabelas, mas não bloqueia as tabelas durante o instantâneo. Com suporte somente para publicações transacionais.|  
|**Instantâneo do banco de dados**|Produz saída de programa de cópia em massa em modo nativo de todas as tabelas de um instantâneo do banco de dados. Instantâneos de banco de dados não estão disponíveis em todas as edições de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).|  
|**caractere de instantâneo de banco de dados**|Produz saída de programa de cópia em massa em modo de caractere de todas as tabelas de um instantâneo de banco de dados. Instantâneos de banco de dados não estão disponíveis em todas as edições de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).|  
|NULL (padrão)|O padrão será a **nativo** para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] editores. Para não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] editores, o padrão é **caracteres** quando o valor de *repl_freq* é **instantâneo** e **concurrent_c** para todos os outros casos.|  
  
 [  **@repl_freq=**] **'***repl_freq***'**  
 É o tipo de frequência de replicação, *repl_freq* é **nvarchar (10)**, e pode ser um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**contínua** (padrão)|O Publicador fornece saída de todas as transações com base em log. Para não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] editores, isso requer que *sync_method* ser definido como **concurrent_c**.|  
|**Instantâneo**|O Publicador só produz eventos de sincronização agendados. Para não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] editores, isso requer que *sync_method* ser definido como **caracteres**.|  
  
 [  **@description=**] **'***descrição***'**  
 É uma descrição opcional para a publicação. *Descrição* é **nvarchar (255)**, com um padrão NULL.  
  
 [  **@status=**] **'***status***'**  
 Especifica se os dados da publicação estão disponíveis. *status* é **nvarchar (8)**, e pode ser um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Ativo**|O dados da publicação estão imediatamente disponíveis para os Assinantes.|  
|**inativo** (padrão)|Os dados da publicação não estão disponíveis aos Assinantes quando a publicação é criada pela primeira vez (eles podem assinar, mas as assinaturas não são processadas).|  
  
 *Não há suportada para editores Oracle*.  
  
 [  **@independent_agent=**] **'***independent_agent***'**  
 Especifica se existe um Agente de Distribuição autônomo para esta publicação. *independent_agent* é **nvarchar (5)**, com um padrão de FALSE. Se **true**, há um Distribution Agent autônomo para essa publicação. Se **false**, a publicação usa um Distribution Agent compartilhado e cada par de banco de dados do publicador/assinante tem um agente compartilhado, único.  
  
 [  **@immediate_sync=**] **'***immediate_synchronization***'**  
 Especifica se os arquivos de sincronização da publicação são criados em cada execução do Agente de Instantâneo. *immediate_synchronization* é **nvarchar (5)**, com um padrão de FALSE. Se **true**, os arquivos de sincronização são criados ou recriados cada vez que o Snapshot Agent é executado. Assinantes podem obter arquivos de sincronização imediatamente se o Snapshot Agent for concluído antes da assinatura ser criada. Novas assinaturas obtêm os arquivos de sincronização mais novos gerados pela execução mais recente do Agente de Instantâneo. *independent_agent* devem ser **true** para *immediate_synchronization* ser **true**. Se **false**, os arquivos de sincronização são criados somente se houver novas assinaturas. Você deve chamar [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) para cada assinatura quando você adicionar paulatinamente um novo artigo para uma publicação existente. Assinantes não podem receber arquivos de sincronização após a assinatura até que os Snapshot Agents sejam iniciados e concluídos.  
  
 [  **@enabled_for_internet=**] **'***enabled_for_internet***'**  
 Especifica se a publicação está habilitada para a Internet, e determina se o protocolo FTP pode ser usado para transferir os arquivos de instantâneo para um assinante. *enabled_for_internet* é **nvarchar (5)**, com um padrão de FALSE. Se **true**, os arquivos de sincronização para a publicação são colocados no diretório C:\Program Files\Microsoft SQL server\mssql\mssql.x\repldata\ftp. O usuário deve criar o diretório Ftp.  
  
 [  **@allow_push=**] **'***allow_push***'**  
 Especifica se podem ser criadas assinaturas push para a publicação determinada. *allow_push* é **nvarchar (5)**, com um padrão de TRUE, que permite assinaturas push na publicação.  
  
 [  **@allow_pull=**] **'***allow_pull***'**  
 Especifica se podem ser criadas assinaturas pull para a publicação determinada. *allow_pull* é **nvarchar (5)**, com um padrão de FALSE. Se **false**, não são permitidas assinaturas pull na publicação.  
  
 [  **@allow_anonymous=**] **'***allow_anonymous***'**  
 Especifica se podem ser criadas assinaturas anônimas para a publicação determinada. *allow_anonymous* é **nvarchar (5)**, com um padrão de FALSE. Se **true**, *immediate_synchronization* também deve ser definido como **true**. Se **false**, não são permitidas assinaturas anônimas na publicação.  
  
 [  **@allow_sync_tran=**] **'***allow_sync_tran***'**  
 Especifica se são permitidas assinaturas de atualização imediata na publicação. *allow_sync_tran* é **nvarchar (5)**, com um padrão de FALSE. **True** é *não tem suporte para editores Oracle*.  
  
 [  **@autogen_sync_procs=**] **'***autogen_sync_procs***'**  
 Especifica se o procedimento armazenado de sincronização para assinaturas de atualização imediata é gerado no Publicador. *autogen_sync_procs* é **nvarchar (5)**, e pode ser um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**true**|Definido automaticamente quando assinaturas de atualização estão habilitadas.|  
|**false**|Definido automaticamente quando assinaturas de atualização não estão habilitadas ou para Publicadores Oracle.|  
|NULL (padrão)|Padrão é **true** quando assinaturas de atualização está habilitada e **false** quando o assinaturas de atualização não está habilitada.|  
  
> [!NOTE]  
>  O usuário forneceu um valor para *autogen_sync_procs*será substituído, dependendo dos valores especificados para *allow_queued_tran* e *allow_sync_tran*.  
  
 [  **@retention=**] *retenção*  
 É o período de retenção, em horas, para atividade de assinatura. *retenção* é **int**, com um padrão de 336 horas. Se uma assinatura não estiver ativa dentro do período de retenção, expirará e será removida. O valor pode ser maior que o período de retenção de máximo do banco de dados de distribuição usado pelo Publicador. Se **0**, assinaturas conhecidas na publicação nunca irão expirar e ser removidas pelo agente de limpeza de assinatura expirada.  
  
 [  **@allow_queued_tran=** ] **'***allow_queued_updating***'**  
 Habilita ou desabilita o enfileiramento de mensagens no Assinante até que possam ser aplicadas no Publicador. *allow_queued_updating* é **nvarchar (5)** com um padrão de FALSE. Se **false**, as alterações no assinante não serão enfileiradas. **True** é *não tem suporte para editores Oracle*.  
  
 [  **@snapshot_in_defaultfolder=** ] **'***snapshot_in_default_folder***'**  
 Especifica se os arquivos de instantâneo são armazenados na pasta padrão. *snapshot_in_default_folder* é **nvarchar (5)** com um padrão de TRUE. Se **true**, arquivos de instantâneo podem ser encontrados na pasta padrão. Se **false**, arquivos de instantâneo foram armazenados no local alternativo especificado por *alternate_snapshot_folder*. Locais alternativos podem ficar em outro servidor, em uma unidade de rede, ou uma mídia removível (como um CD-ROM ou disco removível). Você também pode salvar os arquivos de instantâneo em um site de FTP para ser recuperado pelo Assinante posteriormente Observe que esse parâmetro pode ser verdadeiro e ainda ter um local no **@alt_snapshot_folder** parâmetro. Essa combinação Especifica que os arquivos de instantâneo serão armazenados em ambos os locais padrão e alternativos.  
  
 [  **@alt_snapshot_folder=** ] **'***alternate_snapshot_folder***'**  
 Especifica o local da pasta alternativa para o instantâneo. *alternate_snapshot_folder* é **nvarchar (255)** com um padrão NULL.  
  
 [  **@pre_snapshot_script=** ] **'***pre_snapshot_script***'**  
 Especifica um ponteiro para um **. SQL** local do arquivo. *pre_snapshot_script* é **nvarchar (255),** com um padrão NULL. O Agente de Distribuição executará o script pré-instantâneo antes de executar qualquer script de objeto replicado, ao aplicar um instantâneo no Assinante. O script é executado no contexto de segurança usado pelo Distribution Agente na conexão com o banco de dados de assinatura.  
  
 [  **@post_snapshot_script=** ] **'***post_snapshot_script***'**  
 Especifica um ponteiro para um **. SQL** local do arquivo. *post_snapshot_script* é **nvarchar (255)**, com um padrão NULL. O Agente de Distribuição executará o script pós-instantâneo depois que todos os outros scripts de objeto replicado tentam sido aplicados durante uma sincronização inicial. O script é executado no contexto de segurança usado pelo Distribution Agente na conexão com o banco de dados de assinatura.  
  
 [  **@compress_snapshot=** ] **'***compress_snapshot***'**  
 Especifica que o instantâneo foi criado para o **@alt_snapshot_folder** local é compactado no [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato CAB. *compress_snapshot* é **nvarchar (5)**, com um padrão de FALSE. **False** Especifica que o instantâneo não será compactado; **true** Especifica que o instantâneo será compactado. Arquivos de instantâneo maiores de 2 gigabytes (GB) não podem ser compactados. Arquivos de instantâneo compactados são descompactados no local onde o Distribution Agent é executado; assinaturas pull são geralmente usadas com instantâneos compactados para que os arquivos sejam descompactados no Assinante. O instantâneo na pasta padrão não pode ser compactado.  
  
 [  **@ftp_address =** ] **'***ftp_address***'**  
 É o endereço de rede do serviço FTP para o Distribuidor. *ftp_address* é **sysname**, com um padrão NULL. Especifica onde os arquivos de instantâneo de publicação ficam localizados para serem captados pelo Agente de Distribuição ou por um Assinante. Como essa propriedade é armazenada para cada publicação, cada publicação pode ter outro *ftp_address*. A publicação deve oferecer suporte à propagação de instantâneos por meio de FTP.  
  
 [  **@ftp_port=** ] *ftp_port*  
 É o número da porta do serviço FTP para o Distribuidor. *ftp_port* é **int**, com um padrão de 21. Especifica onde os arquivos de instantâneo de publicação ficam localizados para serem captados pelo Distribution Agent ou por um Assinante. Como essa propriedade é armazenada para cada publicação, cada publicação pode ter seu próprio *ftp_port*.  
  
 [  **@ftp_subdirectory =** ] **'***ftp_subdirectory***'**  
 Especifica onde os arquivos de instantâneo estarão disponíveis para serem retirados pelo Agente de Distribuição ou Agente de Mesclagem do Assinante se a publicação oferecer suporte à propagação de instantâneo usando o FTP.   *ftp_subdirectory* é **nvarchar (255)**, com um padrão NULL. Como essa propriedade é armazenada para cada publicação, cada publicação pode ter seu próprio *ftp_subdirctory* ou optar por não ter um subdiretório indicado com um valor nulo.  
  
 [  **@ftp_login =** ] **'***ftp_login***'**  
 O nome de usuário é usada para se conectar ao serviço FTP. *ftp_login* é **sysname**, com um padrão de ANONYMOUS.  
  
 [  **@ftp_password =** ] **'***ftp_password***'**  
 É a senha de usuário usada para se conectar ao serviço FTP. *ftp_password* é **sysname**, com um padrão NULL.  
  
 [  **@allow_dts =** ] **'***allow_dts***'**  
 Especifica que a publicação permite transformações de dados. Você pode especificar um pacote DTS ao criar uma assinatura. *allow_transformable_subscriptions* é **nvarchar (5)** com um padrão de FALSE, que não permite transformações DTS. Quando *allow_dts* for true, *sync_method* deve ser definido como **caracteres** ou **concurrent_c**.  
  
 **True** é *não tem suporte para editores Oracle*.  
  
 [  **@allow_subscription_copy =** ] **'***allow_subscription_copy***'**  
 Habilita ou desabilita a capacidade para copiar os bancos de dados de assinatura que assinam essa publicação. *allow_subscription_copy* é**nvarchar (5)**, com um padrão de FALSE.  
  
 [  **@conflict_policy =** ] **'***conflict_policy***'**  
 Especifica a política de resolução de conflito seguida quando a opção de assinante de atualização enfileirado é usada. *conflict_policy* é **nvarchar (100)** com um padrão NULL, e pode ser um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**wins pub**|O Publicador vence o conflito.|  
|**sub reinit**|Reinicialize a assinatura.|  
|**sub wins**|O Assinante vence o conflito.|  
|NULL (padrão)|Se NULL e a publicação for uma publicação de instantâneo, a política padrão será **sub reinit**. Se NULL e a publicação não for uma publicação de instantâneo, o padrão será **wins pub**.|  
  
 *Não há suportada para editores Oracle*.  
  
 [  **@centralized_conflicts =** ] **'***centralized_conflicts***'**  
 Especifica se registros de conflito são armazenados no Publicador. *centralized_conflicts* é **nvarchar (5)**, com um padrão de TRUE. Se **true**, registros de conflito são armazenados no publicador. Se **false**, registros de conflito são armazenados no publicador e no assinante que causou o conflito. *Não há suportada para editores Oracle*.  
  
 [  **@conflict_retention =** ] *conflict_retention*  
 Especifica o período de retenção de conflito, em dias. Esse é o período de tempo em que os metadados de conflito são armazenados para replicação transacional ponto a ponto e assinaturas de atualização enfileiradas. *conflict_retention* é **int**, com um padrão de 14. *Não há suportada para editores Oracle*.  
  
 [  **@queue_type =** ] **'***queue_type***'**  
 Especifica o tipo de fila usado. *QUEUE_TYPE* é **nvarchar (10)**, com um padrão NULL, e pode ser um destes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**sql**|Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para armazenar transações.|  
|NULL (padrão)|O padrão será a **sql**, que especifica para usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para armazenar transações.|  
  
> [!NOTE]  
>  O suporte para uso do Serviço de Enfileiramento de Mensagens da [!INCLUDE[msCoName](../../includes/msconame-md.md)] foi descontinuado. Especificando um valor de **msmq** resultará em um aviso e replicação definirá automaticamente o valor como **sql**.  
  
 *Não há suportada para editores Oracle*.  
  
 [  **@add_to_active_directory =** ] **' * Adicionar**_**to_active_directory * '**  
 Esse parâmetro foi preterido e tem suporte somente para a compatibilidade com versões anteriores de scripts. Você não pode mais adicionar informações de publicação ao [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory.  
  
 [  **@logreader_job_name =** ] **'***logreader_agent_name***'**  
 É o nome de um trabalho de agente existente. *logreader_agent_name* é **sysname**, com um valor padrão de NULL. Esse parâmetro só é especificado quando o Log Reader Agent usa um trabalho existente em vez de um novo trabalho que está sendo criado.  
  
 [  **@qreader_job_name =** ] **'***queue_reader_agent_name***'**  
 É o nome de um trabalho de agente existente. *queue_reader_agent_name* é **sysname**, com um valor padrão de NULL. Esse parâmetro só é especificado quando o Queue Reader Agent usa um trabalho existente em vez de um novo trabalho que está sendo criado.  
  
 [  **@publisher =** ] **'***publicador***'**  
 Especifica um publicador que não é do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *publicador* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  *publicador* não deve ser usado durante a adição de uma publicação para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
 [  **@allow_initialize_from_backup =** ] **'***allow_initialize_from_backup***'**  
 Indica se os Assinantes podem iniciar uma assinatura para essa publicação de um backup em vez de um instantâneo inicial. *allow_initialize_from_backup* é **nvarchar (5)**, e pode ser um destes valores:  
  
|Value|Description|  
|-----------|-----------------|  
|**true**|Habilita inicialização de um backup.|  
|**false**|Desabilita inicialização de um backup.|  
|NULL (padrão)|O padrão será a **true** para uma publicação em uma topologia de replicação ponto a ponto e **false** para todas as outras publicações.|  
  
 Para obter mais informações, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
> [!WARNING]  
>  Para evitar perder dados do assinante, ao usar **sp_addpublication** com `@allow_initialize_from_backup = N'true'`, sempre use `@immediate_sync = N'true'`.  
  
 [  **@replicate_ddl =** ] *replicate_ddl*  
 Indica se a replicação de esquema tem suporte para a publicação. *replicate_ddl* é **int**, com um padrão de **1** para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] editores e **0** para não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] editores. **1** indica que instruções de DDL (linguagem) de definição de dados executadas no publicador são replicadas e **0** indica que instruções DDL não são replicadas. *Não há suporte para replicação de esquema para editores Oracle.* Para obter mais informações, consulte [Make Schema Changes on Publication Databases](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md) (Fazer alterações de esquema em bancos de dados de publicação).  
  
 O *@replicate_ddl* parâmetro é honrado quando uma instrução DDL adiciona uma coluna. O *@replicate_ddl* parâmetro é ignorado quando uma instrução DDL altera ou remove uma coluna pelas razões a seguir.  
  
-   Quando uma coluna for descartada, sysarticlecolumns deve ser atualizado para impedir que novas instruções DML incluam a coluna removida que causaria o distribution agent falha. O *@replicate_ddl* parâmetro é ignorado porque a replicação sempre deve replicar a alteração de esquema.  
  
-   Quando uma coluna é alterada, o tipo de dados de origem ou nulidade podem ter sido alterados, fazendo as instruções DML conterem um valor que pode não ser compatível com a tabela no assinante. Estas instruções DML podem causar falha no agente de distribuição. O *@replicate_ddl* parâmetro é ignorado porque a replicação sempre deve replicar a alteração de esquema.  
  
-   Quando uma instrução DDL adiciona uma nova coluna, sysarticlecolumns não inclui a nova coluna. Instruções DML não tentarão replicar dados para a nova coluna. O parâmetro é honrado porque replicar ou não replicar o DDL são aceitáveis.  
  
 [  **@enabled_for_p2p =** ] **'***enabled_for_p2p***'**  
 Permite que a publicação seja usada em uma topologia de replicação ponto a ponto. *enabled_for_p2p* é **nvarchar (5)**, com um padrão de FALSE. **True** indica que a publicação oferece suporte a replicação ponto a ponto. Ao definir *enabled_for_p2p* para **true**, as seguintes restrições se aplicam:  
  
-   *allow_anonymous* devem ser **false**.  
  
-   *allow_dts* devem ser **false**.  
  
-   *allow_initialize_from_backup* devem ser **true**.  
  
-   *allow_queued_tran* devem ser **false**.  
  
-   *allow_sync_tran* devem ser **false**.  
  
-   *conflict_policy* devem ser **false**.  
  
-   *independent_agent* devem ser **true**.  
  
-   *repl_freq* devem ser **contínua**.  
  
-   *replicate_ddl* devem ser **1**.  
  
 Para obter mais informações, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 [  **@publish_local_changes_only =** ] **'***publish_local_changes_only***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@enabled_for_het_sub=** ] **'***enabled_for_het_sub***'**  
 Permite que a publicação dê suporte a Assinantes que não são do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *enabled_for_het_sub* é **nvarchar (5)** com um valor padrão de FALSE. Um valor de **true** significa que a publicação oferece suporte a não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes. Quando *enabled_for_het_sub* é **true**, as seguintes restrições se aplicam:  
  
-   *allow_initialize_from_backup* devem ser **false**.  
  
-   *allow_push* devem ser **true**.  
  
-   *allow_queued_tran* devem ser **false**.  
  
-   *allow_subscription_copy* devem ser **false**.  
  
-   *allow_sync_tran* devem ser **false**.  
  
-   *autogen_sync_procs* devem ser **false**.  
  
-   *conflict_policy* deve ser NULL.  
  
-   *enabled_for_internet* devem ser **false**.  
  
-   *enabled_for_p2p* devem ser **false**.  
  
-   *ftp_address* deve ser NULL.  
  
-   *ftp_subdirectory* deve ser NULL.  
  
-   *ftp_password* deve ser NULL.  
  
-   *pre_snapshot_script* deve ser NULL.  
  
-   *post_snapshot_script* deve ser NULL.  
  
-   *replicate_ddl* deve ser 0.  
  
-   *qreader_job_name* deve ser NULL.  
  
-   *QUEUE_TYPE* deve ser NULL.  
  
-   *método sync_method* não pode ser **nativo** ou **simultâneos**.  
  
 Para obter mais informações, consulte [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
 [  **@p2p_conflictdetection=** ] **'***p2p_conflictdetection***'**  
 Permite que o Agente de Distribuição detecte conflitos se a publicação for habilitada para replicação ponto a ponto. *p2p_conflictdetection* é **nvarchar (5)** com um valor padrão de TRUE. Para obter mais informações, consulte [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
 [  **@p2p_originator_id=** ] *p2p_originator_id*  
 Especifica uma ID para um nó em uma topologia ponto a ponto. *p2p_originator_id* é **int**, com um padrão NULL. Essa ID é usada para detecção de conflitos se *p2p_conflictdetection* está definida como TRUE. Especifica uma ID positiva, diferente de zero, que nunca foi usada na topologia. Para obter uma lista de IDs que já foram usados, execute [sp_help_peerconflictdetection](../../relational-databases/system-stored-procedures/sp-help-peerconflictdetection-transact-sql.md).  
  
 [  **@p2p_continue_onconflict=** ] **'***p2p_continue_onconflict***'**  
 Determina se o Agente de Distribuição deve continuar processando alterações depois da detecção de um conflito. *p2p_continue_onconflict* é **nvarchar (5)** com um valor padrão de FALSE.  
  
> [!CAUTION]  
>  Recomendamos que você use o valor padrão de FALSE. Quando essa opção é definida como TRUE, o Distribution Agent tenta convergir os dados na topologia aplicando a linha conflitante do nó que tem a ID de origem mais alta. Esse método não garante convergência. Verifique se a topologia está consistente depois que um conflito é detectado. Para obter mais informações, consulte “Controlando conflitos” em [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
 [  **@allow_partition_switch=** ] **'***allow_partition_switch***'**  
 Especifica se as instruções ALTER TABLE…SWITCH podem ser executadas no banco de dados publicado. *allow_partition_switch* é **nvarchar (5)** com um valor padrão de FALSE. Para obter mais informações, consulte [Replicar tabelas e índices particionados](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).  
  
 [  **@replicate_partition_switch=** ] **'***replicate_partition_switch***'**  
 Especifica se as instruções ALTER TABLE…SWITCH que são executadas no banco de dados publicado devem ser replicadas para Assinantes. *replicate_partition_switch* é **nvarchar (5)** com um valor padrão de FALSE. Essa opção é válida somente se *allow_partition_switch* está definida como TRUE.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_addpublication** é usado em replicação de instantâneo e replicação transacional.  
  
 Se houver várias publicações que publica o mesmo objeto de banco de dados, somente publicações com um *replicate_ddl* valor **1** replicará ALTER TABLE, ALTER VIEW, ALTER PROCEDURE, ALTER FUNCTION e Instruções ALTER TRIGGER DDL. No entanto, uma instrução ALTER TABLE DROP COLUMN DDL será replicada por todas as publicações que estão publicando a coluna cancelada.  
  
 Com replicação DDL habilitada (*replicate_ddl* = **1**) para uma publicação, para fazer a DDL de não replicação alterações na publicação, [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) deve ser primeiro executado para definir *replicate_ddl* para **0**. Depois que as instruções de DDL de não replicação forem emitidas, [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) pode ser executado novamente para retroceder a replicação de DDL.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-transa_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_addpublication**. Os logons de autenticação do Windows devem ter uma conta de usuário no banco de dados que representa a conta de usuário do Windows. Uma conta de usuário que representa um grupo do Windows não é suficiente.  
  
## <a name="see-also"></a>Consulte também  
 [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)   
 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_droppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [sp_replicationdboption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)   
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
