---
title: sp_helppublication (Transact-SQL) | Microsoft Docs
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
- sp_helppublication_TSQL
- sp_helppublication
helpviewer_keywords:
- sp_helppublication
ms.assetid: e801c3f0-dcbd-4b4a-b254-949a05f63518
caps.latest.revision: 49
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 532c1d371596cff80a547414a316ed0ec401728a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sphelppublication-transact-sql"></a>sp_helppublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre uma publicação. Para uma [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicação, esse procedimento armazenado é executado no publicador do banco de dados de publicação. Para uma publicação Oracle, esse procedimento armazenado é executado no Distribuidor, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helppublication [ [ @publication = ] 'publication' ]  
    [ , [ @found=] found OUTPUT]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication =** ] **'***publicação***'**  
 É o nome da publicação a ser exibida. *publicação* é sysname, com um padrão de **%**, que retorna informações sobre todas as publicações.  
  
 [  **@found =** ] **'***encontrado***'** saída  
 É um sinalizador para indicar linhas de retorno. *encontrado*é **int** e um parâmetro de saída, com um padrão de **23456**. **1** indica que a publicação foi localizada. **0** indica a publicação não foi encontrada.  
  
 [ **@publisher** =] **'***publicador***'**  
 Especifica um publicador que não é do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *publicador* é sysname, com um padrão NULL.  
  
