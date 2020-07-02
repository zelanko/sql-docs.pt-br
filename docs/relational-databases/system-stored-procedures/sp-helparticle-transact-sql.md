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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e863c10b3f2086d6318d6c53b599c7ad186572c6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85634227"
---
# <a name="sp_helparticle-transact-sql"></a>sp_helparticle (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Exibe informações sobre um artigo. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador. Para Editores Oracle, esse procedimento armazenado é executado no Distribuidor, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helparticle [ @publication = ] 'publication'   
    [ , [ @article = ] 'article' ]  
    [ , [ @returnfilter = ] returnfilter ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @found = ] found OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @article = ] 'article'`É o nome de um artigo na publicação. o *artigo* é **sysname**, com um padrão de **%** . Se o *artigo* não for fornecido, serão retornadas informações sobre todos os artigos da publicação especificada.  
  
`[ @returnfilter = ] returnfilter`Especifica se a cláusula de filtro deve ser retornada. *returnfilter* é **bit**, com um padrão de **1**, que retorna a cláusula de filtro.  
  
`[ @publisher = ] 'publisher'`Especifica um não [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o *Publicador* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  o *Publicador* não deve ser especificado ao solicitar informações sobre um artigo publicado por um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador.  
  
`[ @found = ] found OUTPUT`Somente para uso interno.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**ID do artigo**|**int**|ID do artigo.|  
|**article name**|**sysname**|Nome do artigo.|  
|**objeto base**|**nvarchar (257)**|Nome da tabela subjacente representado pelo artigo ou procedimento armazenado.|  
|**objeto de destino**|**sysname**|Nome da tabela de destino (assinatura).|  
|**synchronization object**|**nvarchar (257)**|Nome da exibição que define o artigo publicado.|  
|**type**|**smallint**|O tipo de artigo:<br /><br /> **1** = baseado em log.<br /><br /> **3** = baseado em log com o filtro manual.<br /><br /> **5** = baseado em log com exibição manual.<br /><br /> **7** = baseado em log com filtro manual e exibição manual.<br /><br /> **8** = execução de procedimento armazenado.<br /><br /> **24** = execução de procedimento armazenado serializável.<br /><br /> **32** = procedimento armazenado (somente esquema).<br /><br /> **64** = exibição (somente esquema).<br /><br /> **96** = função de agregação (somente esquema).<br /><br /> **128** = função (somente esquema).<br /><br /> **257** = exibição indexada baseada em log.<br /><br /> **259** = exibição indexada baseada em log com filtro manual.<br /><br /> **261** = exibição indexada baseada em log com exibição manual.<br /><br /> **263** = exibição indexada baseada em log com filtro manual e exibição manual.<br /><br /> **320** = exibição indexada (somente esquema).<br /><br />|  
|**status**|**tinyint**|Pode ser o resultado de [& (e bit e)](../../t-sql/language-elements/bitwise-and-transact-sql.md) de uma ou mais ou essas propriedades de artigo:<br /><br /> **0x00** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> **0x01** = o artigo está ativo.<br /><br /> **0x08** = incluir o nome da coluna em instruções INSERT.<br /><br /> **0x16** = usar instruções parametrizadas.<br /><br /> **0x32** = use instruções parametrizadas e inclua o nome da coluna em instruções INSERT.|  
|**sem**|**nvarchar (257)**|Procedimento armazenado usado para filtrar a tabela horizontalmente. Esse procedimento armazenado deve ter sido criado usando a cláusula FOR REPLICATION.|  
|**ndescrição**|**nvarchar (255)**|Entrada descritiva para o artigo.|  
|**insert_command**|**nvarchar (255)**|O tipo de comando de replicação usado ao replicar inserções com artigos de tabela. Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**update_command**|**nvarchar (255)**|O tipo de comando de replicação usado ao replicar atualizações com artigos de tabela. Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**delete_command**|**nvarchar (255)**|O tipo de comando de replicação usado ao replicar exclusões com artigos de tabela. Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**creation script path**|**nvarchar (255)**|Caminho e nome de um script de esquema de artigo usados para criar tabelas de destino.|  
|**vertical partition**|**bit**|Se o particionamento vertical está habilitado para o artigo; em que um valor de **1** significa que o particionamento vertical está habilitado.|  
|**pre_creation_cmd**|**tinyint**|Comando de pré-criação para DROP TABLE, DELETE TABLE ou TRUNCATE TABLE.|  
|**filter_clause**|**ntext**|Cláusula WHERE especificando filtragem horizontal.|  
|**schema_option**|**binário (8)**|Bitmap da opção de geração de esquema para o artigo determinado. Para obter uma lista completa de valores de **schema_option** , consulte [sp_addarticle &#40;&#41;do Transact-SQL ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).|  
|**dest_owner**|**sysname**|Nome do proprietário do objeto de destino.|  
|**source_owner**|**sysname**|Proprietário do objeto de origem.|  
|**unqua_source_object**|**sysname**|Nome do objeto de origem, sem o nome do proprietário.|  
|**sync_object_owner**|**sysname**|Proprietário da exibição que define o artigo publicado. .|  
|**unqualified_sync_object**|**sysname**|Nome da exibição que define o artigo publicado, sem o nome do proprietário.|  
|**filter_owner**|**sysname**|Proprietário do filtro.|  
|**unqua_filter**|**sysname**|Nome do filtro, sem o nome do proprietário.|  
|**auto_identity_range**|**int**|Sinalizador que indica se o tratamento de um intervalo de identidade automático foi ativado na publicação no momento em que foi criado. **1** significa que o intervalo de identidade automático está habilitado; **0** significa que ele está desabilitado.|  
|**publisher_identity_range**|**int**|Tamanho do intervalo do intervalo de identidade no Publicador se o artigo tiver *identityrangemanagementoption* definido como **auto** ou **auto_identity_range** definido como **true**.|  
|**identity_range**|**bigint**|Tamanho do intervalo do intervalo de identidade no Assinante se o artigo tiver *identityrangemanagementoption* definido como **auto** ou **auto_identity_range** definido como **true**.|  
|**threshold**|**bigint**|Valor de porcentagem que indica quando o Distribution Agent atribui um novo intervalo de identidade.|  
|**identityrangemanagementoption**|**int**|Indica o gerenciamento de intervalo de identidade tratado para o artigo.|  
|**fire_triggers_on_snapshot**|**bit**|Se os gatilhos de usuário replicados forem executados quando o instantâneo inicial for aplicado.<br /><br /> **1** = gatilhos de usuário são executados.<br /><br /> **0** = os gatilhos de usuário não são executados.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helparticle** é usado na replicação de instantâneo e na replicação transacional.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** , a função de banco de dados fixa **db_owner** ou a lista de acesso à publicação da publicação atual podem ser executados **sp_helparticle**.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_helptranarticle](../../relational-databases/replication/codesnippet/tsql/sp-helparticle-transact-_1.sql)]  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e modificar propriedades do artigo](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [&#41;&#40;Transact-SQL de sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changearticle](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_droparticle](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
