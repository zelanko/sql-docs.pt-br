---
title: sp_helppublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppublication_TSQL
- sp_helppublication
helpviewer_keywords:
- sp_helppublication
ms.assetid: e801c3f0-dcbd-4b4a-b254-949a05f63518
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1f7f75d37762f5e6df971f3139eea118c6a3fdf2
ms.sourcegitcommit: 82a1ad732fb31d5fa4368c6270185c3f99827c97
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/21/2019
ms.locfileid: "72689048"
---
# <a name="sp_helppublication-transact-sql"></a>sp_helppublication (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Retorna informações sobre uma publicação. Para uma [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicação, esse procedimento armazenado é executado no Publicador do banco de dados de publicação. Para uma publicação Oracle, esse procedimento armazenado é executado no distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helppublication [ [ @publication = ] 'publication' ]  
    [ , [ @found=] found OUTPUT]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>argumentos  
`[ @publication = ] 'publication'` é o nome da publicação a ser exibida. a *publicação* é sysname, com um padrão de **%** , que retorna informações sobre todas as publicações.  
  
`[ @found = ] 'found' OUTPUT` é um sinalizador para indicar linhas retornando. *encontrado*é **int** e um parâmetro de saída, com um padrão de **23456**. **1** indica que a publicação foi encontrada. **0** indica que a publicação não foi encontrada.  
  
`[ @publisher = ] 'publisher'` especifica um Publicador que não é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. o *Publicador* é sysname, com um padrão de NULL.  
  
