---
title: sp_helpmergepublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_helpmergepublication
- sp_helpmergepublication_TSQL
helpviewer_keywords:
- sp_helpmergepublication
ms.assetid: dfe1e1e1-9a65-406a-aced-6385a078e135
caps.latest.revision: 55
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3898ae087e1dd918d014735ce4c03316bef4551c
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43027263"
---
# <a name="sphelpmergepublication-transact-sql"></a>sp_helpmergepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre uma publicação de mesclagem. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpmergepublication [ [ @publication = ] 'publication' ]  
    [ , [ @found = ] 'found' OUTPUT ]  
    [ , [ @publication_id = ] 'publication_id' OUTPUT ]  
    [ , [ @reserved = ] 'reserved' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @publication **=** ] **'***publicação***'**  
 O nome da publicação. *publicação*está **sysname**, com um padrão de **%**, que retorna informações sobre todas as publicações de mesclagem no banco de dados atual.  
  
 [ @found **=** ] **'***encontrado***'** saída  
 Um sinalizador para indicar linhas de retorno. *encontrado*está **int** e um parâmetro de saída, com um padrão NULL. **1** indica que a publicação foi localizada. **0** indica a publicação não foi encontrada.  
  
 [ @publication_id **=**] **'***publication_id***'** saída  
 O número de identificação da publicação. *publication_id* está **uniqueidentifier** e um parâmetro de saída, com um padrão NULL.  
  
 [ @reserved **=**] **'***reservado***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *reservado* está **nvarchar (20)**, com um padrão NULL.  
  
 [ @publisher **=** ] **'***publisher***'**  
 O nome do publicador. *Publisher* está **sysname**, com um padrão NULL.  
  
 [@publisher_db **=** ] **'***publisher_db***'**  
 O nome do banco de dados de publicação. *publisher_db* está **sysname**, com um padrão NULL.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|id|**int**|Ordem sequencial da publicação na lista de conjunto de resultados.|  
