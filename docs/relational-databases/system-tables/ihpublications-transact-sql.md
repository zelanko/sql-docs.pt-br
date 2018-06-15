---
title: IHpublications (Transact-SQL) | Microsoft Docs
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
- IHpublications_TSQL
- IHpublications
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublications system table
ms.assetid: b519a101-fa53-44be-bd55-6ea79245b5d1
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 0bf90e755f3ba467882cfcf5f9602b1c6a607444
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33003403"
---
# <a name="ihpublications-transact-sql"></a>IHpublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **IHpublications** tabela do sistema contém uma linha para cada publicação não SQL Server usando o distribuidor atual. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**pubid**|**Int**|A coluna de identidade que fornece um ID exclusivo para a publicação.|  
|**name**|**sysname**|O nome exclusivo associado com a publicação.|  
|**repl_freq**|**tinyint**|A frequência da replicação:<br /><br /> **0** = a transação com base.<br /><br /> **1** = atualização de tabela agendada.|  
|**status**|**tinyint**|O status da publicação, que pode ser um dos seguintes:<br /><br /> **0** = inativo.<br /><br /> **1** = ativo.|  
|**sync_method**|**tinyint**|O método de sincronização:<br /><br /> **1** = cópia em massa de caracteres.<br /><br /> **4** = Concurrent_c, o que significa que a cópia em massa de caracteres é usada mas tabelas não são bloqueadas durante o instantâneo.|  
|**snapshot_jobid**|**binary**|A ID da tarefa agendada.|  
|**enabled_for_internet**|**bit**|Indica se os arquivos de sincronização para a publicação são expostos à Internet através de FTP e outros serviços, onde **1** significa que eles podem ser acessados pela Internet.|  
|**immediate_sync_ready**|**bit**|Indica se os arquivos de sincronização estão disponíveis, onde **1** significa que elas estão disponíveis. *Não tem suporte para Publicadores não SQL.*|  
|**allow_queued_tran**|**bit**|Especifica se foi habilitado o enfileiramento de alterações no Assinante até que elas possam ser aplicadas no Publicador. Se **1**, as alterações no assinante serão enfileiradas. *Não tem suporte para Publicadores não SQL.*|  
|**allow_sync_tran**|**bit**|Especifica se são permitidas assinaturas de atualização imediata na publicação. **1** significa que as assinaturas de atualização imediata são permitidas. *Não tem suporte para Publicadores não SQL.*|  
|**autogen_sync_procs**|**bit**|Especifica se o procedimento armazenado de sincronização para assinatura da atualização imediata é gerado no Publicador. **1** significa que é gerado no publicador. *Não tem suporte para Publicadores não SQL.*|  
|**snapshot_in_defaultfolder**|**bit**|Especifica se arquivos de instantâneo são armazenados na pasta padrão. Se **0**, arquivos de instantâneo foram armazenados no local alternativo especificado por *alternate_snapshot_folder*. Se **1**, arquivos de instantâneo podem ser encontrados na pasta padrão.|  
|**alt_snapshot_folder**|**nvarchar(510)**|Especifica o local da pasta alternativa para o instantâneo.|  
|**pre_snapshot_script**|**nvarchar(510)**|Especifica um ponteiro para um **. SQL** local do arquivo. O Distribution Agent executará o script pré-instantâneo antes de executar qualquer script de objeto replicado, ao aplicar um instantâneo no Assinante.|  
|**post_snapshot_script**|**nvarchar(510)**|Especifica um ponteiro para um **. SQL** local do arquivo. O Distribution Agent executará o script pós-instantâneo depois que todos os outros scripts de objeto replicado tiverem sido aplicados durante uma sincronização inicial.|  
|**compress_snapshot**|**bit**|Especifica que o instantâneo foi criado para o *alt_snapshot_folder* local é compactado no [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato CAB. **0** Especifica que o instantâneo não será compactado.|  
|**ftp_address**|**sysname**|O endereço de rede do serviço FTP para o Distribuidor. Especifica onde arquivos de instantâneo de publicação ficam localizados para serem retirados pelo Distribution Agent.|  
|**ftp_port**|**Int**|O número da porta do serviço FTP do Distribuidor. Especifica onde os arquivos de instantâneo de publicação estão localizados para serem retirados pelo Distribution Agent.|  
|**ftp_subdirectory**|**nvarchar(510)**|Especifica onde os arquivos de instantâneo estarão disponíveis para serem retirados pelo Distribution Agent se a publicação oferecer suporte a arquivos de propagação usando o FTP.|  
|**ftp_login**|**nvarchar(256)**|O nome de usuário usado para se conectar ao serviço FTP.|  
|**ftp_password**|**nvarchar(1048)**|A senha de usuário usada para se conectar ao serviço FTP.|  
|**allow_dts**|**bit**|Especifica que a publicação permite transformações de dados. **1** Especifica que transformações DTS são permitidas. *Não tem suporte para Publicadores não SQL.*|  
|**allow_anonymous**|**bit**|Indica se são permitidas assinaturas anônimas na publicação, onde **1** significa que elas são permitidas.|  
|**centralized_conflicts**|**bit**|Especifica se registros de conflito são ou não armazenados no Publicador:<br /><br /> **0** = registros de conflito são armazenados no publicador e no assinante que causou o conflito.<br /><br /> **1** = registros de conflito são armazenados no publicador.<br /><br /> *Não tem suporte para Publicadores não SQL.*|  
|**conflict_retention**|**Int**|Especifica o período de retenção de conflito, em dias. *Não tem suporte para Publicadores não SQL.*|  
|**conflict_policy**|**Int**|Especifica a política de resolução de conflito seguida quando a opção de assinante de atualização enfileirado é usada. Pode ser um destes valores:<br /><br /> **1** = o publicador vence o conflito.<br /><br /> **2** = o assinante vence o conflito.<br /><br /> **3** = assinatura for reinicializada.<br /><br /> *Não tem suporte para Publicadores não SQL.*|  
|**queue_type**|**Int**|Especifica o tipo de fila usado. Pode ser um destes valores:<br /><br /> **1** = msmq, que usa [!INCLUDE[msCoName](../../includes/msconame-md.md)] enfileiramento de mensagens para armazenar transações.<br /><br /> **2** = sql, que usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para armazenar transações.<br /><br /> Esta coluna não é usada por não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] editores.<br /><br /> Observação: Usando [!INCLUDE[msCoName](../../includes/msconame-md.md)] enfileiramento de mensagens foi preterido e não é mais suportado.<br /><br /> *Esta coluna não há suporte para Publicadores não SQL.*|  
|**ad_guidname**|**sysname**|Especifica se a publicação é publicada no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory. Um identificador válido globalmente exclusivo (GUID) Especifica que a publicação é publicada no [!INCLUDE[msCoName](../../includes/msconame-md.md)] do Active Directory e o GUID é o objeto de publicação do Active Directory correspondente **objectGUID**. Se for NULL, a publicação não será publicada no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory. *Não tem suporte para Publicadores não SQL.*|  
|**backward_comp_level**|**Int**|Nível de compatibilidade de banco de dados, que pode ser um dos valores seguintes:<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].<br /><br /> *Não tem suporte para Publicadores não SQL.*|  
|**Descrição**|**nvarchar(255)**|Entrada descritiva para a publicação.|  
|**independent_agent**|**bit**|Especifica se existe um Distribution Agent autônomo para essa publicação.<br /><br /> **0** = a publicação usa um Distribution Agent compartilhado e cada par de banco de dados do publicador/assinante tem um agente compartilhado, único.<br /><br /> **1** = há um Distribution Agent autônomo para essa publicação.|  
|**immediate_sync**|**bit**|Indica se os arquivos de sincronização são criados ou recriados cada vez que o Snapshot Agent é executado, onde **1** significa que eles são criados toda vez que o agente é executado.|  
|**allow_push**|**bit**|Indica se são permitidas assinaturas push na publicação, onde **1** significa que elas são permitidas.|  
|**allow_pull**|**bit**|Indica se são permitidas assinaturas pull na publicação, onde **1** significa que elas são permitidas.|  
|**retention**|**Int**|A quantidade de alteração, em horas, a economizar para a publicação determinada.|  
|**allow_subscription_copy**|**bit**|Especifica se a capacidade para copiar os bancos de dados de assinatura que assinam esta publicação foi habilitada. **1** significa que é permitido copiar.|  
|**allow_initialize_from_backup**|**bit**|Indica se os Assinantes podem iniciar uma assinatura para essa publicação de um backup em vez de um instantâneo inicial. **1** significa que as assinaturas podem ser inicializadas de um backup, e **0** significa que eles não podem. Para obter mais informações, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md). *Não tem suporte para Publicadores não SQL.*|  
|**min_autonosync_lsn**|**binary(1)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**replicate_ddl**|**Int**|Indica se a replicação de esquema tem suporte para a publicação. **1** indica que instruções DDL executadas no publicador são replicadas e **0** indica que instruções DDL não são replicadas. Para obter mais informações, consulte [Make Schema Changes on Publication Databases](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md) (Fazer alterações de esquema em bancos de dados de publicação). *Não tem suporte para Publicadores não SQL.*|  
|**Opções**|**Int**|Bitmap que especifica opções de publicação adicionais, onde os valores de opção bit a bit são:<br /><br /> **0x1** - habilitado para replicação ponto a ponto.<br /><br /> **0x2** -publicar somente alterações locais.<br /><br /> **0x4** - habilitado para assinantes não SQL Server.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [syspublications &#40;exibição do sistema&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/syspublications-system-view-transact-sql.md)   
 [syspublications &#40;Transact-SQL&#41;](../../relational-databases/system-tables/syspublications-transact-sql.md)  
  
  
