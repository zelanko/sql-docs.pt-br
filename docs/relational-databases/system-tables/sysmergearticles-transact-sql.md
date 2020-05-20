---
title: sysmergearticles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergearticles
- sysmergearticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergearticles system table
ms.assetid: e9b1648e-4660-4688-9f56-18b2baf7228c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8328c332fe35b8e157c8631d90b8de67c6e96e17
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831926"
---
# <a name="sysmergearticles-transact-sql"></a>sysmergearticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada artigo de mesclagem definido no banco de dados local. Essa tabela é armazenada no banco de dados de publicação.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do artigo.|  
|**tipo**|**tinyint**|Indica o tipo do artigo, que pode ser um dos seguintes:<br /><br /> **10** = tabela.<br /><br /> **32** = procedimento armazenado (somente esquema).<br /><br /> **64** = exibição ou exibição indexada (somente esquema).<br /><br /> **128** = função definida pelo usuário (somente esquema).<br /><br /> **160** = sinônimo (somente esquema).|  
|**objid**|**int**|O identificador de objeto.|  
|**sync_objid**|**int**|A ID de objeto da exibição que representa o conjunto de dados sincronizado.|  
|**view_type**|**tinyint**|O tipo da exibição.<br /><br /> **0** = não é uma exibição; Use todos os objetos base.<br /><br /> **1** = exibição permanente.<br /><br /> **2** = exibição temporária.|  
|**artid**|**uniqueidentifier**|O número de identificação exclusivo para o artigo determinado.|  
|**ndescrição**|**nvarchar (255)**|A descrição breve do artigo.|  
|**pre_creation_command**|**tinyint**|A ação padrão a ser tomada quando o artigo é criado no banco de dados de assinatura:<br /><br /> **0 =** Nenhum – se a tabela já existir no Assinante, nenhuma ação será executada.<br /><br /> **1** = drop-remove a tabela antes de recriá-la.<br /><br /> **2** = Delete-emite uma exclusão com base na cláusula WHERE no filtro de subconjunto.<br /><br /> **3** = truncar-igual a **2**, mas exclui páginas em vez de linhas. Porém, não exige uma cláusula WHERE.|  
|**pubid**|**uniqueidentifier**|A ID da publicação à qual o artigo atual pertence.|  
|**apelido**|**int**|O mapeamento de apelido para identificação do artigo.|  
|**column_tracking**|**int**|Iindicates se o rastreamento de coluna está implementado para o artigo.|  
|**status**|**tinyint**|Indica o status do artigo, que pode ser um dos seguintes:<br /><br /> **1** = não sincronizado – o script de processamento inicial para publicar a tabela será executado na próxima vez que o agente de instantâneo for executado.<br /><br /> **2** = ativo-o script de processamento inicial para publicar a tabela foi executado.<br /><br /> **5** = New_inactive-a ser adicionado.<br /><br /> **6** = New_active-a ser adicionado.|  
|**conflict_table**|**sysname**|O nome da tabela local que contém os registros conflitantes para o artigo atual. Essa tabela é somente informativa e seu conteúdo pode ser modificado ou excluído por rotinas de resolução de conflitos personalizadas ou diretamente pelo administrador.|  
|**creation_script**|**nvarchar (255)**|O script de criação para este artigo.|  
|**conflict_script**|**nvarchar (255)**|O script de conflito para este artigo.|  
|**article_resolver**|**nvarchar (255)**|O resolvedor de conflitos personalizado de nível de linha para este artigo.|  
|**ins_conflict_proc**|**sysname**|O procedimento usado para gravar em conflito com **conflict_table**.|  
|**insert_proc**|**sysname**|O procedimento usado pelo resolvedor de conflitos padrão para inserir linhas durante a sincronização.|  
|**update_proc**|**sysname**|O procedimento usado pelo resolvedor de conflitos padrão para atualizar linhas durante a sincronização.|  
|**select_proc**|**sysname**|O nome de um procedimento armazenado gerado automaticamente usado pelo Merge Agent para efetuar bloqueio e localizar colunas e linhas para um artigo.|  
|**metadata_select_proc**|**sysname**|O nome do procedimento armazenado gerado automaticamente usado para acessar metadados nas tabelas do sistema de replicação de mesclagem.|  
|**delete_proc**|**sysname**|O procedimento usado pelo resolvedor de conflitos padrão para excluir linhas durante a sincronização.|  
|**schema_option**|**binário (8)**|Para obter os valores com suporte de *schema_option*, consulte [sp_addmergearticle &#40;&#41;do Transact-SQL ](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).|  
|**destination_object**|**sysname**|O nome da tabela criada no Assinante.|  
|**destination_owner**|**sysname**|O nome do proprietário do objeto de destino.|  
|**resolver_clsid**|**nvarchar(50)**|A ID do resolvedor de conflitos personalizado.|  
|**subset_filterclause**|**nvarchar(1000)**|A cláusula de filtro para este artigo.|  
|**missing_col_count**|**int**|O número de colunas ausentes.|  
|**missing_cols**|**varbinary(128)**|O bitmap de colunas ausentes.|  
|**excluded_cols**|**varbinary(128)**|O bitmap das colunas excluídas do artigo quando é enviado ao Assinante.|  
|**excluded_col_count**|**int**|O número de colunas excluídas.|  
|**Columns**|**varbinary(128)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**deleted_cols**|**varbinary(128)**|Os bitmaps de colunas que foram excluídas da tabela de origem.|  
|**resolver_info**|**nvarchar (255)**|O armazenamento de informações adicionais requeridas por resolvedores de conflitos personalizados.|  
|**view_sel_proc**|**nvarchar (290)**|O nome de um procedimento armazenado que o Merge Agent usa para popular inicialmente um artigo em uma publicação filtrada dinamicamente e para enumerar linhas alteradas em qualquer publicação filtrada.|  
|**gen_cur**|**int**|O número gerado de alterações locais para a tabela base de um artigo.|  
|**vertical_partition**|**int**|Especifica se a filtragem de coluna está habilitada em um artigo de tabela. **0** indica que não há nenhuma filtragem vertical e publica todas as colunas.|  
|**identity_support**|**int**|Especifica se o tratamento automático do intervalo de identidades está habilitado. **1** significa que o tratamento de intervalo de identidade está habilitado e **0** significa que não há suporte para o intervalo de identidade.|  
|**before_image_objid**|**int**|A ID de objeto da tabela de controle. A tabela de rastreamento contém certos valores de coluna de chave quando uma publicação é criada com * \@ keep_partition_changes*  =  **true**.|  
|**before_view_objid**|**int**|A ID de objeto de uma tabela de exibição. A exibição está em uma tabela que controla se uma linha pertenceu a um Assinante específico antes de ser excluída ou atualizada. Aplica-se somente quando uma publicação é criada com * \@ keep_partition_changes*  =  **true.**|  
|**verify_resolver_signature**|**int**|Especifica se uma assinatura digital é verificada antes de usar um resolvedor em replicação de mesclagem:<br /><br /> **0** = a assinatura não é verificada.<br /><br /> **1** = a assinatura é verificada para ver se ela é de uma fonte confiável.|  
|**allow_interactive_resolver**|**bit**|Especifica se o uso do Resolvedor Interativo em um artigo está habilitado. **1** especifica que o resolvedor interativo é usado no artigo.|  
|**fast_multicol_updateproc**|**bit**|Especifica se o Merge Agent foi habilitado para aplicar alterações em várias colunas na mesma linha em uma instrução UPDATE.<br /><br /> **0** = emite uma atualização separada para cada coluna alterada.<br /><br /> **1** = emite uma instrução UPDATE que faz com que as atualizações ocorram em várias colunas em uma instrução.|  
|**check_permissions**|**int**|O bitmap das permissões no nível de tabela que são verificadas quando o Merge Agent aplica alterações no Publicador. *check_permissions* pode ter um destes valores:<br /><br /> **0x00 =** As permissões não são verificadas.<br /><br /> **0x10 =** Verifica as permissões no Publicador antes que as inserções feitas em um assinante possam ser carregadas.<br /><br /> **0x20 =** Verifica as permissões no Publicador antes que as atualizações feitas em um assinante possam ser carregadas.<br /><br /> **0x40 =** Verifica as permissões no Publicador antes que as exclusões feitas em um assinante possam ser carregadas.|  
|**maxversion_at_cleanup**|**int**|A geração mais alta para a qual os metadados são limpos.|  
|**processing_order**|**int**|Indica a ordem de processamento dos artigos em uma publicação de mesclagem; em que um valor de **0** indica que o artigo está desordenado e os artigos são processados na ordem do valor mais baixo para o mais alto. Se dois artigos tiverem o mesmo valor, serão processados simultaneamente. Para obter mais informações, confira [propriedades de Especificar Replicação de Mesclagem](../../relational-databases/replication/merge/specify-merge-replication-properties.md).|  
|**upload_options**|**tinyint**|Define restrições em atualizações feitas em um Assinante com uma assinatura de cliente, que pode ser um dos valores a seguir.<br /><br /> **0** = não há restrições sobre as atualizações feitas em um assinante com uma assinatura de cliente; todas as alterações são carregadas no Publicador.<br /><br /> **1** = as alterações são permitidas em um assinante com uma assinatura de cliente, mas não são carregadas no Publicador.<br /><br /> **2** = as alterações não são permitidas em um assinante com uma assinatura de cliente.<br /><br /> Para obter mais informações, consulte [Otimizar o desempenho da replicação de mesclagem com artigos somente para download](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).|  
|**published_in_tran_pub**|**bit**|Indica que um artigo em uma publicação de mesclagem também é publicado em uma publicação transacional.<br /><br /> **0** = o artigo não é publicado em um artigo transacional.<br /><br /> **1** = o artigo também é publicado em um artigo transacional.|  
|**baixa**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**procname_postfix**|**nchar(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**well_partitioned_lightweight**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**before_upd_view_objid**|**int**|A ser adicionado.|  
|**delete_tracking**|**bit**|Indica se as exclusões são replicadas.<br /><br /> **0** = as exclusões não são replicadas<br /><br /> **1** = as exclusões são replicadas, que é o comportamento padrão para replicação de mesclagem.<br /><br /> Quando o valor de *delete_tracking* for **0**, as linhas excluídas no Assinante deverão ser removidas manualmente no Publicador e as linhas excluídas no Publicador deverão ser removidas manualmente no Assinante.<br /><br /> Observação: um valor de **0** resulta em não convergência.|  
|**compensate_for_errors**|**bit**|Indica se as ações de compensação são tomadas quando são encontrados erros durante a sincronização.<br /><br /> **0** = ações de compensação estão desabilitadas.<br /><br /> **1** = alterações que não podem ser aplicadas em um assinante ou Publicador sempre levam a ações de compensação para desfazer essas alterações, que é o comportamento padrão para replicação de mesclagem.<br /><br /> Observação: um valor de **0** resulta em não convergência.|  
|**pub_range**|**bigint**|O tamanho do intervalo de identidade do publicador.|  
|**amplitude**|**bigint**|O tamanho dos valores de identidade consecutivos que seria atribuído a assinantes em um ajuste.|  
|**os**|**int**|A porcentagem de limite do intervalo de identidade.|  
|**stream_blob_columns**|**bit**|Especifica se uma otimização de fluxo de dados é usada ao replicar colunas de objeto binário grande. **1** significa que a otimização é tentada.|  
|**preserve_rowguidcol**|**bit**|Indica se replicação usa uma coluna rowguid existente. Um valor de **1** significa que uma coluna ROWGUIDCOL existente é usada. **0** significa que a replicação adicionou a coluna ROWGUIDCOL.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)  
  
  