|nome|**sysname**|Nome da publicação.|  
|descrição|**nvarchar(255)**|Descrição da publicação.|  
|status|**tinyint**|Indica quando os dados da publicação estão disponíveis.|  
|retenção|**int**|O tempo para salvar metadados sobre alterações para artigos na publicação. As unidades desse período de tempo podem ser dias, semanas, meses ou anos. Para obter informações sobre unidades, consulte a coluna retention_period_unit.|  
|sync_mode|**tinyint**|O modo de sincronização dessa publicação:<br /><br /> **0** = programa de cópia em massa nativa (**bcp** utilitário)<br /><br /> **1** = cópia em massa de caracteres|  
|allow_push|**int**|Determina se podem ser criadas assinaturas push para a publicação especificada. **0** significa que uma assinatura push não é permitida.|  
|allow_pull|**int**|Determina se podem ser criadas assinaturas pull para a publicação especificada. **0** significa que uma assinatura pull não é permitida.|  
|allow_anonymous|**int**|Determina se podem ser criadas assinaturas anônimas para a publicação determinada. **0** significa que uma assinatura anônima não é permitida.|  
|centralized_conflicts|**int**|Determina se registros de conflito são armazenados no Publicador determinado:<br /><br /> **0** = registros de conflito são armazenados no publicador e no assinante que causou o conflito.<br /><br /> **1** = todos os registros de conflito são armazenados no publicador.|  
|priority|**float(8)**|A prioridade da assinatura de loopback.|  
|snapshot_ready|**tinyint**|Indica se o instantâneo da publicação está pronto:<br /><br /> **0** = instantâneo está pronto para uso.<br /><br /> **1** = instantâneo não está pronto para uso.|  
|publication_type|**int**|O tipo de publicação:<br /><br /> **0** = instantâneo.<br /><br /> **1** = transacional.<br /><br /> **2** = mesclagem.|  
|pubid|**uniqueidentifier**|O identificador exclusivo da publicação.|  
|snapshot_jobid|**binary(16)**|A ID de trabalho do Agente de Instantâneo. Para obter a entrada para o trabalho de instantâneo a [sysjobs](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md) tabela do sistema, você deve converter esse valor hexadecimal para **uniqueidentifier**.|  
|enabled_for_internet|**int**|Determina se a publicação está habilitada para a Internet. Se **1**, os arquivos de sincronização para a publicação são colocados no `C:\Program Files\Microsoft SQL Server\MSSQL\Repldata\Ftp` directory. O usuário deve criar o diretório de FTP. Se **0**, a publicação não está habilitada para acesso à Internet.|  
|dynamic_filter|**int**|Indica se um filtro de linha parametrizado é usado. **0** significa que um filtro de linha com parâmetros não é usado.|  
|has_subscription|**bit**|Indica se a publicação tem alguma assinatura. **0** significa que no momento, não há nenhuma assinatura para essa publicação.|  
|snapshot_in_default_folder|**bit**|Especifica se os arquivos de instantâneo são armazenados na pasta padrão.<br /><br /> Se **1**, arquivos de instantâneo podem ser encontrados na pasta padrão.<br /><br /> Se **0**, os arquivos de instantâneo são armazenados no local alternativo especificado por **alt_snapshot_folder**. Os locais alternativos podem ser um outro servidor, uma unidade de rede ou uma mídia removível (como um CD-ROM ou discos removíveis). Você também pode salvar os arquivos de instantâneo em um site de FTP para serem recuperados pelo Assinante posteriormente.<br /><br /> Observação: Esse parâmetro pode ser verdadeiro e ainda ter um local na **alt_snapshot_folder** parâmetro. Essa combinação especifica que os arquivos de instantâneo serão armazenados nos locais padrão e alternativo.|  
|alt_snapshot_folder|**nvarchar(255)**|Especifica o local da pasta alternativa para o instantâneo.|  
|pre_snapshot_script|**nvarchar(255)**|Especifica um ponteiro para um **. SQL** scripts de arquivo que o Merge Agent é executado antes de qualquer objeto replicado ao aplicar o instantâneo no assinante.|  
|post_snapshot_script|**nvarchar(255)**|Especifica um ponteiro para um **. SQL** replicado de arquivo que o agente de mesclagem executa depois que todos os outros scripts de objetos e dados tenham sido aplicados durante uma sincronização inicial.|  
|compress_snapshot|**bit**|Especifica que o instantâneo gravado para o **alt_snapshot_folder** local é compactado no [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato CAB.|  
|ftp_address|**sysname**|É o endereço de rede do serviço FTP para o Distribuidor. Especifica onde os arquivos de instantâneo de publicação ficam localizados para o agente de mesclagem acompanhar.|  
|ftp_port|**int**|É o número da porta do serviço FTP para o Distribuidor. **ftp_port** tem um padrão de **21**. Especifica onde os arquivos de instantâneo de publicação estão localizados para serem retirados pelo Agente de Mesclagem.|  
|ftp_subdirectory|**nvarchar(255)**|Especifica onde os arquivos de instantâneo de publicação estão disponíveis para serem retirados pelo Agente de Mesclagem quando o instantâneo é entregue por meio do FTP.|  
|ftp_login|**sysname**|O nome de usuário é usado para se conectar ao serviço FTP.|  
|conflict_retention|**int**|Especifica o período de retenção, em dias, durante o qual os conflitos são retidos. Quando o número de dias especificado for ultrapassado, a linha de conflito será limpa na tabela de conflitos.|  
|keep_partition_changes|**int**|Especifica se otimização de sincronização está ocorrendo para esta publicação. **keep_partition_changes** tem um padrão de **0**. Um valor de **0** significa que a sincronização não é otimizada e as partições enviadas a todos os assinantes são verificadas quando dados são alterados em uma partição.<br /><br /> **1** significa que a sincronização é otimizada e somente assinantes com linhas nas partições alteradas são afetados.<br /><br /> Observação: Por padrão, publicações de mesclagem usam partições pré-calculadas que fornecem um grau maior de otimização que essa opção. Para obter mais informações, consulte [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md) e [otimizar o desempenho de filtro parametrizado com partições pré-computadas](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).|  
|allow_subscription_copy|**int**|Especifica se a capacidade para copiar os bancos de dados de assinatura que assinam esta publicação foi habilitada. Um valor de **0** significa que não é permitido copiar.|  
|allow_synctoalternate|**int**|Especifica se um parceiro de sincronização alternativo tem permissão para sincronizar com esse Publicador. Um valor de **0** significa um parceiro de sincronização não é permitido.|  
|validate_subscriber_info|**nvarchar(500)**|Lista as funções que estão sendo usadas para recuperar informações do Assinante e validar os critérios de filtragem de linha com parâmetros no Assinante. Ajuda a verificar se as informações estão consistentemente particionadas com cada mesclagem.|  
|backward_comp_level|**int**|O nível de compatibilidade do banco de dados, podendo ser um dos seguintes:<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **90**  =  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP1<br /><br /> **90**  =  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|publish_to_activedirectory|**bit**|Especifica se as informações de publicação são publicadas para o Active Directory. Um valor de **0** significa que as informações de publicação não estão disponíveis a partir do Active Directory.<br /><br /> Esse parâmetro foi preterido e tem suporte somente para a compatibilidade com versões anteriores de scripts. Você não pode mais adicionar informações de publicação no Active Directory.|  
|max_concurrent_merge|**int**|O número de processos de mesclagem simultâneos. Se **0**, não há nenhum limite para o número de processos de mesclagem simultâneos em execução em um determinado momento.|  
|max_concurrent_dynamic_snapshots|**int**|O número máximo de sessões de instantâneo de dados filtrados simultâneas que pode ser executado na publicação de mesclagem. Se **0**, não há nenhum limite para o número máximo de sessões de instantâneo de dados filtrados simultâneas que podem ser executados simultaneamente na publicação, em um determinado momento.|  
|use_partition_groups|**int**|Determina se partições pré-calculadas são utilizadas. Um valor de **1** significa que partições pré-computadas é usadas.|  
|num_of_articles|**int**|Número de artigos na publicação.|  
|replicate_ddl|**int**|Se as alterações de esquema de tabelas publicadas são replicadas. Um valor de **1** significa que as alterações de esquema são replicadas.|  
|publication_number|**smallint**|Número atribuído à publicação.|  
|allow_subscriber_initiated_snapshot|**bit**|Determina se os Assinantes podem iniciar o processo de geração de instantâneo de dados filtrados. Um valor de **1** significa que os assinantes podem iniciar o processo de instantâneo.|  
|allow_web_synchronization|**bit**|Determina se a publicação está habilitada para sincronização da Web. Um valor de **1** significa que a sincronização da Web está habilitada.|  
|web_synchronization_url|**nvarchar(500)**|A URL da Internet usada para a sincronização da Web.|  
|allow_partition_realignment|**bit**|Determina se as exclusões serão enviadas ao assinante quando a modificação da linha no publicador gerar uma alteração na partição. Um valor de **1** significa que as exclusões serão enviadas ao assinante.  Para obter mais informações, consulte [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md).|  
|retention_period_unit|**tinyint**|Define a unidade usada ao definir a retenção. Esse valor pode ser um dos seguintes:<br /><br /> **0** = dia|<br /><br /> **1** = semana<br /><br /> **2** = mês<br /><br /> **3** = ano|  
|has_downloadonly_articles|**bit**|Indica se os artigos pertencentes à publicação são de somente download. Um valor de **1** indica que há artigos de somente download.|  
|decentralized_conflicts|**int**|Indica se os registros de conflito são armazenados no Assinante que causou o conflito. Um valor de **0** indica que os registros de conflito não são armazenados no assinante. Um valor 1 indica que os registros de conflito são armazenados no Assinante.|  
|generation_leveling_threshold|**int**|Especifica o número de alterações que estão contidos em uma geração. Uma geração é uma coleção das alterações que são entregues a um publicador ou assinante|  
|automatic_reinitialization_policy|**bit**|Indica se as alterações são carregadas do Assinante antes da ocorrência de uma reinicialização automática. Um valor de **1** indica que as alterações são carregadas do assinante antes que ocorra uma reinicialização automática. Um valor 0 indica que as alterações não são carregadas antes de uma reinicialização automática.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 sp_helpmergepublication é usado em replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Membros da lista de acesso à publicação de uma publicação podem executar sp_helpmergepublication para aquela publicação. Membros da função de banco de dados fixa db_owner no banco de dados de publicação podem executar sp_helpmergepublication para obter informações sobre todas as publicações.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_helpmergepublication](../../relational-databases/replication/codesnippet/tsql/sp-helpmergepublication-_1.sql)]  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_dropmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
