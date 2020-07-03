---
title: sp_articlecolumn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_articlecolumn
- sp_articlecolumn_TSQL
helpviewer_keywords:
- sp_articlecolumn
ms.assetid: 8abaa8c1-d99e-4788-970f-c4752246c577
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2948a0937983b9304f3d9167a5275c7d386145b8
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85874595"
---
# <a name="sp_articlecolumn-transact-sql"></a>sp_articlecolumn (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Usado para especificar colunas incluídas em um artigo para filtrar dados verticalmente em uma tabela publicada. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_articlecolumn [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @column = ] 'column' ]  
    [ , [ @operation = ] 'operation' ]  
    [ , [ @refresh_synctran_procs = ] refresh_synctran_procs ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @change_active = ] change_actve ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @internal = ] 'internal' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação que contém este artigo. a *publicação* é **sysname**, sem padrão.  
  
`[ @article = ] 'article'`É o nome do artigo. o *artigo* é **sysname**, sem padrão.  
  
`[ @column = ] 'column'`É o nome da coluna a ser adicionada ou removida. a *coluna* é **sysname**, com um padrão de NULL. Se for NULL, todas as colunas serão publicadas.  
  
`[ @operation = ] 'operation'`Especifica se as colunas devem ser adicionadas ou descartadas em um artigo. a *operação* é **nvarchar (5)**, com um padrão de adicionar. **Adicionar** marca a coluna para replicação. **drop** desmarca a coluna.  
  
`[ @refresh_synctran_procs = ] refresh_synctran_procs`Especifica se os procedimentos armazenados que dão suporte a assinaturas de atualização imediata são regenerados para corresponder ao número de colunas replicadas. *refresh_synctran_procs* é **bit**, com um padrão de **1**. Se for **1**, os procedimentos armazenados serão regenerados.  
  
`[ @ignore_distributor = ] ignore_distributor`Indica se este procedimento armazenado é executado sem conexão com o distribuidor. *ignore_distributor* é **bit**, com um padrão de **0**. Se **0**, o banco de dados deve ser habilitado para publicação e o cache do artigo deve ser atualizado para refletir as novas colunas replicadas pelo artigo. Se **1**, permite que as colunas do artigo sejam descartadas para artigos que residem em um banco de dados não publicado; deve ser usado somente em situações de recuperação.  
  
`[ @change_active = ] change_active`Permite modificar as colunas em publicações que têm assinaturas. *change_active* é um **int** com um padrão de **0**. Se **0**, as colunas não serão modificadas. Se **1**, as colunas podem ser adicionadas ou removidas de artigos ativos que têm assinaturas.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`O reconhece que a ação executada por esse procedimento armazenado pode invalidar um instantâneo existente. *force_invalidate_snapshot* é um **bit**, com um padrão de **0**.  
  
 **0** especifica que as alterações no artigo não fazem com que o instantâneo seja inválido. Se o procedimento armazenado detectar que a alteração requer um novo instantâneo, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** especifica que as alterações no artigo podem fazer com que o instantâneo seja inválido e, se houver assinaturas existentes que exijam um novo instantâneo, concederá permissão para o instantâneo existente ser marcado como obsoleto e um novo instantâneo gerado.  
  
 [** @force_reinit_subscription =** ] *force_reinit_subscription*  
 Confirma que a ação tomada por esse procedimento armazenado pode exigir que as assinaturas existentes sejam reinicializadas. *force_reinit_subscription* é um **bit**, com um padrão de **0**.  
  
 **0** especifica que as alterações no artigo não fazem com que a assinatura seja reinicializada. Se o procedimento armazenado detectar que a alteração exigiria que as assinaturas fossem reinicializadas, ocorrerá um erro e nenhuma alteração será feita. **1** especifica que as alterações no artigo fazem com que as assinaturas existentes sejam reinicializadas e concede a permissão para que a reinicialização da assinatura ocorra.  
  
`[ @publisher = ] 'publisher'`Especifica um não [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o *Publicador* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  o *Publicador* não deve ser usado com um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador.  
  
`[ @internal = ] 'internal'`Somente para uso interno.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_articlecolumn** é usado na replicação de instantâneo e na replicação transacional.  
  
 Apenas um artigo não assinado pode ser filtrado usando **sp_articlecolumn**.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlecolumn-transac_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_articlecolumn**.  
  
## <a name="see-also"></a>Consulte Também  
 [Definir um artigo](../../relational-databases/replication/publish/define-an-article.md)   
 [Definir e modificar um filtro de coluna](../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)   
 [Filtrar dados publicados](../../relational-databases/replication/publish/filter-published-data.md)   
 [&#41;&#40;Transact-SQL de sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changearticle](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_droparticle](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helparticle](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helparticlecolumns](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
