---
title: sp_articleview (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_articleview
- sp_articleview_TSQL
helpviewer_keywords:
- sp_articleview
ms.assetid: a3d63fd6-f360-4a2f-8a82-a0dc15f650b3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 10c46ac2ff35d73453976a91276246d3e810e425
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62997980"
---
# <a name="sparticleview-transact-sql"></a>sp_articleview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria a exibição que define o artigo publicado, quando uma tabela é filtrada verticalmente ou horizontalmente. Essa exibição é usada como a fonte filtrada de esquema e dados para as tabelas de destino. Somente artigos não assinados podem ser modificados por esse procedimento armazenado. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_articleview [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @view_name = ] 'view_name']  
    [ , [ @filter_clause = ] 'filter_clause']  
    [ , [ @change_active = ] change_active ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @refreshsynctranprocs = ] refreshsynctranprocs ]  
    [ , [ @internal = ] internal ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação que contém o artigo. *publicação* está **sysname**, sem padrão.  
  
`[ @article = ] 'article'` É o nome do artigo. *artigo* está **sysname**, sem padrão.  
  
`[ @view_name = ] 'view_name'` É o nome da exibição que define o artigo publicado. *view_name* está **nvarchar(386)** , com um padrão NULL.  
  
`[ @filter_clause = ] 'filter_clause'` É uma restrição cláusula (WHERE) que define um filtro horizontal. Ao inserir a cláusula de restrição, omita a palavra-chave WHERE. *filter_clause* está **ntext**, com um padrão NULL.  
  
`[ @change_active = ] change_active` Permite modificar as colunas em publicações que têm assinaturas. *change_active* é um **int**, com um padrão de **0**. Se **0**, colunas não são alteradas. Se **1**, modos de exibição podem ser criados ou recriados em artigos ativos que têm assinaturas.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` Confirma que a ação tomada por esse procedimento armazenado pode invalidar um instantâneo existente. *force_invalidate_snapshot* é um **bit**, com um padrão de **0**.  
  
 **0** Especifica que as alterações no artigo fazem com que o instantâneo seja inválido. Se o procedimento armazenado detectar que a alteração requer um novo instantâneo, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** Especifica que as alterações no artigo podem invalidar o instantâneo ser inválida e se houver assinaturas existentes que exigem um novo instantâneo, dará permissão para o instantâneo existente seja marcado como obsoleto e um novo instantâneo seja gerado.  
  
`[ @force_reinit_subscription = ] _force_reinit_subscription_` Reconhece que a ação tomada por esse procedimento armazenado pode requerer que as assinaturas existentes sejam reinicializadas. *force_reinit_subscription* é um **bit** com um padrão de **0**.  
  
 **0** Especifica que as alterações no artigo fazem com que a assinatura seja reiniciada. Se o procedimento armazenado detectar que a alteração irá requerer assinaturas sejam reiniciadas, ocorrerá um erro e nenhuma alteração é feita.  
  
 **1** Especifica que as alterações no artigo faz com que uma assinatura existente seja reiniciada e dá permissão para que ocorra a reinicialização da assinatura.  
  
`[ @publisher = ] 'publisher'` Especifica um não [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador. *Publisher* está **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  *Publisher* não deve ser usado durante a publicação de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
`[ @refreshsynctranprocs = ] refreshsynctranprocs` É se os procedimentos armazenados usados para sincronizar replicações são recriados automaticamente. *refreshsynctranprocs* está **bit**, com um padrão de 1.  
  
 **1** significa que os procedimentos armazenados são recriados.  
  
 **0** significa que os procedimentos armazenados não são recriados.  
  
`[ @internal = ] internal` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_articleview** cria a exibição que define o artigo publicado e insere a ID dessa exibição na **sync_objid** coluna o [sysarticles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) tabela e, em seguida, insere o texto da cláusula de restrição na **filter_clause** coluna. Se todas as colunas são replicadas e não há nenhuma **filter_clause**, o **sync_objid** no [sysarticles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) tabela está definida como a ID das tabela base e o uso de **sp_articleview** não é necessária.  
  
 Para publicar uma tabela filtrada verticalmente (ou seja, para filtrar colunas) executado pela primeira vez **sp_addarticle** sem nenhum *sync_object* parâmetro, execute [sp_articlecolumn &#40;&#41; ](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) uma vez para cada coluna a ser replicada (definindo o filtro vertical) e, em seguida, execute **sp_articleview** para criar o modo de exibição que define o artigo publicado.  
  
 Para publicar uma tabela horizontalmente filtrada (ou seja, para filtrar linhas), execute [sp_addarticle &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) sem nenhum *filtro* parâmetro. Execute [sp_articlefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md), fornecendo todos os parâmetros incluindo *filter_clause*. Em seguida, execute **sp_articleview**, fornecendo todos os parâmetros incluindo idênticas *filter_clause*.  
  
 Para publicar uma tabela filtrada verticalmente e horizontalmente, execute [sp_addarticle &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) sem nenhum *sync_object* ou *filtro* parâmetros. Execute [sp_articlecolumn &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) uma vez para cada coluna a serem replicados e, em seguida, execute [sp_articlefilter &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) e **SP _ articleview**.  
  
 Se o artigo já tiver uma exibição que define o artigo publicado, **sp_articleview** descarta o modo de exibição existente e cria um novo automaticamente. Se o modo de exibição foi criado manualmente (**tipo** na [sysarticles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) é **5**), o modo de exibição existente não será descartado.  
  
 Se você criar um procedimento armazenado de filtro personalizado e uma exibição que define o artigo publicado manualmente, não execute **sp_articleview**. Em vez disso, forneça esses como os *filtro* e *sync_object* parâmetros a serem [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), juntamente com o apropriado*tipo* valor.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articleview-transact-_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_articleview**.  
  
## <a name="see-also"></a>Consulte também  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Definir e modificar um filtro de linha estático](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
