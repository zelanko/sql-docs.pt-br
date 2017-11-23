---
title: sp_articleview (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_articleview
- sp_articleview_TSQL
helpviewer_keywords: sp_articleview
ms.assetid: a3d63fd6-f360-4a2f-8a82-a0dc15f650b3
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 165f494482aaac169eef7137bd0b45c0fa8b55d7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sparticleview-transact-sql"></a>sp_articleview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria a exibição que define o artigo publicado, quando uma tabela é filtrada verticalmente ou horizontalmente. Essa exibição é usada como a fonte filtrada de esquema e dados para as tabelas de destino. Somente artigos não assinados podem ser modificados por esse procedimento armazenado. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação que contém o artigo. *publicação* é **sysname**, sem padrão.  
  
 [  **@article=**] **'***artigo***'**  
 É o nome do artigo. *artigo* é **sysname**, sem padrão.  
  
 [  **@view_name=**] **'***view_name***'**  
 É o nome da exibição que define o artigo publicado. *view_name* é **nvarchar (386)**, com um padrão NULL.  
  
 [  **@filter_clause=**] **'***filter_clause***'**  
 É uma cláusula de restrição (WHERE) que define um filtro horizontal. Ao inserir a cláusula de restrição, omita a palavra-chave WHERE. *filter_clause* é **ntext**, com um padrão NULL.  
  
 [  **@change_active =** ] *change_active*  
 Permite modificar as colunas em publicações que têm assinaturas. *change_active* é um **int**, com um padrão de **0**. Se **0**, colunas não serão alteradas. Se **1**, modos de exibição podem ser criados ou recriados em artigos ativos que têm assinaturas.  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 Confirma que a ação tomada por esse procedimento armazenado pode invalidar um instantâneo existente. *force_invalidate_snapshot* é um **bit**, com um padrão de **0**.  
  
 **0** Especifica que as alterações no artigo fazem com que o instantâneo seja inválido. Se o procedimento armazenado detectar que a alteração requer um novo instantâneo, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** Especifica que as alterações no artigo podem invalidar o instantâneo inválido e se houver assinaturas existentes que exigem um novo instantâneo, dará permissão para que o instantâneo existente seja marcado como obsoleto e um novo instantâneo seja gerado.  
  
 [  **@force_reinit_subscription =]** *force_reinit_subscription*  
 Confirma que a ação tomada por esse procedimento armazenado pode exigir que as assinaturas existentes sejam reinicializadas. *force_reinit_subscription* é um **bit** com um padrão de **0**.  
  
 **0** Especifica que as alterações no artigo fazem com que a assinatura ser reiniciada. Se o procedimento armazenado detectar que a alteração irá requerer assinaturas sejam reiniciadas, ocorrerá um erro e nenhuma alteração é feita.  
  
 **1** Especifica que as alterações no artigo faz com que uma assinatura existente seja reiniciada e dá permissão para que ocorra a reinicialização da assinatura.  
  
 [  **@publisher** =] **'***publicador***'**  
 Especifica um não[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador. *publicador* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  *publicador* não deve ser usado durante a publicação de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
 [  **@refreshsynctranprocs**  =] *refreshsynctranprocs*  
 Especifica se os procedimentos armazenados usados para sincronizar replicações são recriados automaticamente. *refreshsynctranprocs* é **bit**, com um padrão de 1.  
  
 **1** significa que os procedimentos armazenados são recriados.  
  
 **0** significa que os procedimentos armazenados não são recriados.  
  
 [  **@internal** =] *interno*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_articleview** cria a exibição que define o artigo publicado e insere a ID dessa exibição no **sync_objid** coluna o [sysarticles &#40; Transact-SQL &#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) da tabela e insere o texto da cláusula de restrição de **filter_clause** coluna. Se todas as colunas são replicadas e não há nenhum **filter_clause**, o **sync_objid** no [sysarticles &#40; Transact-SQL &#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) tabela está definida como a ID da tabela base e o uso de **sp_articleview** não é necessária.  
  
 Para publicar uma tabela filtrada verticalmente (ou seja, para filtrar colunas) executado pela primeira vez **sp_addarticle** sem nenhum *sync_object* parâmetro, execute [sp_articlecolumn &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) uma vez para cada coluna a ser replicada (definindo o filtro vertical) e, em seguida, execute **sp_articleview** para criar o modo de exibição que define o artigo publicado.  
  
 Para publicar uma tabela horizontalmente filtrada (isto é, para filtrar linhas), execute [sp_addarticle &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) sem nenhum *filtro* parâmetro. Executar [sp_articlefilter &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md), fornecendo todos os parâmetros incluindo *filter_clause*. Em seguida, execute **sp_articleview**, fornecendo todos os parâmetros incluindo idênticas *filter_clause*.  
  
 Para publicar uma tabela filtrada verticalmente e horizontalmente, execute [sp_addarticle &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) sem nenhum *sync_object* ou *filtro* parâmetros. Executar [sp_articlecolumn &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) uma vez para cada coluna a ser replicada e, em seguida, execute [sp_articlefilter &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) e **sp_articleview**.  
  
 Se o artigo já tiver uma exibição que define o artigo publicado, **sp_articleview** descarta o modo de exibição existente e cria um novo automaticamente. Se a exibição foi criada manualmente (**tipo** na [sysarticles &#40; Transact-SQL &#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) é **5**), o modo de exibição existente não será removido.  
  
 Se você criar um procedimento armazenado de filtro personalizado e uma exibição que define o artigo publicado manualmente, não execute **sp_articleview**. Em vez disso, forneça esses como o *filtro* e *sync_object* parâmetros para [sp_addarticle &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), junto com as *tipo* valor.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articleview-transact-_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_articleview**.  
  
## <a name="see-also"></a>Consulte também  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Definir e modificar um filtro de linha estático](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [sp_addarticle &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