> [!NOTE]  
>  *publicador* não deve ser especificado ao solicitar informações da publicação de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|pubid|**Int**|ID da publicação.|  
|nome|**sysname**|Nome da publicação.|  
|restrito|**Int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|status|**tinyint**|O status atual da publicação.<br /><br /> **0** = inativo.<br /><br /> **1** = ativo.|  
|tarefa||Usado para compatibilidade com versões anteriores.|  
|frequência de replicação|**tinyint**|Tipo de frequência de replicação:<br /><br /> **0** = transacional<br /><br /> **1** = instantâneo|  
|método de sincronização|**tinyint**|Modo de sincronização:<br /><br /> **0** = programa de cópia em massa (**bcp** utilitário)<br /><br /> **1** = cópia em massa de caracteres<br /><br /> **3** = simultâneo, o que significa que essa cópia em massa (**bcp**utilitário) é usado, mas tabelas não são bloqueadas durante o instantâneo<br /><br /> **4** = Concurrent_c, o que significa que a cópia em massa de caracteres é usada mas tabelas não são bloqueadas durante o instantâneo|  
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
|retenção|**Int**|A quantidade de alteração, em horas, a ser salva para a publicação determinada.|  
|has subscription|**bit**|Se a publicação tem assinatura ativas. **1** significa que a publicação tem assinaturas ativas, e **0** significa que a publicação não tem assinaturas.|  
|allow_queued_tran|**bit**|Especifica se o serviço de enfileiramento de alterações no Assinante foi desabilitado até que possam ser aplicadas no Publicador. Se **0**, as alterações no assinante não serão enfileiradas.|  
|snapshot_in_defaultfolder|**bit**|Especifica se arquivos de instantâneo são armazenados na pasta padrão. Se **0**, arquivos de instantâneo foram armazenados no local alternativo especificado por *alternate_snapshot_folder*. Se **1**, arquivos de instantâneo podem ser encontrados na pasta padrão.|  
|alt_snapshot_folder|**nvarchar(255)**|Especifica o local da pasta alternativa para o instantâneo.|  
|pre_snapshot_script|**nvarchar(255)**|Especifica um ponteiro para um **. SQL** local do arquivo. O Agente de Distribuição executará o script pré-instantâneo antes de executar qualquer script de objeto replicado, ao aplicar um instantâneo no Assinante.|  
|post_snapshot_script|**nvarchar(255)**|Especifica um ponteiro para um **. SQL** local do arquivo. O Agente de Distribuição executará o script pós-instantâneo depois que todos os outros scripts de objeto replicado tentam sido aplicados durante uma sincronização inicial.|  
|compress_snapshot|**bit**|Especifica que o instantâneo foi criado para o *alt_snapshot_folder* local é compactado no [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato CAB. **0** Especifica que o instantâneo não será compactado.|  
|ftp_address|**sysname**|O endereço de rede do serviço FTP para o Distribuidor. Especifica onde os arquivos de instantâneo de publicação ficam localizados para serem captados pelo Agente de Distribuição ou por um Assinante.|  
|ftp_port|**Int**|O número da porta do serviço FTP do Distribuidor.|  
|ftp_subdirectory|**nvarchar(255)**|Especifica onde os arquivos de instantâneo estarão disponíveis para serem retirados pelo Agente de Distribuição ou Agente de Mesclagem do Assinante se a publicação oferecer suporte à propagação de instantâneo usando o FTP.  |  
|ftp_login|**sysname**|O nome de usuário usado para se conectar ao serviço FTP.|  
|allow_dts|**bit**|Especifica que a publicação permite transformações de dados. **0** Especifica que transformações DTS não são permitidas.|  
|allow_subscription_copy|**bit**|Especifica se a capacidade para copiar os bancos de dados de assinatura que assinam esta publicação foi habilitada. **0** significa que não é permitido copiar.|  
|centralized_conflicts|**bit**|Especifica se registros de conflito são ou não armazenados no Publicador:<br /><br /> **0** = registros de conflito são armazenados no publicador e no assinante que causou o conflito.<br /><br /> **1** = registros de conflito são armazenados no publicador.|  
|conflict_retention|**Int**|Especifica o período de retenção de conflito, em dias.|  
|conflict_policy|**Int**|Especifica a política de resolução de conflito seguida quando a opção de assinante de atualização enfileirado é usada. Pode ser um destes valores:<br /><br /> **1** = o publicador vence o conflito.<br /><br /> **2** = o assinante vence o conflito.<br /><br /> **3** = assinatura for reinicializada.|  
|queue_type||Especifica o tipo de fila usado. Pode ser um destes valores:<br /><br /> **MSMQ** = usar [!INCLUDE[msCoName](../../includes/msconame-md.md)] enfileiramento de mensagens para armazenar transações.<br /><br /> **SQL** = usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para armazenar transações.<br /><br /> Observação: Suporte para enfileiramento de mensagens foi descontinuado.|  
|backward_comp_level||O nível de compatibilidade do banco de dados, podendo ser um dos seguintes:<br /><br /> **90** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **100** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|publish_to_AD|**bit**|Especifica se a publicação é publicada no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory™. Um valor de **1** indica que ele é publicado e um valor de **0** indica que não é publicado.|  
|allow_initialize_from_backup|**bit**|Indica se os Assinantes podem iniciar uma assinatura para essa publicação de um backup em vez de um instantâneo inicial. **1** significa que as assinaturas podem ser inicializadas de um backup, e **0** significa que eles não podem. Para obter mais informações, consulte [inicializar um transacional assinatura sem um instantâneo](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md) um assinante transacional sem um instantâneo.|  
|replicate_ddl|**Int**|Indica se a replicação de esquema tem suporte para a publicação. **1** indica que instruções de DDL (linguagem) de definição de dados executadas no publicador são replicadas e **0** indica que instruções DDL não são replicadas. Para obter mais informações, consulte [Make Schema Changes on Publication Databases](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md) (Fazer alterações de esquema em bancos de dados de publicação).|  
|enabled_for_p2p|**Int**|Se a publicação pode ser usada em uma topologia de replicação ponto a ponto. **1** indica que a publicação oferece suporte a replicação ponto a ponto. Para obter mais informações, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).|  
|publish_local_changes_only|**Int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|enabled_for_het_sub|**Int**|Especifica se a publicação oferece suporte a Assinantes não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um valor de **1** significa que não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] há suporte para assinantes. Um valor de **0** significa que somente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] há suporte para assinantes. Para obter mais informações, consulte [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).|  
|enabled_for_p2p_conflictdetection|**Int**|Especifica se o Agente de Distribuição detecta conflitos para uma publicação que está habilitada para replicação ponto a ponto. Um valor de **1** significa que os conflitos são detectados. Para obter mais informações, consulte [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
|originator_id|**Int**|Especifica uma ID para um nó em uma topologia ponto a ponto. Essa ID é usada para detecção de conflitos se **enabled_for_p2p_conflictdetection** é definido como **1**. Para uma lista de IDs que já foram usadas, consulte a tabela do sistema [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) .|  
|p2p_continue_onconflict|**Int**|Especifica se o Agente de Distribuição deve continuar processando alterações quando um conflito é detectado. Um valor de **1** significa que o agente continua processando alterações.<br /><br /> **\*\* Cuidado \* \***  é recomendável que você use o valor padrão de **0**. Quando essa opção é definida como **1**, o Distribution Agent tenta convergir os dados na topologia aplicando a linha conflitante do nó que tem o maior ID de originador. Esse método não garante convergência. Verifique se a topologia está consistente depois que um conflito é detectado. Para obter mais informações, consulte “Controlando conflitos” em [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
|alllow_partition_switch|**Int**|Especifica se as instruções ALTER TABLE…SWITCH podem ser executadas no banco de dados publicado. Para obter mais informações, consulte [Replicar tabelas e índices particionados](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).|  
|replicate_partition_switch|**Int**|Especifica se as instruções ALTER TABLE…SWITCH que são executadas no banco de dados publicado devem ser replicadas para Assinantes. Essa opção é válida somente se *allow_partition_switch* é definido como **1**.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 sp_helppublication é usado em replicação transacional e de instantâneo.  
  
 sp_helppublication retornará informações sobre todas as publicações do usuário que executa este procedimento.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_helppublication](../../relational-databases/replication/codesnippet/tsql/sp-helppublication-trans_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros da função de servidor fixa sysadmin no Publicador ou membros da função de banco de dados fixa db_owner no banco de dados de publicação ou usuários na PAL (lista de acesso à publicação) podem executar sp_helppublication.  
  
 Para um Publicador não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], somente membros da função de servidor fixa sysadmin no Distribuidor ou membros da função de banco de dados fixa db_owner no banco de dados de distribuição ou usuários da PAL podem executar sp_helppublication.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_droppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
