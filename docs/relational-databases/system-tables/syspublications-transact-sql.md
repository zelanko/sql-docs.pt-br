---
title: syspublications (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- syspublications
- syspublications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspublications system table
ms.assetid: a86eb4f5-1f7b-493e-af55-3d15cf878228
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ec8c1f12755afa1a12e4e28c9f84c2f21963fc9f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="syspublications-transact-sql"></a>syspublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada publicação definida no banco de dados. Essa tabela é armazenada no banco de dados de publicação.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**Descrição**|**nvarchar(255)**|A entrada descritiva para a publicação.|  
|**name**|**sysname**|O nome exclusivo associado com a publicação.|  
|**pubid**|**Int**|A coluna de identidade que fornece um ID exclusivo para a publicação.|  
|**repl_freq**|**tinyint**|A frequência da replicação:<br /><br /> **0** = a transação com base.<br /><br /> **1** = atualização de tabela agendada.|  
|**status**|**tinyint**|O status:<br /><br /> **0** = inativo.<br /><br /> **1** = ativo.|  
|**sync_method**|**tinyint**|O método de sincronização:<br /><br /> **0** = utilitário de programa de cópia em massa de modo nativo (**BCP**).<br /><br /> **1** = BCP de modo de caractere.<br /><br /> **3** = simultâneo, o que significa que BCP de modo nativo é usado, mas as tabelas não são bloqueadas durante o instantâneo.<br /><br /> **4** = Concurrent_c, o que significa que BCP de modo de caractere é usado, mas tabelas não são bloqueadas durante o instantâneo.|  
|**snapshot_jobid**|**binary(16)**|A ID da tarefa agendada.|  
|**independent_agent**|**bit**|Especifica se existe um Distribution Agent autônomo para essa publicação.<br /><br /> **0** = a publicação usa um Distribution Agent compartilhado e cada par de banco de dados do publicador/assinante tem um agente compartilhado, único.<br /><br /> **1** = há um Distribution Agent autônomo para essa publicação.|  
|**immediate_sync**|**bit**|Indica se os arquivos de sincronização são criados ou recriados cada vez que o Snapshot Agent é executado, onde **1** significa que eles são criados toda vez que o agente é executado.|  
|**enabled_for_internet**|**bit**|Indica se os arquivos de sincronização para a publicação são expostos à Internet por meio do protocolo de transferência de arquivo (FTP) e outros serviços, onde **1** significa que eles podem ser acessados pela Internet.|  
|**allow_push**|**bit**|Indica se são permitidas assinaturas push na publicação, onde **1** significa que elas são permitidas.|  
|**allow_pull**|**bit**|Indica se são permitidas assinaturas pull na publicação, onde **1** significa que elas são permitidas.|  
|**allow_anonymous**|**bit**|Indica se são permitidas assinaturas anônimas na publicação, onde **1** significa que elas são permitidas.|  
|**immediate_sync_ready**|**bit**|Indica se o instantâneo foi gerado pelo Snapshot Agent e está pronto para ser usado por novas assinaturas. Só é significativo para publicações de atualização imediata. **1** indica que o instantâneo está pronto.|  
|**allow_sync_tran**|**bit**|Especifica se são permitidas assinaturas de atualização imediata na publicação. **1** significa que as assinaturas de atualização imediata são permitidas.|  
|**autogen_sync_procs**|**bit**|Especifica se o procedimento armazenado de sincronização para assinatura da atualização imediata é gerado no Publicador. **1** significa que é gerado no publicador.|  
|**retention**|**Int**|A quantidade de alteração, em horas, a economizar para a publicação determinada.|  
|**allowed_queued_tran**|**bit**|Especifica se foi habilitado o enfileiramento de alterações no Assinante até que elas possam ser aplicadas no Publicador. Se **1**, as alterações no assinante serão enfileiradas.|  
|**snapshot_in_defaultfolder**|**bit**|Especifica se arquivos de instantâneo são armazenados na pasta padrão.<br /><br /> **0** = instantâneo arquivos foram armazenados no local alternativo especificado por *alternate_snapshot_folder*.<br /><br /> **1** = instantâneo arquivos podem ser encontrados na pasta padrão.|  
|**alt_snapshot_folder**|**nvarchar(255)**|Especifica o local da pasta alternativa para o instantâneo.|  
|**pre_snapshot_script**|**nvarchar(255)**|Especifica um ponteiro para um **. SQL** local do arquivo. O Distribution Agent executará o script pré-instantâneo antes de executar qualquer script de objeto replicado, ao aplicar um instantâneo no Assinante.|  
|**post_snapshot_script**|**nvarchar(255)**|Especifica um ponteiro para um **. SQL** local do arquivo. O Distribution Agent executará o script pós-instantâneo depois que todos os outros scripts de objeto replicado tiverem sido aplicados durante uma sincronização inicial.|  
|**compress_snapshot**|**bit**|Especifica que o instantâneo foi criado para o *alt_snapshot_folder* local é compactado no [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato CAB. **1** significa que o instantâneo será compactado.|  
|**ftp_address**|**sysname**|O endereço de rede do serviço FTP para o Distribuidor. Especifica onde arquivos de instantâneo de publicação ficam localizados para serem retirados pelo Distribution Agent.|  
|**ftp_port**|**Int**|O número da porta do serviço FTP do Distribuidor. Especifica onde os arquivos de instantâneo de publicação estão localizados para serem retirados pelo Distribution Agent.|  
|**ftp_subdirectory**|**nvarchar(255)**|Especifica onde os arquivos de instantâneo estarão disponíveis para o Distribution Agent acompanhar se a publicação oferece suporte à propagação de instantâneo usando FTP.|  
|**ftp_login**|**sysname**|O nome de usuário usado para se conectar ao serviço FTP.|  
|**ftp_password**|**nvarchar (524)**|A senha de usuário usada para se conectar ao serviço FTP.|  
|**allow_dts**|**bit**|Especifica se a publicação permite transformações de dados. **1** Especifica que transformações DTS são permitidas.|  
|**allow_subscription_copy**|**bit**|Especifica se a capacidade para copiar os bancos de dados de assinatura que assinam esta publicação foi habilitada. **1** significa que é permitido copiar.|  
|**centralized_conflicts**|**bit**|Especifica se registros de conflito são ou não armazenados no Publicador:<br /><br /> **0** = registros de conflito são armazenados no publicador e no assinante que causou o conflito.<br /><br /> **1** = registros de conflito são armazenados no publicador.|  
|**conflict_retention**|**Int**|Especifica o período de retenção de conflito, em dias.|  
|**conflict_policy**|**Int**|Especifica a política de resolução de conflito seguida quando a opção de assinante de atualização enfileirado é usada. Pode ser um destes valores:<br /><br /> **1** = o publicador vence o conflito.<br /><br /> **2** = o assinante vence o conflito.<br /><br /> **3** = assinatura for reinicializada.|  
|**queue_type**|**Int**|Especifica o tipo de fila usado. Pode ser um destes valores:<br /><br /> **1** = msmq, que usa [!INCLUDE[msCoName](../../includes/msconame-md.md)] enfileiramento de mensagens para armazenar transações.<br /><br /> **2** = sql, que usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para armazenar transações.<br /><br /> Observação: Usando [!INCLUDE[msCoName](../../includes/msconame-md.md)] enfileiramento de mensagens foi preterido e não está mais disponível.|  
|**ad_guidname**|**sysname**|Especifica se a publicação é publicada no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory. Um identificador válido globalmente exclusivo (GUID) Especifica que a publicação é publicada no Active Directory e o GUID é o objeto de publicação do Active Directory correspondente **objectGUID**. Se for NULL, a publicação não será publicada no Active Directory.|  
|**backward_comp_level**|**Int**|Nível de compatibilidade de banco de dados, que pode ser um dos valores seguintes:<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].<br /><br /> **110** = [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].<br /><br /> **120** = [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].|  
|**allow_initialize_from_backup**|**bit**|Indica se os assinantes podem iniciar uma assinatura para esta publicação de um backup em vez de um instantâneo inicial. **1** significa que as assinaturas podem ser inicializadas de um backup, e **0** significa que eles não podem. Para obter mais informações, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).|  
|**min_autonosync_lsn**|**binary**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**replicate_ddl**|**Int**|Indica se replicação de esquema tem suporte para a publicação. **1** indica que instruções de DDL (linguagem) de definição de dados executadas no publicador são replicadas e **0** indica que instruções DDL não são replicadas. Para obter mais informações, consulte [Make Schema Changes on Publication Databases](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md) (Fazer alterações de esquema em bancos de dados de publicação).|  
|**Opções**|**Int**|Um bitmap que especifica opções de publicação adicionais, onde os valores de opção bit a bit são os seguintes:<br /><br /> **0x1** - habilitado para replicação ponto a ponto.<br /><br /> **0x2** -publicar somente alterações locais para replicação ponto a ponto.<br /><br /> **0x4** - habilitado para não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes.<br /><br /> **0x8** - habilitado para detecção de conflitos ponto a ponto.|  
|**originator_id**|**smallint**|Identifica cada nó em uma topologia de replicação ponto a ponto com a finalidade de detecção de conflito. Para obter mais informações, consulte [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)  
  
  
