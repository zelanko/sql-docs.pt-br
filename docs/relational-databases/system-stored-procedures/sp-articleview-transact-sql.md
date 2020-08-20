---
description: sp_articleview (Transact-SQL)
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5b1d18b8e4249f2948dccb3b042742afe0c0f54a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464522"
---
# <a name="sp_articleview-transact-sql"></a>sp_articleview (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Cria a exibição que define o artigo publicado, quando uma tabela é filtrada verticalmente ou horizontalmente. Essa exibição é usada como a fonte filtrada de esquema e dados para as tabelas de destino. Somente artigos não assinados podem ser modificados por esse procedimento armazenado. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publication = ] 'publication'` É o nome da publicação que contém o artigo. a *publicação* é **sysname**, sem padrão.  
  
`[ @article = ] 'article'` É o nome do artigo. o *artigo* é **sysname**, sem padrão.  
  
`[ @view_name = ] 'view_name'` É o nome da exibição que define o artigo publicado. *view_name* é **nvarchar (386)**, com um padrão de NULL.  
  
`[ @filter_clause = ] 'filter_clause'` É uma cláusula de restrição (WHERE) que define um filtro horizontal. Ao inserir a cláusula de restrição, omita a palavra-chave WHERE. *filter_clause* é **ntext**, com um padrão de NULL.  
  
`[ @change_active = ] change_active` Permite modificar as colunas em publicações que têm assinaturas. *change_active* é um **int**, com um padrão de **0**. Se **0**, as colunas não serão alteradas. Se **1**, as exibições poderão ser criadas ou recriadas em artigos ativos que tenham assinaturas.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` O reconhece que a ação executada por esse procedimento armazenado pode invalidar um instantâneo existente. *force_invalidate_snapshot* é um **bit**, com um padrão de **0**.  
  
 **0** especifica que as alterações no artigo não fazem com que o instantâneo seja inválido. Se o procedimento armazenado detectar que a alteração requer um novo instantâneo, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** especifica que as alterações no artigo podem fazer com que o instantâneo seja inválido e, se houver assinaturas existentes que exijam um novo instantâneo, concederá permissão para o instantâneo existente ser marcado como obsoleto e um novo instantâneo gerado.  
  
`[ @force_reinit_subscription = ] _force_reinit_subscription_` Reconhece que a ação executada por este procedimento armazenado pode exigir que as assinaturas existentes sejam reinicializadas. *force_reinit_subscription* é um **bit** com um padrão de **0**.  
  
 **0** especifica que as alterações no artigo não fazem com que a assinatura seja reinicializada. Se o procedimento armazenado detectar que a alteração exigiria que as assinaturas fossem reinicializadas, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** especifica que as alterações no artigo fazem com que a assinatura existente seja reinicializada e dá permissão para que a reinicialização da assinatura ocorra.  
  
`[ @publisher = ] 'publisher'` Especifica um não [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o *Publicador* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  o *Publicador* não deve ser usado ao publicar a partir de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador.  
  
`[ @refreshsynctranprocs = ] refreshsynctranprocs` É se os procedimentos armazenados usados para sincronizar a replicação são recriados automaticamente. *refreshsynctranprocs* é **bit**, com um padrão de 1.  
  
 **1** significa que os procedimentos armazenados são recriados.  
  
 **0** significa que os procedimentos armazenados não são recriados.  
  
`[ @internal = ] internal` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_articleview** cria a exibição que define o artigo publicado e insere a ID dessa exibição na coluna **sync_objid** do [sysarticles &#40;tabela de&#41;Transact-SQL ](../../relational-databases/system-tables/sysarticles-transact-sql.md) e insere o texto da cláusula de restrição na coluna **filter_clause** . Se todas as colunas forem replicadas e não houver **filter_clause**, a **sync_objid** no [sysarticles &#40;tabela de&#41;de Transact-SQL ](../../relational-databases/system-tables/sysarticles-transact-sql.md) será definida como a ID da tabela base e o uso de **sp_articleview** não será necessário.  
  
 Para publicar uma tabela filtrada verticalmente (ou seja, para filtrar colunas) primeiro execute **sp_addarticle** sem *sync_object* parâmetro, execute [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) uma vez para cada coluna a ser replicada (definindo o filtro vertical) e, em seguida, execute **sp_articleview** para criar a exibição que define o artigo publicado.  
  
 Para publicar uma tabela filtrada horizontalmente (ou seja, para filtrar linhas), execute [sp_addarticle &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) sem parâmetro de *filtro* . Execute [sp_articlefilter &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md), fornecendo todos os parâmetros, incluindo *filter_clause*. Em seguida, execute **sp_articleview**, fornecendo todos os parâmetros, incluindo os *filter_clause*idênticos.  
  
 Para publicar uma tabela filtrada vertical e horizontalmente, execute [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) sem parâmetros de *sync_object* ou de *filtro* . Execute [sp_articlecolumn &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) uma vez para cada coluna a ser replicada e, em seguida, execute sp_articlefilter **&#40;&#41;e SP_ARTICLEVIEW** [Transact-SQL](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) .  
  
 Se o artigo já tiver uma exibição que define o artigo publicado, **sp_articleview** descartará a exibição existente e criará uma nova automaticamente. Se a exibição foi criada manualmente (**tipo** no [sysarticles &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysarticles-transact-sql.md) é **5**), a exibição existente não será descartada.  
  
 Se você criar um procedimento armazenado de filtro personalizado e uma exibição que define o artigo publicado manualmente, não execute **sp_articleview**. Em vez disso, forneça esses parâmetros como *filtro* e *sync_object* para [sp_addarticle &#40;&#41;do Transact-SQL ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), juntamente com o valor do *tipo* apropriado.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articleview-transact-_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_articleview**.  
  
## <a name="see-also"></a>Consulte Também  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Definir e modificar um filtro de linha estático](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [&#41;&#40;Transact-SQL de sp_addarticle ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_articlefilter ](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changearticle ](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_droparticle ](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