> [!NOTE]  
>  o *Publicador* não deve ser especificado ao solicitar informações de publicação de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|pubid|**inteiro**|ID da publicação.|  
|Nomes|**sysname**|Nome da publicação.|  
|Restricted|**inteiro**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|Estado|**tinyint**|O status atual da publicação.<br /><br /> **0** = inativo.<br /><br /> **1** = ativo.|  
|tarefa||Usado para compatibilidade com versões anteriores.|  
|frequência de replicação|**tinyint**|Tipo de frequência de replicação:<br /><br /> **0** = transacional<br /><br /> **1** = instantâneo|  
|método de sincronização|**tinyint**|Modo de sincronização:<br /><br /> **0** = programa de cópia em massa nativo (utilitário**bcp** )<br /><br /> **1** = cópia em massa de caractere<br /><br /> **3** = simultâneo, o que significa que a cópia em massa nativa (utilitário**bcp**) é usada, mas as tabelas não são bloqueadas durante o instantâneo<br /><br /> **4** = Concurrent_c, o que significa que a cópia em massa de caracteres é usada, mas as tabelas não são bloqueadas durante o instantâneo|  
|Ndescrição|**nvarchar (255)**|Descrição opcional para a publicação.|  
|immediate_sync|**parte**|Se os arquivos de sincronização são criados ou recriados sempre que o Agente de Instantâneo é executado.|  
|enabled_for_internet|**parte**|Se os arquivos de sincronização da publicação são expostos à Internet, por meio de FTP (File Transfer Protocol) e outros serviços.|  
|allow_push|**parte**|Se as assinaturas push são permitidas na publicação.|  
|allow_pull|**parte**|Se as assinaturas pull são permitidas na publicação.|  
|allow_anonymous|**parte**|Se as assinaturas anônimas são permitidas na publicação.|  
|independent_agent|**parte**|Se há um Agente de Distribuição autônomo para esta publicação.|  
|immediate_sync_ready|**parte**|Se o Agente de Instantâneo gerou ou não um instantâneo que está pronto para ser usado por novas assinaturas. Esse parâmetro será definido somente se a publicação estiver definida para sempre ter um instantâneo disponível para assinaturas novas ou reinicializadas.|  
|allow_sync_tran|**parte**|Se as assinaturas de atualização imediata são permitidas na publicação.|  
|autogen_sync_procs|**parte**|Se os procedimentos armazenados devem ser gerados automaticamente para dar suporte a assinaturas de atualização imediata.|  
|snapshot_jobid|**Binary (16)**|ID da tarefa agendada.|  
|políticas|**inteiro**|Quantidade de alteração, em horas, a ser salva para a publicação fornecida.|  
|tem assinatura|**parte**|Se a publicação tiver uma assinatura ativa. **1** significa que a publicação tem assinaturas ativas e **0** significa que a publicação não tem assinaturas.|  
|allow_queued_tran|**parte**|Especifica se o desabilita a fila de alterações no Assinante até que elas possam ser aplicadas no Publicador tenha sido habilitada. Se **0**, as alterações no Assinante não serão enfileiradas.|  
|snapshot_in_defaultfolder|**parte**|Especifica se os arquivos de instantâneo são armazenados na pasta padrão. Se **0**, os arquivos de instantâneo foram armazenados no local alternativo especificado por *alternate_snapshot_folder*. Se **1**, os arquivos de instantâneo podem ser encontrados na pasta padrão.|  
|alt_snapshot_folder|**nvarchar (255)**|Especifica o local da pasta alternativa para o instantâneo.|  
|pre_snapshot_script|**nvarchar (255)**|Especifica um ponteiro para um local de arquivo **. SQL** . O Agente de Distribuição executará o script de pré-instantâneo antes de executar qualquer um dos scripts de objeto replicado ao aplicar um instantâneo em um assinante.|  
|post_snapshot_script|**nvarchar (255)**|Especifica um ponteiro para um local de arquivo **. SQL** . O Agente de Distribuição executará o script de pós-instantâneo depois que todos os outros scripts e dados de objeto replicados tiverem sido aplicados durante uma sincronização inicial.|  
|compress_snapshot|**parte**|Especifica que o instantâneo gravado no local da *alt_snapshot_folder* deve ser compactado no formato CAB [!INCLUDE[msCoName](../../includes/msconame-md.md)]. **0** especifica que o instantâneo não será compactado.|  
|ftp_address|**sysname**|O endereço de rede do serviço FTP para o distribuidor. Especifica onde os arquivos de instantâneo de publicação estão localizados para o Agente de Distribuição ou Agente de Mesclagem de um assinante a ser coletado.|  
|ftp_port|**inteiro**|O número da porta do serviço FTP para o distribuidor.|  
|ftp_subdirectory|**nvarchar (255)**|Especifica onde os arquivos de instantâneo estarão disponíveis para o Agente de Distribuição ou Agente de Mesclagem de assinante a serem coletados se a publicação der suporte à propagação de instantâneos usando FTP.|  
|ftp_login|**sysname**|O nome de usuário usado para se conectar ao serviço FTP.|  
|allow_dts|**parte**|Especifica que a publicação permite transformações de dados. **0** especifica que as transformações DTS não são permitidas.|  
|allow_subscription_copy|**parte**|Especifica se a capacidade de copiar os bancos de dados de assinatura que assinam esta publicação foi habilitada. **0** significa que a cópia não é permitida.|  
|centralized_conflicts|**parte**|Especifica se os registros de conflitos são armazenados no Publicador:<br /><br /> **0** = registros de conflitos são armazenados no Publicador e no Assinante que causou o conflito.<br /><br /> **1** = registros de conflitos são armazenados no Publicador.|  
|conflict_retention|**inteiro**|Especifica o período de retenção de conflito, em dias.|  
|conflict_policy|**inteiro**|Especifica a política de resolução de conflitos seguida quando a opção de assinante de atualização em fila é usada. Pode ser um destes valores:<br /><br /> **1** = o Publicador vence o conflito.<br /><br /> **2** = Assinante vence o conflito.<br /><br /> **3** = a assinatura é reinicializada.|  
|queue_type||Especifica qual tipo de fila é usado. Pode ser um destes valores:<br /><br /> **MSMQ** = use [!INCLUDE[msCoName](../../includes/msconame-md.md)] enfileiramento de mensagens para armazenar transações.<br /><br /> **SQL** = use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para armazenar transações.<br /><br /> Observação: o suporte para enfileiramento de mensagens foi descontinuado.|  
|backward_comp_level||Nível de compatibilidade do banco de dados e pode ser um dos seguintes:<br /><br /> **90**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **100**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|publish_to_AD|**parte**|Especifica se a publicação é publicada no Active Directory de [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Um valor de **1** indica que ele é publicado e um valor de **0** indica que ele não está publicado.|  
|allow_initialize_from_backup|**parte**|Indica se os assinantes podem inicializar uma assinatura para esta publicação a partir de um backup em vez de um instantâneo inicial. **1** significa que as assinaturas podem ser inicializadas a partir de um backup e **0** significa que elas não podem. Para obter mais informações, consulte [inicializar uma assinatura transacional sem um](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md) assinante transacional de um instantâneo sem um instantâneo.|  
|replicate_ddl|**inteiro**|Indica se a replicação do esquema tem suporte para a publicação. **1** indica que as instruções DDL (linguagem de definição de dados) executadas no Publicador são replicadas e **0** indica que as instruções DDL não são replicadas. Para obter mais informações, consulte [fazer alterações de esquema em bancos de dados de publicação](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).|  
|enabled_for_p2p|**inteiro**|Se a publicação puder ser usada em uma topologia de replicação ponto a ponto. **1** indica que a publicação dá suporte à replicação ponto a ponto. Para obter mais informações, consulte [replicação transacional ponto a ponto](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).|  
|publish_local_changes_only|**inteiro**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|enabled_for_het_sub|**inteiro**|Especifica se a publicação dá suporte a assinantes não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um valor de **1** significa que os assinantes não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] têm suporte. Um valor de **0** significa que apenas os assinantes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] têm suporte. Para obter mais informações, consulte [assinantes não SQL Server](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).|  
|enabled_for_p2p_conflictdetection|**inteiro**|Especifica se o Agente de Distribuição detecta conflitos para uma publicação que está habilitada para replicação ponto a ponto. Um valor de **1** significa que os conflitos são detectados. Para obter mais informações, consulte [detecção de conflitos na replicação ponto a ponto](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
|originator_id|**inteiro**|Especifica uma ID para um nó em uma topologia ponto a ponto. Essa ID será usada para detecção de conflitos se **enabled_for_p2p_conflictdetection** estiver definido como **1**. Para obter uma lista de IDs que já foram usadas, consulte a tabela do sistema [MSpeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) .|  
|p2p_continue_onconflict|**inteiro**|Especifica se o Agente de Distribuição continuará a processar as alterações quando um conflito for detectado. Um valor de **1** significa que o agente continua a processar as alterações.<br /><br /> **\* \* cuidado \* \*** Recomendamos que você use o valor padrão de **0**. Quando essa opção é definida como **1**, a agente de distribuição tenta convergir dados na topologia aplicando a linha conflitante do nó que tem a ID de originador mais alta. Esse método não garante a convergência. Você deve garantir que a topologia seja consistente depois que um conflito for detectado. Para obter mais informações, consulte "Manipulando conflitos" em [detecção de conflitos na replicação ponto a ponto](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
|allow_partition_switch|**inteiro**|Especifica se ALTER TABLE... As instruções SWITCH podem ser executadas no banco de dados publicado. Para obter mais informações, consulte [replicar tabelas e índices particionados](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).|  
|replicate_partition_switch|**inteiro**|Especifica se ALTER TABLE... As instruções SWITCH executadas no banco de dados publicado devem ser replicadas para os assinantes. Essa opção só será válida se *allow_partition_switch* estiver definido como **1**.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 sp_helppublication é usado em instantâneo e replicação transacional.  
  
 sp_helppublication retornará informações sobre todas as publicações que pertencem ao usuário que está executando este procedimento.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_helppublication](../../relational-databases/replication/codesnippet/tsql/sp-helppublication-trans_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa sysadmin no Publicador ou membros da função de banco de dados fixa db_owner no banco de dados de publicação ou usuários na PAL (lista de acesso à publicação) podem executar sp_helppublication.  
  
 Para um Publicador não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], somente membros da função de servidor fixa sysadmin no distribuidor ou membros da função de banco de dados fixa db_owner no banco de dados de distribuição ou usuários na PAL podem executar sp_helppublication.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)    
 [  &#40;Transact-SQL&#41; sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)  
 [  &#40;Transact-SQL&#41; sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)  
 [  &#40;Transact-SQL&#41; sp_droppublication](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)  
 [Procedimentos &#40;armazenados de replicação TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
