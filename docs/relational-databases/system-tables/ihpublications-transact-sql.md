---
title: IHpublications (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublications_TSQL
- IHpublications
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublications system table
ms.assetid: b519a101-fa53-44be-bd55-6ea79245b5d1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a8185249a40c11a031be8206a4a1ea016ed50faa
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85764240"
---
# <a name="ihpublications-transact-sql"></a>IHpublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  A tabela do sistema **IHpublications** contém uma linha para cada publicação não SQL Server usando o distribuidor atual. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**pubid**|**int**|A coluna de identidade que fornece um ID exclusivo para a publicação.|  
|**name**|**sysname**|O nome exclusivo associado com a publicação.|  
|**repl_freq**|**tinyint**|A frequência da replicação:<br /><br /> **0** = baseado em transação.<br /><br /> **1** = atualização de tabela agendada.|  
|**status**|**tinyint**|O status da publicação, que pode ser um dos seguintes:<br /><br /> **0** = inativo.<br /><br /> **1** = ativo.|  
|**sync_method**|**tinyint**|O método de sincronização:<br /><br /> **1** = cópia em massa de caractere.<br /><br /> **4** = Concurrent_c, o que significa que a cópia em massa de caracteres é usada, mas as tabelas não são bloqueadas durante o instantâneo.|  
|**snapshot_jobid**|**binary**|A ID da tarefa agendada.|  
|**enabled_for_internet**|**bit**|Indica se os arquivos de sincronização da publicação estão expostos à Internet por FTP e outros serviços, em que **1** significa que eles podem ser acessados pela Internet.|  
|**immediate_sync_ready**|**bit**|Indica se os arquivos de sincronização estão disponíveis, em que **1** significa que eles estão disponíveis. *Sem suporte para Publicadores não SQL.*|  
|**allow_queued_tran**|**bit**|Especifica se foi habilitado o enfileiramento de alterações no Assinante até que elas possam ser aplicadas no Publicador. Se **1**, as alterações no Assinante serão enfileiradas. *Sem suporte para Publicadores não SQL.*|  
|**allow_sync_tran**|**bit**|Especifica se as assinaturas de atualização imediata são permitidas na publicação. **1** significa que as assinaturas de atualização imediata são permitidas. *Sem suporte para Publicadores não SQL.*|  
|**autogen_sync_procs**|**bit**|Especifica se o procedimento armazenado de sincronização para assinatura da atualização imediata é gerado no Publicador. **1** significa que ele é gerado no Publicador. *Sem suporte para Publicadores não SQL.*|  
|**snapshot_in_defaultfolder**|**bit**|Especifica se arquivos de instantâneo são armazenados na pasta padrão. Se **0**, os arquivos de instantâneo foram armazenados no local alternativo especificado pelo *alternate_snapshot_folder*. Se **1**, os arquivos de instantâneo podem ser encontrados na pasta padrão.|  
|**alt_snapshot_folder**|**nvarchar (510)**|Especifica o local da pasta alternativa para o instantâneo.|  
|**pre_snapshot_script**|**nvarchar (510)**|Especifica um ponteiro para um local de arquivo **. SQL** . O Distribution Agent executará o script pré-instantâneo antes de executar qualquer script de objeto replicado, ao aplicar um instantâneo no Assinante.|  
|**post_snapshot_script**|**nvarchar (510)**|Especifica um ponteiro para um local de arquivo **. SQL** . O Distribution Agent executará o script pós-instantâneo depois que todos os outros scripts de objeto replicado tiverem sido aplicados durante uma sincronização inicial.|  
|**compress_snapshot**|**bit**|Especifica que o instantâneo gravado no local de *alt_snapshot_folder* deve ser compactado no [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato CAB. **0** especifica que o instantâneo não será compactado.|  
|**ftp_address**|**sysname**|O endereço de rede do serviço FTP para o Distribuidor. Especifica onde arquivos de instantâneo de publicação ficam localizados para serem retirados pelo Distribution Agent.|  
|**ftp_port**|**int**|O número da porta do serviço FTP do Distribuidor. Especifica onde os arquivos de instantâneo de publicação estão localizados para serem retirados pelo Distribution Agent.|  
|**ftp_subdirectory**|**nvarchar (510)**|Especifica onde os arquivos de instantâneo estarão disponíveis para serem retirados pelo Distribution Agent se a publicação oferecer suporte a arquivos de propagação usando o FTP.|  
|**ftp_login**|**nvarchar(256)**|O nome de usuário usado para se conectar ao serviço FTP.|  
|**ftp_password**|**nvarchar (1048)**|A senha de usuário usada para se conectar ao serviço FTP.|  
|**allow_dts**|**bit**|Especifica que a publicação permite transformações de dados. **1** especifica que as transformações DTS são permitidas. *Sem suporte para Publicadores não SQL.*|  
|**allow_anonymous**|**bit**|Indica se as assinaturas anônimas são permitidas na publicação, em que **1** significa que elas são permitidas.|  
|**centralized_conflicts**|**bit**|Especifica se registros de conflito são ou não armazenados no Publicador:<br /><br /> **0** = registros de conflitos são armazenados no Publicador e no Assinante que causou o conflito.<br /><br /> **1** = registros de conflitos são armazenados no Publicador.<br /><br /> *Sem suporte para Publicadores não SQL.*|  
|**conflict_retention**|**int**|Especifica o período de retenção de conflito, em dias. *Sem suporte para Publicadores não SQL.*|  
|**conflict_policy**|**int**|Especifica a política de resolução de conflito seguida quando a opção de assinante de atualização enfileirado é usada. Pode ser um destes valores:<br /><br /> **1** = o Publicador vence o conflito.<br /><br /> **2** = Assinante vence o conflito.<br /><br /> **3** = a assinatura é reinicializada.<br /><br /> *Sem suporte para Publicadores não SQL.*|  
|**queue_type**|**int**|Especifica o tipo de fila usado. Pode ser um destes valores:<br /><br /> **1** = MSMQ, que usa o [!INCLUDE[msCoName](../../includes/msconame-md.md)] enfileiramento de mensagens para armazenar transações.<br /><br /> **2** = SQL, que usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para armazenar transações.<br /><br /> Esta coluna não é usada por não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicadores.<br /><br /> Observação: o uso do [!INCLUDE[msCoName](../../includes/msconame-md.md)] enfileiramento de mensagens foi preterido e não tem mais suporte.<br /><br /> *Não há suporte para esta coluna em Publicadores não SQL.*|  
|**ad_guidname**|**sysname**|Especifica se a publicação é publicada no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory. Um GUID (identificador global exclusivo) válido especifica que a publicação é publicada no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory e o GUID é o **objectGUID**do objeto de publicação Active Directory correspondente. Se for NULL, a publicação não será publicada no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory. *Sem suporte para Publicadores não SQL.*|  
|**backward_comp_level**|**int**|Nível de compatibilidade de banco de dados, que pode ser um dos valores seguintes:<br /><br /> **90**  =  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .<br /><br /> **100**  =  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] .<br /><br /> *Sem suporte para Publicadores não SQL.*|  
|**ndescrição**|**nvarchar (255)**|Entrada descritiva para a publicação.|  
|**independent_agent**|**bit**|Especifica se existe um Distribution Agent autônomo para essa publicação.<br /><br /> **0** = a publicação usa um agente de distribuição compartilhado e cada par de banco de dados/assinante do Publicador tem um agente único e compartilhado.<br /><br /> **1** = há um agente de distribuição autônomo para esta publicação.|  
|**immediate_sync**|**bit**|Indica se os arquivos de sincronização são criados ou recriados sempre que o Agente de Instantâneo é executado, em que **1** significa que eles são criados toda vez que o agente é executado.|  
|**allow_push**|**bit**|Indica se as assinaturas push são permitidas na publicação, em que **1** significa que elas são permitidas.|  
|**allow_pull**|**bit**|Indica se as assinaturas pull são permitidas na publicação, em que **1** significa que elas são permitidas.|  
|**políticas**|**int**|A quantidade de alteração, em horas, a economizar para a publicação determinada.|  
|**allow_subscription_copy**|**bit**|Especifica se a capacidade para copiar os bancos de dados de assinatura que assinam esta publicação foi habilitada. **1** significa que a cópia é permitida.|  
|**allow_initialize_from_backup**|**bit**|Indica se os Assinantes podem iniciar uma assinatura para essa publicação de um backup em vez de um instantâneo inicial. **1** significa que as assinaturas podem ser inicializadas a partir de um backup e **0** significa que elas não podem. Para obter mais informações, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md). *Sem suporte para Publicadores não SQL.*|  
|**min_autonosync_lsn**|**binário (1)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**replicate_ddl**|**int**|Indica se a replicação do esquema tem suporte para a publicação. **1** indica que as instruções DDL executadas no Publicador são replicadas e **0** indica que as instruções DDL não são replicadas. Para obter mais informações, consulte [Make Schema Changes on Publication Databases](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md) (Fazer alterações de esquema em bancos de dados de publicação). *Sem suporte para Publicadores não SQL.*|  
|**options**|**int**|Bitmap que especifica opções de publicação adicionais, onde os valores de opção bit a bit são:<br /><br /> **0x1** -habilitado para replicação ponto a ponto.<br /><br /> **0x2** -publicar apenas alterações locais.<br /><br /> **0x4** -habilitado para assinantes não SQL Server.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helppublication](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [syspublications &#40;exibição do sistema&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/syspublications-system-view-transact-sql.md)   
 [&#41;syspublications &#40;Transact-SQL](../../relational-databases/system-tables/syspublications-transact-sql.md)  
  
  
