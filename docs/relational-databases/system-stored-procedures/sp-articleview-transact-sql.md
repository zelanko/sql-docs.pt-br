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
ms.openlocfilehash: 7cc40187ccafebee672214a0926a3ca0d0bc4176
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768988"
---
# <a name="sp_articleview-transact-sql"></a>sp_articleview (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

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
`[ @publication = ] 'publication'`É o nome da publicação que contém o artigo. a *publicação* é **sysname**, sem padrão.  
  
`[ @article = ] 'article'`É o nome do artigo. o *artigo* é **sysname**, sem padrão.  
  
`[ @view_name = ] 'view_name'`É o nome da exibição que define o artigo publicado. *view_name* é **nvarchar (386)** , com um padrão de NULL.  
  
`[ @filter_clause = ] 'filter_clause'`É uma cláusula de restrição (WHERE) que define um filtro horizontal. Ao inserir a cláusula de restrição, omita a palavra-chave WHERE. *filter_clause* é **ntext**, com um padrão de NULL.  
  
`[ @change_active = ] change_active`Permite modificar as colunas em publicações que têm assinaturas. *change_active* é um **int**, com um padrão de **0**. Se **0**, as colunas não serão alteradas. Se **1**, as exibições poderão ser criadas ou recriadas em artigos ativos que tenham assinaturas.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`O reconhece que a ação executada por esse procedimento armazenado pode invalidar um instantâneo existente. *force_invalidate_snapshot* é um **bit**, com um padrão de **0**.  
  
 **0** especifica que as alterações no artigo não fazem com que o instantâneo seja inválido. Se o procedimento armazenado detectar que a alteração requer um novo instantâneo, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** especifica que as alterações no artigo podem fazer com que o instantâneo seja inválido e, se houver assinaturas existentes que exijam um novo instantâneo, concederá permissão para o instantâneo existente ser marcado como obsoleto e um novo instantâneo gerado.  
  
`[ @force_reinit_subscription = ] _force_reinit_subscription_`Reconhece que a ação executada por este procedimento armazenado pode exigir que as assinaturas existentes sejam reinicializadas. *force_reinit_subscription* é um **bit** com um padrão de **0**.  
  
 **0** especifica que as alterações no artigo não fazem com que a assinatura seja reinicializada. Se o procedimento armazenado detectar que a alteração exigiria que as assinaturas fossem reinicializadas, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** especifica que as alterações no artigo fazem com que a assinatura existente seja reinicializada e dá permissão para que a reinicialização da assinatura ocorra.  
  
`[ @publisher = ] 'publisher'`Especifica um não [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o Publicador é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  o Publicador não deve ser usado ao publicar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir de um Publicador.  
  
`[ @refreshsynctranprocs = ] refreshsynctranprocs`É se os procedimentos armazenados usados para sincronizar a replicação são recriados automaticamente. *refreshsynctranprocs* é **bit**, com um padrão de 1.  
  
 **1** significa que os procedimentos armazenados são recriados.  
  
 **0** significa que os procedimentos armazenados não são recriados.  
  
`[ @internal = ] internal` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_articleview** cria a exibição que define o artigo publicado e insere a ID dessa exibição na coluna **sync_objid** da tabela [sysarticles &#40;&#41; Transact-SQL](../../relational-databases/system-tables/sysarticles-transact-sql.md) e insere o texto da cláusula de restrição em a coluna **filter_clause** . Se todas as colunas forem replicadas e não houver nenhum **filter_clause**, o **sync_objid** na tabela [Transact-SQL&#41; sysarticles &#40;](../../relational-databases/system-tables/sysarticles-transact-sql.md) será definido como a ID da tabela base e o uso de **sp_articleview** não será necessário.  
  
 Para publicar uma tabela filtrada verticalmente (ou seja, para filtrar colunas), primeiro execute **sp_addarticle** sem nenhum parâmetro *sync_object* , execute [sp_articlecolumn &#40;Transact&#41; -SQL](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) uma vez para cada coluna a ser replicada (definindo o filtro vertical) e execute **sp_articleview** para criar a exibição que define o artigo publicado.  
  
 Para publicar uma tabela filtrada horizontalmente (ou seja, para filtrar linhas), [Execute &#40;sp_addarticle Transact-&#41; SQL](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) sem parâmetro de *filtro* . Execute [sp_articlefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md), fornecendo todos os parâmetros, incluindo *filter_clause*. Em seguida, execute **sp_articleview**, fornecendo todos os parâmetros, incluindo o *filter_clause*idêntico.  
  
 Para publicar uma tabela filtrada vertical e horizontalmente, execute [sp_addarticle &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) sem parâmetros *sync_object* ou *Filter* . Execute [sp_articlecolumn &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) uma vez para cada coluna a ser replicada e, em seguida, execute [ &#40;sp_articlefilter&#41; Transact-SQL](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) e **sp_articleview**.  
  
 Se o artigo já tiver uma exibição que define o artigo publicado, **sp_articleview** descartará a exibição existente e criará uma nova automaticamente. Se a exibição foi criada manualmente (**tipo** no [Transact &#40;-SQL&#41; sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md) é **5**), a exibição existente não será descartada.  
  
 Se você criar um procedimento armazenado de filtro personalizado e uma exibição que define o artigo publicado manualmente, não execute **sp_articleview**. Em vez disso, forneça isso como os parâmetros *Filter* e *sync_object* para [sp_addarticle &#40;Transact&#41;-SQL](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), juntamente com o valor de *tipo* apropriado.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articleview-transact-_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou da função de banco de dados fixa **db_owner** podem executar **sp_articleview**.  
  
## <a name="see-also"></a>Consulte também  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Definir e modificar um filtro de linha estático](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
