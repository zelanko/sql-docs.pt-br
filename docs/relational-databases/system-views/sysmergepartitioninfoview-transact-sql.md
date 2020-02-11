---
title: sysmergepartitioninfoview (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergepartitioninfoview
- sysmergepartitioninfoview_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergepartitioninfoview view
ms.assetid: 714e2935-1bc7-4901-aea2-64b1bbda03d6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 40b1ebc5319c13b5aa84a28e1a5c5546dd62bd03
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094821"
---
# <a name="sysmergepartitioninfoview-transact-sql"></a>sysmergepartitioninfoview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A exibição **sysmergepartitioninfoview** expõe informações de particionamento para artigos de tabela. Essa exibição é armazenada no banco de dados de publicação, no Publicador, e no banco de dados de assinatura, no Assinante.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|O nome do artigo.|  
|**tipo**|**tinyint**|Indica o tipo do artigo, que pode ser um dos seguintes:<br /><br /> **0x0A** = tabela.<br /><br /> **0x20** = somente esquema de procedimento.<br /><br /> **0x40** = somente esquema de exibição ou somente esquema de exibição indexada.<br /><br /> **0x80** = somente esquema de função.|  
|**objID**|**int**|O identificador do objeto publicado.|  
|**sync_objid**|**int**|A ID de objeto da exibição que representa o conjunto de dados sincronizado.|  
|**view_type**|**tinyint**|O tipo da exibição.<br /><br /> **0** = não é uma exibição; Use todos os objetos base.<br /><br /> **1** = exibição permanente.<br /><br /> **2** = exibição temporária.|  
|**artid**|**uniqueidentifier**|O número de identificação exclusivo para o artigo determinado.|  
|**ndescrição**|**nvarchar (255)**|A descrição breve do artigo.|  
|**pre_creation_command**|**tinyint**|A ação padrão a ser tomada quando o artigo é criado no banco de dados de assinatura:<br /><br /> **0** = None-se a tabela já existir no Assinante, nenhuma ação será executada.<br /><br /> **1** = descartar a tabela antes de recriá-la.<br /><br /> **2** = Delete-emite uma exclusão com base na cláusula WHERE no filtro de subconjunto.<br /><br /> **3** = truncar-igual a 2, mas exclui páginas em vez de linhas. Porém, não exige uma cláusula WHERE.|  
|**pubid**|**uniqueidentifier**|A ID da publicação à qual o artigo atual pertence.|  
|**apelido**|**int**|O mapeamento de apelido para identificação do artigo.|  
|**column_tracking**|**int**|Indica se o controle de coluna é implementado para o artigo.|  
|**status**|**tinyint**|Indica o status do artigo, que pode ser um dos seguintes:<br /><br /> **1** = não sincronizado – o script de processamento inicial para publicar a tabela será executado na próxima vez que o agente de instantâneo for executado.<br /><br /> **2** = ativo-o script de processamento inicial para publicar a tabela foi executado.|  
|**conflict_table**|**sysname**|O nome da tabela local que contém os registros conflitantes para o artigo atual. Essa tabela é somente informativa e seu conteúdo pode ser modificado ou excluído por rotinas de resolução de conflitos personalizadas ou diretamente pelo administrador.|  
|**creation_script**|**nvarchar (255)**|O script de criação para este artigo.|  
|**conflict_script**|**nvarchar (255)**|O script de conflito para este artigo.|  
|**article_resolver**|**nvarchar (255)**|O resolvedor de conflito para esse artigo.|  
|**ins_conflict_proc**|**sysname**|O procedimento usado para gravar informações de conflito na tabela de conflitos.|  
|**insert_proc**|**sysname**|O procedimento usado para inserir linhas durante a sincronização.|  
|**update_proc**|**sysname**|O procedimento usado para atualizar linhas durante a sincronização.|  
|**select_proc**|**sysname**|O nome de um procedimento armazenado gerado automaticamente que o Agente de Mesclagem usa para realizar bloqueio e localizar colunas e linhas para um artigo.|  
|**metadata_select_proc**|**sysname**|O nome do procedimento armazenado gerado automaticamente usado para acessar metadados nas tabelas de sistema de replicação de mesclagem.|  
|**delete_proc**|**sysname**|O procedimento usado para excluir linhas durante a sincronização.|  
|**schema_option**|**binário (8)**|O bitmap da opção de geração de esquema para o artigo determinado. Para obter informações sobre valores de *schema_option* com suporte, consulte [sp_addmergearticle &#40;&#41;do Transact-SQL ](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).|  
|**destination_object**|**sysname**|O nome da tabela criada no Assinante.|  
|**destination_owner**|**sysname**|O nome do proprietário do objeto de destino.|  
|**resolver_clsid**|**nvarchar (50)**|A ID do resolvedor de conflitos personalizado. Para um manipulador de lógica de negócios, este valor é NULL.|  
|**subset_filterclause**|**nvarchar (1000)**|A cláusula de filtro para este artigo.|  
|**missing_col_count**|**int**|O número de colunas publicadas que faltam no artigo.|  
|**missing_cols**|**varbinary(128)**|O bitmap que descreve as colunas que faltam no artigo.|  
|**excluded_cols**|**varbinary(128)**|O bitmap das colunas excluídas do artigo.|  
|**excluded_col_count**|**int**|O número de colunas excluídas do artigo.|  
|**Columns**|**varbinary(128)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**deleted_cols**|**varbinary(128)**|O bitmap que descreve as colunas excluídas do artigo.|  
|**resolver_info**|**nvarchar (255)**|O armazenamento de informações adicionais requeridas por resolvedores de conflitos personalizados.|  
|**view_sel_proc**|**nvarchar (290)**|O nome de um procedimento armazenado que o Agente de Mesclagem usa para fazer a população inicial de um artigo em uma publicação filtrada dinamicamente e para enumerar linhas alteradas em qualquer publicação filtrada.|  
|**gen_cur**|**bigint**|Gera número de alterações locais para a tabela base de um artigo.|  
|**vertical_partition**|**int**|Especifica se a filtragem de coluna está habilitada em um artigo de tabela. **0** indica que não há nenhuma filtragem vertical e publica todas as colunas.|  
|**identity_support**|**int**|Especifica se o tratamento automático do intervalo de identidades está habilitado. **1** significa que o tratamento de intervalo de identidade está habilitado e **0** significa que não há suporte para o intervalo de identidade.|  
|**before_image_objid**|**int**|A ID de objeto da tabela de controle. A tabela de controle contém certos valores de coluna de chave quando otimizações de alteração de partição foram habilitadas para a publicação.|  
|**before_view_objid**|**int**|A ID de objeto de uma tabela de exibição. A exibição está em uma tabela que controla se uma linha pertenceu a um Assinante específico antes de ser excluída ou atualizada. Só se aplica quando otimizações de alteração de partição foram habilitadas para a publicação.|  
|**verify_resolver_signature**|**int**|Especifica se uma assinatura digital é verificada antes de usar um resolvedor em replicação de mesclagem:<br /><br /> **0** = a assinatura não é verificada.<br /><br /> **1** = a assinatura é verificada para ver se ela é de uma fonte confiável.|  
|**allow_interactive_resolver**|**bit**|Especifica se o uso do Resolvedor Interativo em um artigo está habilitado. **1** significa que o resolvedor interativo pode ser usado no artigo.|  
|**fast_multicol_updateproc**|**bit**|Especifica se o Merge Agent foi habilitado para aplicar alterações em várias colunas na mesma linha em uma instrução UPDATE.<br /><br /> **0** = emite uma atualização separada para cada coluna alterada.<br /><br /> **1** = emitido na instrução UPDATE que faz com que as atualizações ocorram em várias colunas em uma instrução.|  
|**check_permissions**|**int**|O bitmap das permissões no nível de tabela que serão verificadas quando o Agente de Mesclagem aplicar alterações no Publicador. *check_permissions* pode ter um destes valores:<br /><br /> **0x00** = permissões não são verificadas.<br /><br /> **0x10** = verifica se as permissões no Publicador antes das inserções são feitas em um assinante podem ser carregadas.<br /><br /> **0x20** = verifica as permissões no Publicador antes que as atualizações feitas em um assinante possam ser carregadas.<br /><br /> **0x40** = verifica as permissões no Publicador antes que as exclusões feitas em um assinante possam ser carregadas.|  
|**maxversion_at_cleanup**|**int**|A geração máxima que é limpa na próxima execução do Agente de Mesclagem.|  
|**processing_order**|**int**|Indica a ordem de processamento dos artigos em uma publicação de mesclagem; em que um valor de **0** indica que o artigo não está ordenado, e os artigos são processados na ordem do valor mais baixo para o mais alto. Se dois artigos tiverem o mesmo valor, serão processados simultaneamente. Para obter mais informações, confira [propriedades de Especificar Replicação de Mesclagem](../../relational-databases/replication/merge/specify-merge-replication-properties.md).|  
|**upload_options**|**tinyint**|Define se as alterações poderão ser feitas ou carregadas do Assinante, que pode ser um dos valores a seguir.<br /><br /> **0** = não há restrições sobre as atualizações feitas no Assinante; todas as alterações são carregadas no Publicador.<br /><br /> **1** = as alterações são permitidas no Assinante, mas não são carregadas no Publicador.<br /><br /> **2** = as alterações não são permitidas no Assinante.|  
|**published_in_tran_pub**|**bit**|Indica que um artigo em uma publicação de mesclagem também é publicado em uma publicação transacional.<br /><br /> **0** = o artigo não é publicado em um artigo transacional.<br /><br /> **1** = o artigo também é publicado em um artigo transacional.|  
|**baixa**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**procname_postfix**|**nchar (32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**well_partitioned_lightweight**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**before_upd_view_objid**|**int**|A ID de exibição da tabela antes das atualizações.|  
|**delete_tracking**|**bit**|Indica se as exclusões são replicadas.<br /><br /> **0** = as exclusões não são replicadas.<br /><br /> **1** = as exclusões são replicadas, que é o comportamento padrão para replicação de mesclagem.<br /><br /> Quando o valor de *delete_tracking* for **0**, as linhas excluídas no Assinante deverão ser removidas manualmente no Publicador e as linhas excluídas no Publicador deverão ser removidas manualmente no Assinante.<br /><br /> Observação: um valor de **0** resulta em não convergência.|  
|**compensate_for_errors**|**bit**|Indica se ações de compensação são executadas quando são encontrados erros durante a sincronização.<br /><br /> **0** = ações de compensação estão desabilitadas.<br /><br /> **1** = alterações que não podem ser aplicadas em um assinante ou Publicador sempre levam a ações de compensação para desfazer essas alterações, que é o comportamento padrão para replicação de mesclagem.<br /><br /> Observação: um valor de **0** resulta em não convergência.|  
|**pub_range**|**bigint**|O tamanho do intervalo de identidade do publicador.|  
|**amplitude**|**bigint**|O tamanho dos valores de identidade consecutivos que seria atribuído a assinantes em um ajuste.|  
|**os**|**int**|A porcentagem de limite do intervalo de identidade.|  
|**stream_blob_columns**|**bit**|Indica se otimização de fluxo contínuo para colunas de objeto binário grande é usada. **1** significa que a otimização é tentada.|  
|**preserve_rowguidcol**|**bit**|Indica se a replicação usa uma coluna rowguid existente. Um valor de **1** significa que uma coluna ROWGUIDCOL existente é usada. **0** significa que a replicação adicionou a coluna ROWGUIDCOL.|  
|**partition_view_id**|**int**|Identifica a exibição que define uma partição de assinante.|  
|**repl_view_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**partition_deleted_view_rule**|**sysname**|A instrução usada em um gatilho de replicação de mesclagem para recuperar a ID de partição de cada linha excluída ou atualizada com base em seus valores antigos de coluna.|  
|**partition_inserted_view_rule**|**Sysname**|A instrução usada em um gatilho de replicação de mesclagem para recuperar a ID de partição de cada linha inserida ou atualizada com base em seus novos valores de coluna.|  
|**membership_eval_proc_name**|**sysname**|O nome do procedimento que avalia as IDs de partição atuais de linhas em [MSmerge_contents &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/msmerge-contents-transact-sql.md).|  
|**column_list**|**sysname**|Uma lista separada por vírgula de colunas publicadas no artigo.|  
|**column_list_blob**|**sysname**|Uma lista separada por vírgulas de colunas publicada em um artigo, incluindo colunas de objeto binário grande.|  
|**expand_proc**|**sysname**|O nome do procedimento que reavalia IDs de partição para todas as linhas filho de uma linha pai recém-inserida e para linhas pai que sofreram alteração de partição ou foram excluídas.|  
|**logical_record_parent_nickname**|**int**|O apelido de pai de alto nível de um determinado artigo em um registro lógico.|  
|**logical_record_view**|**int**|Uma exibição que produz o rowguid de artigo pai de alto nível correspondente a cada rowguid filho.|  
|**logical_record_deleted_view_rule**|**sysname**|Semelhante a **logical_record_view**, exceto pelo fato de que ele mostra linhas filho na tabela "Deleted" nos gatilhos Update e Delete.|  
|**logical_record_level_conflict_detection**|**bit**|Indica se os conflitos devem ser detectados no nível de registro lógico, ou no nível de linha ou coluna.<br /><br /> **0** = a detecção de conflito em nível de linha ou coluna é usada.<br /><br /> **1** = a detecção de conflito de registro lógico é usada, em que uma alteração em uma linha no Publicador e alterada em uma linha separada o mesmo registro lógico no assinante é tratada como um conflito.<br /><br /> Quando esse valor é 1, somente a resolução de conflito do nível de registro lógica pode ser usada.|  
|**logical_record_level_conflict_resolution**|**bit**|Indica se os conflitos devem ser resolvidos no nível de registro lógico ou no nível de linha ou coluna.<br /><br /> **0** = a resolução em nível de linha ou coluna é usada.<br /><br /> **1** = no caso de um conflito, o registro lógico inteiro do vencedor substitui todo o registro lógico no lado perdido.<br /><br /> Um valor 1 pode ser usado com detecção do nível de registro lógico e detecção de nível de coluna ou linha.|  
|**partition_options**|**tinyint**|Define a forma pela qual os dados no artigo são particionados, o que habilita otimizações de desempenho quando todas as linhas pertencem a apenas uma partição ou assinatura. O *partition_options* pode ser um dos valores a seguir.<br /><br /> **0** = a filtragem do artigo é estática ou não produz um subconjunto exclusivo de dados para cada partição, ou seja, uma partição de "sobreposição".<br /><br /> **1** = as partições estão sobrepostas e as atualizações DML feitas no Assinante não podem alterar a partição à qual uma linha pertence.<br /><br /> **2** = a filtragem do artigo produz partições não sobrepostas, mas vários assinantes podem receber a mesma partição.<br /><br /> **3** = a filtragem do artigo gera partições não sobrepostas que são exclusivas para cada assinatura.|  
|**name**|**sysname**|O nome da partição.|  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar partições para uma publicação de mesclagem com filtros com parâmetros](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)   
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addmergepartition](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpmergepartition](../../relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql.md)  
  
  
