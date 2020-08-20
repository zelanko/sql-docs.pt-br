---
description: sp_helppublication (Transact-SQL)
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: dd5452439cc3467cc840ac11dd9ce3cf880a4ce8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489295"
---
# <a name="sp_helppublication-transact-sql"></a>sp_helppublication (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Retorna informações sobre uma publicação. Para uma [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicação, esse procedimento armazenado é executado no Publicador do banco de dados de publicação. Para uma publicação Oracle, esse procedimento armazenado é executado no Distribuidor, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helppublication [ [ @publication = ] 'publication' ]  
    [ , [ @found=] found OUTPUT]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação a ser exibida. a *publicação* é sysname, com um padrão de **%** , que retorna informações sobre todas as publicações.  
  
`[ @found = ] 'found' OUTPUT` É um sinalizador para indicar linhas de retorno. *encontrado*é **int** e um parâmetro de saída, com um padrão de **23456**. **1** indica que a publicação foi encontrada. **0** indica que a publicação não foi encontrada.  
  
`[ @publisher = ] 'publisher'` Especifica um não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o *Publicador* é sysname, com um padrão de NULL.  
  
> [!NOTE]  
>  o *Publicador* não deve ser especificado ao solicitar informações de publicação de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|pubid|**int**|ID da publicação.|  
|name|**sysname**|Nome da publicação.|  
|restricted|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|status|**tinyint**|O status atual da publicação.<br /><br /> **0** = inativo.<br /><br /> **1** = ativo.|  
|task||Usado para compatibilidade com versões anteriores.|  
|frequência de replicação|**tinyint**|Tipo de frequência de replicação:<br /><br /> **0** = transacional<br /><br /> **1** = instantâneo|  
|método de sincronização|**tinyint**|Modo de sincronização:<br /><br /> **0** = programa de cópia em massa nativo (utilitário**bcp** )<br /><br /> **1** = cópia em massa de caractere<br /><br /> **3** = simultâneo, o que significa que a cópia em massa nativa (utilitário**bcp**) é usada, mas as tabelas não são bloqueadas durante o instantâneo<br /><br /> **4** = Concurrent_c, o que significa que a cópia em massa de caracteres é usada, mas as tabelas não são bloqueadas durante o instantâneo|  
|descrição|**nvarchar(255)**|Descrição opcional para a publicação.|  
|immediate_sync|**bit**|Se os arquivos de sincronização serão criados ou recriados em cada execução do Agente de Instantâneo.|  
|enabled_for_internet|**bit**|Se os arquivos de sincronização para a publicação são expostos na Internet pelo FTP (File Transfer Protocol) e outros serviços.|  
|allow_push|**bit**|Se são permitidas assinaturas push na publicação.|  
|allow_pull|**bit**|Se são permitidas assinaturas pull na publicação.|  
|allow_anonymous|**bit**|Se são permitidas assinatura anônimas na publicação.|  
|independent_agent|**bit**|Se há um Agente de Distribuição autônomo para essa publicação.|  
|immediate_sync_ready|**bit**|Se o Agente de Instantâneo gerou um instantâneo que está pronto para ser usado por novas assinaturas. Esse parâmetro só será definido se a publicação estiver definida para ter sempre um instantâneo disponível para assinaturas novas ou reiniciadas.|  
|allow_sync_tran|**bit**|Se são permitidas assinaturas de atualização imediata na publicação.|  
|autogen_sync_procs|**bit**|Se procedimentos armazenados devem ser gerados automaticamente dar suporte a assinaturas de atualização imediata.|  
|snapshot_jobid|**binary(16)**|ID de tarefa agendada.|  
|retenção|**int**|A quantidade de alteração, em horas, a ser salva para a publicação determinada.|  
|has subscription|**bit**|Se a publicação tem assinatura ativas. **1** significa que a publicação tem assinaturas ativas e **0** significa que a publicação não tem assinaturas.|  
|allow_queued_tran|**bit**|Especifica se o serviço de enfileiramento de alterações no Assinante foi desabilitado até que possam ser aplicadas no Publicador. Se **0**, as alterações no Assinante não serão enfileiradas.|  
|snapshot_in_defaultfolder|**bit**|Especifica se arquivos de instantâneo são armazenados na pasta padrão. Se **0**, os arquivos de instantâneo foram armazenados no local alternativo especificado pelo *alternate_snapshot_folder*. Se **1**, os arquivos de instantâneo podem ser encontrados na pasta padrão.|  
|alt_snapshot_folder|**nvarchar(255)**|Especifica o local da pasta alternativa para o instantâneo.|  
|pre_snapshot_script|**nvarchar(255)**|Especifica um ponteiro para um local de arquivo **. SQL** . O Agente de Distribuição executará o script pré-instantâneo antes de executar qualquer script de objeto replicado, ao aplicar um instantâneo no Assinante.|  
|post_snapshot_script|**nvarchar(255)**|Especifica um ponteiro para um local de arquivo **. SQL** . O Agente de Distribuição executará o script pós-instantâneo depois que todos os outros scripts de objeto replicado tentam sido aplicados durante uma sincronização inicial.|  
|compress_snapshot|**bit**|Especifica que o instantâneo gravado no local de *alt_snapshot_folder* deve ser compactado no [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato CAB. **0** especifica que o instantâneo não será compactado.|  
|ftp_address|**sysname**|O endereço de rede do serviço FTP para o Distribuidor. Especifica onde os arquivos de instantâneo de publicação ficam localizados para serem captados pelo Agente de Distribuição ou por um Assinante.|  
|ftp_port|**int**|O número da porta do serviço FTP do Distribuidor.|  
|ftp_subdirectory|**nvarchar(255)**|Especifica onde os arquivos de instantâneo estarão disponíveis para serem retirados pelo Agente de Distribuição ou Agente de Mesclagem do Assinante se a publicação oferecer suporte à propagação de instantâneo usando o FTP.  |  
|ftp_login|**sysname**|O nome de usuário usado para se conectar ao serviço FTP.|  
|allow_dts|**bit**|Especifica que a publicação permite transformações de dados. **0** especifica que as transformações DTS não são permitidas.|  
|allow_subscription_copy|**bit**|Especifica se a capacidade para copiar os bancos de dados de assinatura que assinam esta publicação foi habilitada. **0** significa que a cópia não é permitida.|  
|centralized_conflicts|**bit**|Especifica se registros de conflito são ou não armazenados no Publicador:<br /><br /> **0** = registros de conflitos são armazenados no Publicador e no Assinante que causou o conflito.<br /><br /> **1** = registros de conflitos são armazenados no Publicador.|  
|conflict_retention|**int**|Especifica o período de retenção de conflito, em dias.|  
|conflict_policy|**int**|Especifica a política de resolução de conflito seguida quando a opção de assinante de atualização enfileirado é usada. Pode ser um destes valores:<br /><br /> **1** = o Publicador vence o conflito.<br /><br /> **2** = Assinante vence o conflito.<br /><br /> **3** = a assinatura é reinicializada.|  
|queue_type||Especifica o tipo de fila usado. Pode ser um destes valores:<br /><br /> **MSMQ** = usar o [!INCLUDE[msCoName](../../includes/msconame-md.md)] enfileiramento de mensagens para armazenar transações.<br /><br /> **SQL** = use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para armazenar transações.<br /><br /> Observação: o suporte para enfileiramento de mensagens foi descontinuado.|  
|backward_comp_level||O nível de compatibilidade do banco de dados, podendo ser um dos seguintes:<br /><br /> **90**  =  90 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **100**  =  100 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|publish_to_AD|**bit**|Especifica se a publicação é publicada no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory. Um valor de **1** indica que ele é publicado e um valor de **0** indica que ele não está publicado.|  
|allow_initialize_from_backup|**bit**|Indica se os Assinantes podem iniciar uma assinatura para essa publicação de um backup em vez de um instantâneo inicial. **1** significa que as assinaturas podem ser inicializadas a partir de um backup e **0** significa que elas não podem. Para obter mais informações, consulte [inicializar uma assinatura transacional sem um](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md) assinante transacional de um instantâneo sem um instantâneo.|  
|replicate_ddl|**int**|Indica se a replicação do esquema tem suporte para a publicação. **1** indica que as instruções DDL (linguagem de definição de dados) executadas no Publicador são replicadas e **0** indica que as instruções DDL não são replicadas. Para obter mais informações, consulte [Make Schema Changes on Publication Databases](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md) (Fazer alterações de esquema em bancos de dados de publicação).|  
|enabled_for_p2p|**int**|Se a publicação pode ser usada em uma topologia de replicação ponto a ponto. **1** indica que a publicação dá suporte à replicação ponto a ponto. Para obter mais informações, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).|  
|publish_local_changes_only|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|enabled_for_het_sub|**int**|Especifica se a publicação oferece suporte a Assinantes não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um valor de **1** significa que não há [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suporte para assinantes. Um valor de **0** significa que somente os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes têm suporte. Para obter mais informações, consulte [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).|  
|enabled_for_p2p_conflictdetection|**int**|Especifica se o Agente de Distribuição detecta conflitos para uma publicação que está habilitada para replicação ponto a ponto. Um valor de **1** significa que os conflitos são detectados. Para obter mais informações, consulte [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
|originator_id|**int**|Especifica uma ID para um nó em uma topologia ponto a ponto. Essa ID será usada para detecção de conflitos se **enabled_for_p2p_conflictdetection** for definido como **1**. Para uma lista de IDs que já foram usadas, consulte a tabela do sistema [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) .|  
|p2p_continue_onconflict|**int**|Especifica se o Agente de Distribuição deve continuar processando alterações quando um conflito é detectado. Um valor de **1** significa que o agente continua a processar as alterações.<br /><br /> ** \* \* Cuidado \* é \* ** recomendável que você use o valor padrão de **0**. Quando essa opção é definida como **1**, a agente de distribuição tenta convergir dados na topologia aplicando a linha conflitante do nó que tem a ID de originador mais alta. Esse método não garante convergência. Verifique se a topologia está consistente depois que um conflito é detectado. Para obter mais informações, consulte “Controlando conflitos” em [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
|allow_partition_switch|**int**|Especifica se ALTER TABLE... As instruções SWITCH podem ser executadas no banco de dados publicado. Para obter mais informações, consulte [Replicar tabelas e índices particionados](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).|  
|replicate_partition_switch|**int**|Especifica se ALTER TABLE... As instruções SWITCH executadas no banco de dados publicado devem ser replicadas para os assinantes. Essa opção só será válida se *allow_partition_switch* estiver definida como **1**.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 sp_helppublication é usado em replicação transacional e de instantâneo.  
  
 sp_helppublication retornará informações sobre todas as publicações do usuário que executa este procedimento.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_helppublication](../../relational-databases/replication/codesnippet/tsql/sp-helppublication-trans_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros da função de servidor fixa sysadmin no Publicador ou membros da função de banco de dados fixa db_owner no banco de dados de publicação ou usuários na PAL (lista de acesso à publicação) podem executar sp_helppublication.  
  
 Para um não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador, somente membros da função de servidor fixa sysadmin no distribuidor ou membros da função de banco de dados fixa db_owner no banco de dados de distribuição ou usuários na PAL podem executar sp_helppublication.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [&#41;&#40;Transact-SQL de sp_addpublication ](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changepublication ](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_droppublication ](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
