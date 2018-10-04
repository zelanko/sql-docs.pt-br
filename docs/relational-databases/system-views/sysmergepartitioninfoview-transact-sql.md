---
title: sysmergepartitioninfoview (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
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
manager: craigg
ms.openlocfilehash: 75b68bd0699443c46be512520822b2faea0daed1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47762044"
---
# <a name="sysmergepartitioninfoview-transact-sql"></a>sysmergepartitioninfoview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **sysmergepartitioninfoview** exibição expõe informações de particionamento para artigos de tabela. Essa exibição é armazenada no banco de dados de publicação, no Publicador, e no banco de dados de assinatura, no Assinante.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|O nome do artigo.|  
|**type**|**tinyint**|Indica o tipo do artigo, que pode ser um dos seguintes:<br /><br /> **0x0A** = tabela.<br /><br /> **0x20** = somente esquema de procedimento.<br /><br /> **0x40** = somente esquema de exibição ou somente o esquema de exibição indexada.<br /><br /> **0x80** = somente esquema de função.|  
|**objid**|**int**|O identificador do objeto publicado.|  
|**sync_objid**|**int**|A ID de objeto da exibição que representa o conjunto de dados sincronizado.|  
|**view_type**|**tinyint**|O tipo da exibição.<br /><br /> **0** = não uma exibição; use todos os objetos base.<br /><br /> **1** = exibição permanente.<br /><br /> **2** = exibição temporária.|  
|**artid**|**uniqueidentifier**|O número de identificação exclusivo para o artigo determinado.|  
|**Descrição**|**nvarchar(255)**|A descrição breve do artigo.|  
|**pre_creation_command**|**tinyint**|A ação padrão a ser tomada quando o artigo é criado no banco de dados de assinatura:<br /><br /> **0** = nenhum - se a tabela já existir no assinante, nenhuma ação será tomada.<br /><br /> **1** = descartar - descarta a tabela antes de recriá-la.<br /><br /> **2** = excluir - emite uma exclusão com base na cláusula WHERE no filtro de subconjunto.<br /><br /> **3** = truncar - o mesmo que 2, mas exclui páginas em vez de linhas. Porém, não exige uma cláusula WHERE.|  
|**pubid**|**uniqueidentifier**|A ID da publicação à qual o artigo atual pertence.|  
|**Apelido**|**int**|O mapeamento de apelido para identificação do artigo.|  
|**column_tracking**|**int**|Indica se o controle de coluna é implementado para o artigo.|  
|**status**|**tinyint**|Indica o status do artigo, que pode ser um dos seguintes:<br /><br /> **1** = não sincronizado - o script de processamento inicial para publicar a tabela será executado na próxima vez em que o Snapshot Agent é executado.<br /><br /> **2** = ativo - o script de processamento inicial para publicar a tabela tiver sido executado.|  
|**conflict_table**|**sysname**|O nome da tabela local que contém os registros conflitantes para o artigo atual. Essa tabela é somente informativa e seu conteúdo pode ser modificado ou excluído por rotinas de resolução de conflitos personalizadas ou diretamente pelo administrador.|  
|**creation_script**|**nvarchar(255)**|O script de criação para este artigo.|  
|**conflict_script**|**nvarchar(255)**|O script de conflito para este artigo.|  
|**article_resolver**|**nvarchar(255)**|O resolvedor de conflito para esse artigo.|  
|**ins_conflict_proc**|**sysname**|O procedimento usado para gravar informações de conflito na tabela de conflitos.|  
|**insert_proc**|**sysname**|O procedimento usado para inserir linhas durante a sincronização.|  
|**update_proc**|**sysname**|O procedimento usado para atualizar linhas durante a sincronização.|  
|**select_proc**|**sysname**|O nome de um procedimento armazenado gerado automaticamente que o Agente de Mesclagem usa para realizar bloqueio e localizar colunas e linhas para um artigo.|  
|**metadata_select_proc**|**sysname**|O nome do procedimento armazenado gerado automaticamente usado para acessar metadados nas tabelas de sistema de replicação de mesclagem.|  
|**delete_proc**|**sysname**|O procedimento usado para excluir linhas durante a sincronização.|  
|**schema_option**|**binary(8)**|O bitmap da opção de geração de esquema para o artigo determinado. Para obter informações sobre suporte para *schema_option* valores, consulte [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).|  
|**destination_object**|**sysname**|O nome da tabela criada no Assinante.|  
|**destination_owner**|**sysname**|O nome do proprietário do objeto de destino.|  
|**resolver_clsid**|**nvarchar(50)**|A ID do resolvedor de conflitos personalizado. Para um manipulador de lógica de negócios, este valor é NULL.|  
|**subset_filterclause**|**nvarchar(1000)**|A cláusula de filtro para este artigo.|  
|**missing_col_count**|**int**|O número de colunas publicadas que faltam no artigo.|  
|**missing_cols**|**varbinary(128)**|O bitmap que descreve as colunas que faltam no artigo.|  
|**excluded_cols**|**varbinary(128)**|O bitmap das colunas excluídas do artigo.|  
|**excluded_col_count**|**int**|O número de colunas excluídas do artigo.|  
|**columns**|**varbinary(128)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**deleted_cols**|**varbinary(128)**|O bitmap que descreve as colunas excluídas do artigo.|  
|**resolver_info**|**nvarchar(255)**|O armazenamento de informações adicionais requeridas por resolvedores de conflitos personalizados.|  
|**view_sel_proc**|**nvarchar(290)**|O nome de um procedimento armazenado que o Agente de Mesclagem usa para fazer a população inicial de um artigo em uma publicação filtrada dinamicamente e para enumerar linhas alteradas em qualquer publicação filtrada.|  
|**gen_cur**|**bigint**|Gera número de alterações locais para a tabela base de um artigo.|  
|**vertical_partition**|**int**|Especifica se a filtragem de coluna está habilitada em um artigo de tabela. **0** indica que não há filtragem vertical e publica todas as colunas.|  
|**identity_support**|**int**|Especifica se o tratamento de intervalo de identidade automático está habilitado. **1** significa que a manipulação de intervalo de identidade é habilitada, e **0** significa que não há nenhuma identidade de intervalo de suporte.|  
|**before_image_objid**|**int**|A ID de objeto da tabela de controle. A tabela de controle contém certos valores de coluna de chave quando otimizações de alteração de partição foram habilitadas para a publicação.|  
|**before_view_objid**|**int**|A ID de objeto de uma tabela de exibição. A exibição está em uma tabela que controla se uma linha pertenceu a um Assinante específico antes de ser excluída ou atualizada. Só se aplica quando otimizações de alteração de partição foram habilitadas para a publicação.|  
|**verify_resolver_signature**|**int**|Especifica se uma assinatura digital é verificada antes de usar um resolvedor em replicação de mesclagem:<br /><br /> **0** = assinatura não é verificada.<br /><br /> **1** = assinatura é verificada para ver se ele é de uma fonte confiável.|  
|**allow_interactive_resolver**|**bit**|Especifica se o uso do Resolvedor Interativo em um artigo está habilitado. **1** significa que o resolvedor interativo pode ser usado no artigo.|  
|**fast_multicol_updateproc**|**bit**|Especifica se o Merge Agent foi habilitado para aplicar alterações em várias colunas na mesma linha em uma instrução UPDATE.<br /><br /> **0** = problemas uma UPDATE separada para cada coluna alterada.<br /><br /> **1** = emitido em instrução UPDATE que faz com que as atualizações ocorram em várias colunas em uma instrução.|  
|**check_permissions**|**int**|O bitmap das permissões no nível de tabela que serão verificadas quando o Agente de Mesclagem aplicar alterações no Publicador. *check_permissions* pode ter um destes valores:<br /><br /> **0x00** = as permissões não são verificadas.<br /><br /> **0x10** = verifica permissões no publicador antes que INSERTs feitas no assinante sejam carregadas.<br /><br /> **0x20** = verifica permissões no publicador antes que as atualizações feitas no assinante sejam carregadas.<br /><br /> **0x40** = verifica permissões no publicador antes que DELETEs feitas no assinante sejam carregadas.|  
|**maxversion_at_cleanup**|**int**|A geração máxima que é limpa na próxima execução do Agente de Mesclagem.|  
|**processing_order**|**int**|Indica a ordem de processamento de artigos em uma publicação de mesclagem; onde um valor de **0** indica que o artigo não está ordenado e artigos são processados na ordem do menor para o maior valor. Se dois artigos tiverem o mesmo valor, serão processados simultaneamente. Para obter mais informações, consulte [Especificar a ordem de processamento dos artigos de mesclagem](../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md).|  
|**upload_options**|**tinyint**|Define se as alterações poderão ser feitas ou carregadas do Assinante, que pode ser um dos valores a seguir.<br /><br /> **0** = não há restrições em atualizações feitas no assinante; todas as alterações são carregadas no publicador.<br /><br /> **1** = as alterações são permitidas no assinante, mas eles não são carregados no publicador.<br /><br /> **2** = as alterações não são permitidas no assinante.|  
|**published_in_tran_pub**|**bit**|Indica que um artigo em uma publicação de mesclagem também é publicado em uma publicação transacional.<br /><br /> **0** = o artigo não é publicado em um artigo transacional.<br /><br /> **1** = o artigo também é publicado em um artigo transacional.|  
|**lightweight**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**procname_postfix**|**nchar(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**well_partitioned_lightweight**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**before_upd_view_objid**|**int**|A ID de exibição da tabela antes das atualizações.|  
|**delete_tracking**|**bit**|Indica se as exclusões são replicadas.<br /><br /> **0** = exclusões não são replicadas.<br /><br /> **1** = as exclusões são replicadas, que é o comportamento padrão para replicação de mesclagem.<br /><br /> Quando o valor de *delete_tracking* é **0**, linhas excluídas no assinante devem ser removidas manualmente no publicador e linhas excluídas no publicador devem ser removidas manualmente no assinante.<br /><br /> Observação: Um valor de **0** resulta em não convergência.|  
|**compensate_for_errors**|**bit**|Indica se ações de compensação são executadas quando são encontrados erros durante a sincronização.<br /><br /> **0** = Compensating ações estão desabilitadas.<br /><br /> **1** = as alterações que não podem ser aplicadas em um assinante ou publicador sempre conduzem a ações de compensação para desfazer essas alterações, que é o comportamento padrão para replicação de mesclagem.<br /><br /> Observação: Um valor de **0** resulta em não convergência.|  
|**pub_range**|**bigint**|O tamanho do intervalo de identidade do publicador.|  
|**range**|**bigint**|O tamanho dos valores de identidade consecutivos que seria atribuído a assinantes em um ajuste.|  
|**threshold**|**int**|A porcentagem de limite do intervalo de identidade.|  
|**stream_blob_columns**|**bit**|Indica se otimização de fluxo contínuo para colunas de objeto binário grande é usada. **1** significa que a otimização é tentada.|  
|**preserve_rowguidcol**|**bit**|Indica se a replicação usa uma coluna rowguid existente. Um valor de **1** significa que uma coluna ROWGUIDCOL existente é usada. **0** significa que a replicação adicionou a coluna ROWGUIDCOL.|  
|**partition_view_id**|**int**|Identifica a exibição que define uma partição de assinante.|  
|**repl_view_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**partition_deleted_view_rule**|**sysname**|A instrução usada em um gatilho de replicação de mesclagem para recuperar a ID de partição de cada linha excluída ou atualizada com base em seus valores antigos de coluna.|  
|**partition_inserted_view_rule**|**sysname**|A instrução usada em um gatilho de replicação de mesclagem para recuperar a ID de partição de cada linha inserida ou atualizada com base em seus novos valores de coluna.|  
|**membership_eval_proc_name**|**sysname**|O nome do procedimento que avalia a ID de partição atual de linhas no [MSmerge_contents &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-contents-transact-sql.md).|  
|**column_list**|**sysname**|Uma lista separada por vírgula de colunas publicadas no artigo.|  
|**column_list_blob**|**sysname**|Uma lista separada por vírgulas de colunas publicada em um artigo, incluindo colunas de objeto binário grande.|  
|**expand_proc**|**sysname**|O nome do procedimento que reavalia IDs de partição para todas as linhas filho de uma linha pai recém-inserida e para linhas pai que sofreram alteração de partição ou foram excluídas.|  
|**logical_record_parent_nickname**|**int**|O apelido de pai de alto nível de um determinado artigo em um registro lógico.|  
|**logical_record_view**|**int**|Uma exibição que produz o rowguid de artigo pai de alto nível correspondente a cada rowguid filho.|  
|**logical_record_deleted_view_rule**|**sysname**|Semelhante ao **logical_record_view**, exceto que ele mostra linhas filho na tabela "excluída" em atualizar e excluir gatilhos.|  
|**logical_record_level_conflict_detection**|**bit**|Indica se os conflitos devem ser detectados no nível de registro lógico, ou no nível de linha ou coluna.<br /><br /> **0** = a linha ou coluna nível - detecção de conflito é usada.<br /><br /> **1** = lógico detecção de conflitos de registro é usada, em que uma alteração em uma linha no publicador e a alteração em um separado de linha a mesma lógica registro no assinante é tratado como um conflito.<br /><br /> Quando esse valor é 1, somente a resolução de conflito do nível de registro lógica pode ser usada.|  
|**logical_record_level_conflict_resolution**|**bit**|Indica se os conflitos devem ser resolvidos no nível de registro lógico ou no nível de linha ou coluna.<br /><br /> **0** = coluna-nível de linha ou a resolução é usada.<br /><br /> **1** = no caso de um conflito, todo o registro lógico do vencedor sobrescreve todo o registro lógico do lado perdedor.<br /><br /> Um valor 1 pode ser usado com detecção do nível de registro lógico e detecção de nível de coluna ou linha.|  
|**partition_options**|**tinyint**|Define a forma pela qual os dados no artigo são particionados, o que habilita otimizações de desempenho quando todas as linhas pertencem a apenas uma partição ou assinatura. O *partition_options* pode ser um dos valores a seguir.<br /><br /> **0** = a filtragem para o artigo ou é estática ou não produz um único subconjunto de dados para cada partição, ou seja, uma partição "sobreposta".<br /><br /> **1** = as partições são sobrepostas e as atualizações DML feitas no assinante não podem alterar a partição à qual uma linha pertence.<br /><br /> **2** = a filtragem para o artigo gera partições não sobrepostas, mas vários assinantes podem receber a mesma partição.<br /><br /> **3** = a filtragem para o artigo gera partições não sobrepostas exclusivas de cada assinatura.|  
|**name**|**sysname**|O nome da partição.|  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar partições para uma publicação de mesclagem com filtros com parâmetros](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)   
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addmergepartition &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)   
 [sp_helpmergepartition &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql.md)  
  
  
