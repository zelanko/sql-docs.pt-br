---
title: sp_helparticle (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helparticle_TSQL
- sp_helparticle
helpviewer_keywords:
- sp_helparticle
ms.assetid: 9c4a1a88-56f1-45a0-890c-941b8e0f0799
author: stevestein
ms.author: sstein
ms.openlocfilehash: cffdecba62283e3fc404c3630866467bc3a2b1c1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084988"
---
# <a name="sphelparticle-transact-sql"></a>sp_helparticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe informações sobre um artigo. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador. Para Editores Oracle, esse procedimento armazenado é executado no Distribuidor, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helparticle [ @publication = ] 'publication'   
    [ , [ @article = ] 'article' ]  
    [ , [ @returnfilter = ] returnfilter ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @found = ] found OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação. *publicação* está **sysname**, sem padrão.  
  
`[ @article = ] 'article'` É o nome de um artigo na publicação. *artigo* está **sysname**, com um padrão de **%** . Se *artigo* não é fornecido, informações sobre todos os artigos da publicação especificada serão retornadas.  
  
`[ @returnfilter = ] returnfilter` Especifica se a cláusula de filtro deve ser retornada. *returnfilter* está **bit**, com um padrão de **1**, que retorna a cláusula de filtro.  
  
`[ @publisher = ] 'publisher'` Especifica um não [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador. *Publisher* está **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  *Publisher* não deve ser especificado quando solicitar informações sobre um artigo publicado por um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
`[ @found = ] found OUTPUT` Somente para uso interno.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id do artigo**|**int**|ID do artigo.|  
|**nome do artigo**|**sysname**|Nome do artigo.|  
|**objeto base**|**nvarchar(257)**|Nome da tabela subjacente representado pelo artigo ou procedimento armazenado.|  
|**objeto de destino**|**sysname**|Nome da tabela de destino (assinatura).|  
|**objeto de sincronização**|**nvarchar(257)**|Nome da exibição que define o artigo publicado.|  
|**type**|**smallint**|O tipo de artigo:<br /><br /> **1** = baseado em log.<br /><br /> **3** = baseado em log com filtro manual.<br /><br /> **5** = baseado em log com exibição manual.<br /><br /> **7** = baseado em log com filtro manual e exibição manual.<br /><br /> **8** = execução de procedimento armazenado.<br /><br /> **24** = a execução do procedimento armazenado serializável.<br /><br /> **32** = procedimento armazenado (somente esquema).<br /><br /> **64** = exibição (somente esquema).<br /><br /> **96** = função de agregação (somente esquema).<br /><br /> **128** = função (somente esquema).<br /><br /> **257** = a exibição indexada baseado em log.<br /><br /> **259** = exibição indexada baseado em log com filtro manual.<br /><br /> **261** = a exibição indexada baseado em log com exibição manual.<br /><br /> **263** = a exibição indexada baseado em log com filtro manual e exibição manual.<br /><br /> **320** = a exibição indexada (somente esquema).<br /><br />|  
|**status**|**tinyint**|Pode ser o [& (AND bit a bit)](../../t-sql/language-elements/bitwise-and-transact-sql.md) resultado de uma ou mais ou destas propriedades do artigo:<br /><br /> **0x00** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> **0x01** = artigo está ativo.<br /><br /> **0x08** = incluir o nome da coluna em instruções insert.<br /><br /> **0x16** = usar instruções com parâmetros.<br /><br /> **0x32** = usar instruções com parâmetros e incluir o nome da coluna em instruções insert.|  
|**filter**|**nvarchar(257)**|Procedimento armazenado usado para filtrar a tabela horizontalmente. Esse procedimento armazenado deve ter sido criado usando a cláusula FOR REPLICATION.|  
|**description**|**nvarchar(255)**|Entrada descritiva para o artigo.|  
|**insert_command**|**nvarchar(255)**|O tipo de comando de replicação usado ao replicar inserções com artigos de tabela. Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**update_command**|**nvarchar(255)**|O tipo de comando de replicação usado ao replicar atualizações com artigos de tabela. Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**delete_command**|**nvarchar(255)**|O tipo de comando de replicação usado ao replicar exclusões com artigos de tabela. Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**caminho do script de criação**|**nvarchar(255)**|Caminho e nome de um script de esquema de artigo usados para criar tabelas de destino.|  
|**partição vertical**|**bit**|É se o particionamento vertical está habilitado para o artigo; onde um valor de **1** significa que o particionamento vertical está habilitado.|  
|**pre_creation_cmd**|**tinyint**|Comando de pré-criação para DROP TABLE, DELETE TABLE ou TRUNCATE TABLE.|  
|**filter_clause**|**ntext**|Cláusula WHERE especificando filtragem horizontal.|  
|**schema_option**|**binary(8)**|Bitmap da opção de geração de esquema para o artigo determinado. Para obter uma lista completa dos **schema_option** valores, consulte [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).|  
|**dest_owner**|**sysname**|Nome do proprietário do objeto de destino.|  
|**source_owner**|**sysname**|Proprietário do objeto de origem.|  
|**unqua_source_object**|**sysname**|Nome do objeto de origem, sem o nome do proprietário.|  
|**sync_object_owner**|**sysname**|Proprietário da exibição que define o artigo publicado. .|  
|**unqualified_sync_object**|**sysname**|Nome da exibição que define o artigo publicado, sem o nome do proprietário.|  
|**filter_owner**|**sysname**|Proprietário do filtro.|  
|**unqua_filter**|**sysname**|Nome do filtro, sem o nome do proprietário.|  
|**auto_identity_range**|**int**|Sinalizador que indica se o tratamento de um intervalo de identidade automático foi ativado na publicação no momento em que foi criado. **1** significa que o intervalo de identidade automático está habilitado; **0** significa que ele está desabilitado.|  
|**publisher_identity_range**|**int**|Intervalo de tamanho do intervalo de identidade no publicador se o artigo tiver *identityrangemanagementoption* definido como **automática** ou **auto_identity_range** definido como  **True**.|  
|**identity_range**|**bigint**|Intervalo de tamanho do intervalo de identidade no assinante se o artigo tiver *identityrangemanagementoption* definido como **automática** ou **auto_identity_range** definido como  **True**.|  
|**threshold**|**bigint**|Valor de porcentagem que indica quando o Distribution Agent atribui um novo intervalo de identidade.|  
|**identityrangemanagementoption**|**int**|Indica o gerenciamento de intervalo de identidade tratado para o artigo.|  
|**fire_triggers_on_snapshot**|**bit**|Se os gatilhos de usuário replicados forem executados quando o instantâneo inicial for aplicado.<br /><br /> **1** = gatilhos de usuário são executados.<br /><br /> **0** = usuário gatilhos não são executados.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helparticle** é usado em replicação de instantâneo e replicação transacional.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa, o **db_owner** função fixa de banco de dados ou a lista de acesso à publicação para a publicação atual pode executar **sp_helparticle**.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_helptranarticle](../../relational-databases/replication/codesnippet/tsql/sp-helparticle-transact-_1.sql)]  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar propriedades do artigo](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
