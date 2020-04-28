---
title: sysmergepublications (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergepublications
- sysmergepublications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergepublications system table
ms.assetid: 7f82c6c3-22d1-47c0-a92b-4d64b98cc455
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9a2c2802f0bd077c64800225590b2346205fb30a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68029784"
---
# <a name="sysmergepublications-transact-sql"></a>sysmergepublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada publicação de mesclagem definida no banco de dados. Essa tabela é armazenada nos bancos de dados de publicação e de assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**programa**|**sysname**|O nome do servidor padrão.|  
|**publisher_db**|**sysname**|O nome do banco de dados Publicador padrão.|  
|**name**|**sysname**|O nome da publicação.|  
|**ndescrição**|**nvarchar (255)**|Uma descrição breve da publicação.|  
|**políticas**|**int**|O período de retenção para todo o conjunto de publicação, em que a unidade é indicada pelo valor da coluna **retention_period_unit** .|  
|**publication_type**|**tinyint**|Indica se a publicação é filtrada:<br /><br /> **0** = não filtrado.<br /><br /> **1** = filtrado.|  
|**pubid**|**uniqueidentifier**|O número de identificação exclusivo desta publicação. Isso é gerado quando a publicação é adicionada.|  
|**designmasterid**|**uniqueidentifier**|Reservado para uso futuro.|  
|**parentID**|**uniqueidentifier**|Indica a publicação pai da qual a publicação ponto a ponto ou de subconjunto atual foi criada (usado para topologias de publicação hierárquicas).|  
|**sync_mode**|**tinyint**|O modo de sincronização desta publicação:<br /><br /> **0** = nativo.<br /><br /> **1** = caractere.|  
|**allow_push**|**int**|Indica se a publicação permite assinaturas push.<br /><br /> **0** = assinaturas push não permitidas.<br /><br /> **1** = assinaturas push são permitidas.|  
|**allow_pull**|**int**|Indica se a publicação permite assinaturas pull.<br /><br /> **0** = assinaturas pull não permitidas.<br /><br /> **1** = assinaturas pull são permitidas.|  
|**allow_anonymous**|**int**|Indica se a publicação permite assinaturas anônimas.<br /><br /> **0** = assinaturas anônimas não permitidas.<br /><br /> **1** = assinaturas anônimas são permitidas.|  
|**centralized_conflicts**|**int**|Indica se os registros de conflito são armazenados no Publicador:<br /><br /> **0** = registros de conflitos não são armazenados no Publicador.<br /><br /> **1** = registros de conflitos são armazenados no Publicador.|  
|**status**|**tinyint**|Reservado para uso futuro.|  
|**snapshot_ready**|**tinyint**|Indica o status para o instantâneo da publicação:<br /><br /> **0** = o instantâneo não está pronto para uso.<br /><br /> **1** = o instantâneo está pronto para uso.<br /><br /> **2** = um novo instantâneo para esta publicação deve ser criado.|  
|**enabled_for_internet**|**bit**|Indica se os arquivos de sincronização para a publicação são expostos à Internet pelo FTP e outros serviços.<br /><br /> **0** = os arquivos de sincronização podem ser acessados pela Internet.<br /><br /> **1** = os arquivos de sincronização não podem ser acessados pela Internet.|  
|**dynamic_filters**|**bit**|Indica se a publicação é filtrada usando um filtro de linha com parâmetros.<br /><br /> **0** = a publicação não é filtrada por linha.<br /><br /> **1** = a publicação é de linha filtrada.|  
|**snapshot_in_defaultfolder**|**bit**|Especifica se arquivos de instantâneo são armazenados na pasta padrão:<br /><br /> **0** = os arquivos de instantâneo estão na pasta padrão.<br /><br /> **1** = os arquivos de instantâneo são armazenados no local especificado por **alt_snapshot_folder**.|  
|**alt_snapshot_folder**|**nvarchar (255)**|O local da pasta alternativa para o instantâneo.|  
|**pre_snapshot_script**|**nvarchar (255)**|Ponteiro para um. o arquivo **SQL** que o agente de mesclagem executa antes de qualquer um dos scripts do objeto de replicação ao aplicar o instantâneo no Assinante.|  
|**post_snapshot_script**|**nvarchar (255)**|O ponteiro para um. o arquivo **SQL** que o agente de mesclagem é executado depois que todos os outros scripts e dados de objeto de replicação são aplicados durante uma sincronização inicial.|  
|**compress_snapshot**|**bit**|Especifica se o instantâneo gravado no local de **alt_snapshot_folder** é compactado no [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato CAB. **0** especifica que o arquivo não está compactado.|  
|**ftp_address**|**sysname**|Endereço de rede do serviço de protocolo FTP (FTP) para o distribuidor. Especifica onde os arquivos de instantâneo de publicação ficam localizados para serem separados pelo Agente de Mesclagem se o FTP estiver habilitado.|  
|**ftp_port**|**int**|O número da porta do serviço FTP do Distribuidor.|  
|**ftp_subdirectory**|**nvarchar (255)**|O subdiretório onde os arquivos de instantâneo estão disponíveis para serem separados pelo Agente de Mesclagem.|  
|**ftp_login**|**sysname**|O nome de usuário usado para se conectar ao serviço FTP.|  
|**ftp_password**|**nvarchar (524)**|A senha de usuário usada para se conectar ao serviço FTP.|  
|**conflict_retention**|**int**|Especifica o período de retenção, em dias, durante o qual os conflitos são retidos. Após esse período, a linha de conflito é excluída da tabela de conflitos.|  
|**keep_before_values**|**int**|Especifica se otimização de sincronização está ocorrendo para esta publicação:<br /><br /> **0** = a sincronização não é otimizada e as partições enviadas a todos os assinantes serão verificadas quando os dados forem alterados em uma partição.<br /><br /> **1** = a sincronização é otimizada e somente os assinantes que têm linhas na partição alterada são afetados.|  
|**allow_subscription_copy**|**bit**|Especifica se a capacidade de copiar banco de dados de assinatura foi habilitada. **0** significa que a cópia não é permitida.|  
|**allow_synctoalternate**|**bit**|Especifica se um parceiro de sincronização alternativo tem permissão para sincronizar com esse Publicador. **0** significa que um parceiro de sincronização não é permitido.|  
|**validate_subscriber_info**|**nvarchar (500)**|Lista as funções que estão sendo usadas para recuperar informações do Assinante e validar os critérios de filtragem de linha com parâmetros no Assinante.|  
|**ad_guidname**|**sysname**|Especifica se a publicação é publicada no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory. Um GUID válido especifica que a publicação é publicada no Active Directory e o GUID é o objeto de publicação de Active Directory do **objectGUID**correspondente. Se for NULL, a publicação não será publicada no Active Directory.|  
|**backward_comp_level**|**int**|Nível de compatibilidade do banco de dados. Pode ser um dos seguintes valores:<br /><br /> **90** = 90[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].<br /><br /> **100** = 100[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].|  
|**max_concurrent_merge**|**int**|O número máximo de processos de mesclagem simultâneos permitido. Um valor de **0** para essa propriedade significa que não há nenhum limite para o número de processos de mesclagem simultâneos em execução em um determinado momento. Essa propriedade define um limite para o número de processos de mesclagem simultâneos que podem ser executados em uma publicação de mesclagem ao mesmo tempo. Se houver mais processos de instantâneo agendados ao mesmo tempo do que o valor permitido para execução, os trabalhos em excesso serão enfileirados e esperarão até que o processo de mesclagem em execução no momento seja concluído.|  
|**max_concurrent_dynamic_snapshots**|**int**|O número máximo permitido de sessões de instantâneo de dados filtrados simultâneas que pode ser executado na publicação de mesclagem. Se for **0**, não há nenhum limite para o número máximo de sessões de instantâneos de dados filtradas simultâneas que podem ser executadas simultaneamente na publicação em um determinado momento. Essa propriedade define um limite para o número de processos de instantâneo simultâneos que pode ser executado em uma publicação de mesclagem de uma só vez. Se houver mais processos de instantâneo agendados ao mesmo tempo do que o valor permitido para execução, os trabalhos em excesso serão enfileirados e esperarão até que o processo de mesclagem em execução no momento seja concluído.|  
|**use_partition_groups**|**smallint**|Especifica se a publicação usa partições pré-computadas.|  
|**dynamic_filters_function_list**|**nvarchar (500)**|Uma lista de funções delimitada por ponto-e-vírgula usada nos filtros de linha com parâmetros da publicação.|  
|**partition_id_eval_proc**|**sysname**|Especifica o nome do procedimento executado pelo Agente de Mesclagem de um Assinante para determinar a ID de partição atribuída.|  
|**publication_number**|**smallint**|Especifica a coluna de identidade que fornece um mapeamento de 2 bytes para **pubid**. **pubid** é um identificador global exclusivo para uma publicação, enquanto o número da publicação é exclusivo somente em um banco de dados especificado.|  
|**replicate_ddl**|**int**|Indica se replicação de esquema tem suporte para a publicação.<br /><br /> **0** = as instruções DDL não são replicadas.<br /><br /> **1** = as instruções DDL executadas no Publicador são replicadas.<br /><br /> Para obter mais informações, consulte [Make Schema Changes on Publication Databases](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md) (Fazer alterações de esquema em bancos de dados de publicação).|  
|**allow_subscriber_initiated_snapshot**|**bit**|Indica que os Assinantes podem iniciar o processo que gera o instantâneo para uma publicação usando filtros com parâmetros. **1** indica que os assinantes podem iniciar o processo de instantâneo.|  
|**dynamic_snapshot_queue_timeout**|**int**|Especifica quantos minutos um Assinante precisa esperar na fila para que o processo de geração de instantâneo comece, ao usar filtros com parâmetros.|  
|**dynamic_snapshot_ready_timeout**|**int**|Especifica quantos minutos um Assinante espera para que o processo de geração de instantâneo seja concluído, ao usar filtros com parâmetros.|  
|**distribuidor**|**sysname**|O nome do Distribuidor para a publicação.|  
|**snapshot_jobid**|**binary(16)**|Identifica o trabalho de agente que gera o instantâneo quando o Assinante pode iniciar o processo de geração de instantâneo.|  
|**allow_web_synchronization**|**bit**|Especifica se a publicação está habilitada para sincronização da Web, em que **1** significa que a sincronização da Web está habilitada para a publicação.|  
|**web_synchronization_url**|**nvarchar (500)**|Especifica o valor padrão da URL da Internet usado para sincronização da Web.|  
|**allow_partition_realignment**|**bit**|Indica se exclusões serão enviadas para o Assinante quando modificação da linha no Publicador causar a mudança de sua partição.<br /><br /> **0** = os dados de uma partição antiga serão deixados no Assinante, onde as alterações feitas a esses dados no Publicador não serão replicadas para esse assinante, mas as alterações feitas no Assinante serão replicadas para o Publicador.<br /><br /> **1** = exclui o Assinante para refletir os resultados de uma alteração de partição removendo dados que não fazem mais parte da partição do Assinante.<br /><br /> Para obter mais informações, consulte [sp_addmergepublication &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md).<br /><br /> Observação: os dados que permanecem no Assinante quando esse valor é **0** devem ser tratados como se fossem somente leitura; no entanto, isso não é estritamente imposto pelo sistema de replicação.|  
|**retention_period_unit**|**tinyint**|Define a unidade usada ao definir a *retenção*, que pode ser um destes valores:<br /><br /> **0** = dia.<br /><br /> **1** = semana.<br /><br /> **2** = mês.<br /><br /> **3** = ano.|  
|**decentralized_conflicts**|**int**|Indica se os registros de conflito são armazenados ao Assinante que causou o conflito:<br /><br /> **0** = registros de conflitos não são armazenados no Assinante.<br /><br /> **1** = registros de conflitos são armazenados no Assinante.|  
|**generation_leveling_threshold**|**int**|Especifica o número de alterações contido em uma geração. Uma geração é uma coleção de alterações que é entregue a um Publicador ou Assinante.|  
|**automatic_reinitialization_policy**|**bit**|Indica se as alterações são carregadas do Assinante antes da ocorrência de uma reinicialização automática.<br /><br /> **1** = as alterações são carregadas do assinante antes que ocorra uma reinicialização automática.<br /><br /> **0** = as alterações não são carregadas antes de uma reinicialização automática.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changemergepublication](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_helpmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)  
  
  
