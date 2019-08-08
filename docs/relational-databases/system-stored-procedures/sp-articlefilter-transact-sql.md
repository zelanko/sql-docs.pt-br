---
title: sp_articlefilter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_articlefilter_TSQL
- sp_articlefilter
helpviewer_keywords:
- sp_articlefilter
ms.assetid: 4c3fee32-a43f-4757-a029-30aef4696afb
author: stevestein
ms.author: sstein
ms.openlocfilehash: d90cd0ba957da820ce5a937ae687e39ca0302025
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769065"
---
# <a name="sp_articlefilter-transact-sql"></a>sp_articlefilter (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Filtra dados que são publicados com base em um artigo de tabela. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_articlefilter [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @filter_name = ] 'filter_name' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação que contém o artigo. a *publicação* é **sysname**, sem padrão.  
  
`[ @article = ] 'article'`É o nome do artigo. o *artigo* é **sysname**, sem padrão.  
  
`[ @filter_name = ] 'filter_name'`É o nome do procedimento armazenado de filtro a ser criado a partir de *filter_name*. *filter_name* é **nvarchar (386)** , com um padrão de NULL. Você deve especificar um nome exclusivo para o filtro de artigo.  
  
`[ @filter_clause = ] 'filter_clause'`É uma cláusula de restrição (WHERE) que define um filtro horizontal. Ao inserir a cláusula de restrição, omita a palavra-chave WHERE. *filter_clause* é **ntext**, com um padrão de NULL.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`O reconhece que a ação executada por esse procedimento armazenado pode invalidar um instantâneo existente. *force_invalidate_snapshot* é um **bit**, com um padrão de **0**.  
  
 **0** especifica que as alterações no artigo não fazem com que o instantâneo seja inválido. Se o procedimento armazenado detectar que a alteração requer um novo instantâneo, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** especifica que as alterações no artigo podem fazer com que o instantâneo seja inválido e, se houver assinaturas existentes que exijam um novo instantâneo, concederá permissão para o instantâneo existente ser marcado como obsoleto e um novo instantâneo gerado.  
  
`[ @force_reinit_subscription = ] force_reinit_subscription`Reconhece que a ação executada por este procedimento armazenado pode exigir que as assinaturas existentes sejam reinicializadas. *force_reinit_subscription* é um **bit**, com um padrão de **0**.  
  
 **0** especifica que as alterações no artigo não causam a reinicialização das assinaturas. Se o procedimento armazenado detectar que a alteração exigiria que as assinaturas fossem reinicializadas, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** especifica que as alterações no artigo fazem com que as assinaturas existentes sejam reinicializadas e concede a permissão para que a reinicialização da assinatura ocorra.  
  
`[ @publisher = ] 'publisher'`Especifica um não [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o Publicador é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  o Publicador não deve ser usado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com um Publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_articlefilter** é usado na replicação de instantâneo e na replicação transacional.  
  
 A execução de **sp_articlefilter** para um artigo com assinaturas existentes requer que essas assinaturas sejam reinicializadas.  
  
 **sp_articlefilter** cria o filtro, insere a ID do procedimento armazenado de filtro na coluna **filtro** da tabela [Transact- &#40;&#41; SQL sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md) e insere o texto da cláusula de restrição no **filtro coluna _clause** .  
  
 Para criar um artigo com um filtro horizontal, execute [sp_addarticle &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) sem nenhum parâmetro de *filtro* . Execute **sp_articlefilter**, fornecendo todos os parâmetros, incluindo *filter_clause*, e [Execute &#40;sp_articleview Transact-&#41;SQL](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md), fornecendo todos os parâmetros, incluindo *filter_clause*idênticos. Se o filtro já existir e se o **tipo** em **sysarticles** for **1** (artigo baseado em log), o filtro anterior será excluído e um novo filtro será criado.  
  
 Se *filter_name* e *filter_clause* não forem fornecidos, o filtro anterior será excluído e a ID do filtro será definida como **0**.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlefilter-transac_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou da função de banco de dados fixa **db_owner** podem executar **sp_articlefilter**.  
  
## <a name="see-also"></a>Consulte também  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Definir e modificar um filtro de linha estático](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articleview &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
