---
title: syspublications (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- syspublications
- syspublications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspublications system table
ms.assetid: a86eb4f5-1f7b-493e-af55-3d15cf878228
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6d7fb57743726a59c0b501544802ecc7c701da20
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68029765"
---
# <a name="syspublications-transact-sql"></a>syspublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada publicação definida no banco de dados. Essa tabela é armazenada no banco de dados de publicação.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**ndescrição**|**nvarchar (255)**|A entrada descritiva para a publicação.|  
|**name**|**sysname**|O nome exclusivo associado com a publicação.|  
|**pubid**|**int**|A coluna de identidade que fornece um ID exclusivo para a publicação.|  
|**repl_freq**|**tinyint**|A frequência da replicação:<br /><br /> **0** = baseado em transação.<br /><br /> **1** = atualização de tabela agendada.|  
|**status**|**tinyint**|O status:<br /><br /> **0** = inativo.<br /><br /> **1** = ativo.|  
|**sync_method**|**tinyint**|O método de sincronização:<br /><br /> **0** =**bcp**(utilitário de programa de cópia em massa) de modo nativo.<br /><br /> **1** = bcp de modo de caractere.<br /><br /> **3** = simultâneo, o que significa que o bcp de modo nativo é usado, mas as tabelas não são bloqueadas durante o instantâneo.<br /><br /> **4** = Concurrent_c, o que significa que o bcp de modo de caractere é usado, mas as tabelas não são bloqueadas durante o instantâneo.|  
|**snapshot_jobid**|**binary(16)**|A ID da tarefa agendada.|  
|**independent_agent**|**bit**|Especifica se existe um Distribution Agent autônomo para essa publicação.<br /><br /> **0** = a publicação usa um agente de distribuição compartilhado e cada par de banco de dados/assinante do Publicador tem um agente único e compartilhado.<br /><br /> **1** = há um agente de distribuição autônomo para esta publicação.|  
|**immediate_sync**|**bit**|Indica se os arquivos de sincronização são criados ou recriados sempre que o Agente de Instantâneo é executado, em que **1** significa que eles são criados toda vez que o agente é executado.|  
|**enabled_for_internet**|**bit**|Indica se os arquivos de sincronização da publicação são expostos à Internet por meio de FTP (File Transfer Protocol) e outros serviços, em que **1** significa que eles podem ser acessados pela Internet.|  
|**allow_push**|**bit**|Indica se as assinaturas push são permitidas na publicação, em que **1** significa que elas são permitidas.|  
|**allow_pull**|**bit**|Indica se as assinaturas pull são permitidas na publicação, em que **1** significa que elas são permitidas.|  
|**allow_anonymous**|**bit**|Indica se as assinaturas anônimas são permitidas na publicação, em que **1** significa que elas são permitidas.|  
|**immediate_sync_ready**|**bit**|Indica se o instantâneo foi gerado pelo Snapshot Agent e está pronto para ser usado por novas assinaturas. Só é significativo para publicações de atualização imediata. **1** indica que o instantâneo está pronto.|  
|**allow_sync_tran**|**bit**|Especifica se as assinaturas de atualização imediata são permitidas na publicação. **1** significa que as assinaturas de atualização imediata são permitidas.|  
|**autogen_sync_procs**|**bit**|Especifica se o procedimento armazenado de sincronização para assinatura da atualização imediata é gerado no Publicador. **1** significa que ele é gerado no Publicador.|  
|**políticas**|**int**|A quantidade de alteração, em horas, a economizar para a publicação determinada.|  
|**allowed_queued_tran**|**bit**|Especifica se foi habilitado o enfileiramento de alterações no Assinante até que elas possam ser aplicadas no Publicador. Se **1**, as alterações no Assinante serão enfileiradas.|  
|**snapshot_in_defaultfolder**|**bit**|Especifica se arquivos de instantâneo são armazenados na pasta padrão.<br /><br /> **0** = arquivos de instantâneo foram armazenados no local alternativo especificado pelo *alternate_snapshot_folder*.<br /><br /> **1** = arquivos de instantâneo podem ser encontrados na pasta padrão.|  
|**alt_snapshot_folder**|**nvarchar (255)**|Especifica o local da pasta alternativa para o instantâneo.|  
|**pre_snapshot_script**|**nvarchar (255)**|Especifica um ponteiro para um local de arquivo **. SQL** . O Distribution Agent executará o script pré-instantâneo antes de executar qualquer script de objeto replicado, ao aplicar um instantâneo no Assinante.|  
|**post_snapshot_script**|**nvarchar (255)**|Especifica um ponteiro para um local de arquivo **. SQL** . O Distribution Agent executará o script pós-instantâneo depois que todos os outros scripts de objeto replicado tiverem sido aplicados durante uma sincronização inicial.|  
|**compress_snapshot**|**bit**|Especifica que o instantâneo gravado no local de *alt_snapshot_folder* deve ser compactado no formato [!INCLUDE[msCoName](../../includes/msconame-md.md)] cab. **1** significa que o instantâneo será compactado.|  
|**ftp_address**|**sysname**|O endereço de rede do serviço FTP para o Distribuidor. Especifica onde arquivos de instantâneo de publicação ficam localizados para serem retirados pelo Distribution Agent.|  
|**ftp_port**|**int**|O número da porta do serviço FTP do Distribuidor. Especifica onde os arquivos de instantâneo de publicação estão localizados para serem retirados pelo Distribution Agent.|  
|**ftp_subdirectory**|**nvarchar (255)**|Especifica onde os arquivos de instantâneo estarão disponíveis para a Agente de Distribuição a serem coletadas se a publicação der suporte à propagação de instantâneos usando FTP.|  
|**ftp_login**|**sysname**|O nome de usuário usado para se conectar ao serviço FTP.|  
|**ftp_password**|**nvarchar (524)**|A senha de usuário usada para se conectar ao serviço FTP.|  
|**allow_dts**|**bit**|Especifica se a publicação permite transformações de dados. **1** especifica que as transformações DTS são permitidas.|  
|**allow_subscription_copy**|**bit**|Especifica se a capacidade para copiar os bancos de dados de assinatura que assinam esta publicação foi habilitada. **1** significa que a cópia é permitida.|  
|**centralized_conflicts**|**bit**|Especifica se registros de conflito são ou não armazenados no Publicador:<br /><br /> **0** = registros de conflitos são armazenados no Publicador e no Assinante que causou o conflito.<br /><br /> **1** = registros de conflitos são armazenados no Publicador.|  
|**conflict_retention**|**int**|Especifica o período de retenção de conflito, em dias.|  
|**conflict_policy**|**int**|Especifica a política de resolução de conflito seguida quando a opção de assinante de atualização enfileirado é usada. Pode ser um destes valores:<br /><br /> **1** = o Publicador vence o conflito.<br /><br /> **2** = Assinante vence o conflito.<br /><br /> **3** = a assinatura é reinicializada.|  
|**queue_type**|**int**|Especifica o tipo de fila usado. Pode ser um destes valores:<br /><br /> **1** = MSMQ, que usa [!INCLUDE[msCoName](../../includes/msconame-md.md)] o enfileiramento de mensagens para armazenar transações.<br /><br /> **2** = SQL, que usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para armazenar transações.<br /><br /> Observação: o [!INCLUDE[msCoName](../../includes/msconame-md.md)] uso do enfileiramento de mensagens foi preterido e não está mais disponível.|  
|**ad_guidname**|**sysname**|Especifica se a publicação é publicada no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory. Um GUID (identificador global exclusivo) válido especifica que a publicação é publicada no Active Directory e o GUID é o **objectGUID**do objeto de publicação Active Directory correspondente. Se for NULL, a publicação não será publicada no Active Directory.|  
|**backward_comp_level**|**int**|Nível de compatibilidade de banco de dados, que pode ser um dos valores seguintes:<br /><br /> **90** = 90[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].<br /><br /> **100** = 100[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].<br /><br /> **110** = 110[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].<br /><br /> **120** = 120[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].|  
|**allow_initialize_from_backup**|**bit**|Indica se os assinantes podem inicializar uma assinatura para esta publicação a partir de um backup em vez de um instantâneo inicial. **1** significa que as assinaturas podem ser inicializadas a partir de um backup e **0** significa que elas não podem. Para obter mais informações, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).|  
|**min_autonosync_lsn**|**binary**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**replicate_ddl**|**int**|Indica se replicação de esquema tem suporte para a publicação. **1** indica que as instruções DDL (linguagem de definição de dados) executadas no Publicador são replicadas e **0** indica que as instruções DDL não são replicadas. Para obter mais informações, consulte [Make Schema Changes on Publication Databases](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md) (Fazer alterações de esquema em bancos de dados de publicação).|  
|**options**|**int**|Um bitmap que especifica opções de publicação adicionais, onde os valores de opção bit a bit são os seguintes:<br /><br /> **0x1** -habilitado para replicação ponto a ponto.<br /><br /> **0x2** -publicar apenas alterações locais para replicação ponto a ponto.<br /><br /> **0x4** -habilitado para[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes não.<br /><br /> **0x8** -habilitado para detecção de conflitos ponto a ponto.|  
|**originator_id**|**smallint**|Identifica cada nó em uma topologia de replicação ponto a ponto com a finalidade de detecção de conflito. Para obter mais informações, consulte [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)  
  
  
