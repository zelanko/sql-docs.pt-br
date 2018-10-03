---
title: sp_articlecolumn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_articlecolumn
- sp_articlecolumn_TSQL
helpviewer_keywords:
- sp_articlecolumn
ms.assetid: 8abaa8c1-d99e-4788-970f-c4752246c577
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 72d9238e5b0f8ad5480e05ded3a0154eb5510904
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47640714"
---
# <a name="sparticlecolumn-transact-sql"></a>sp_articlecolumn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Usado para especificar colunas incluídas em um artigo para filtrar dados verticalmente em uma tabela publicada. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação que contém esse artigo. *publicação* está **sysname**, sem padrão.  
  
 [  **@article=**] **'***artigo***'**  
 É o nome do artigo. *artigo* está **sysname**, sem padrão.  
  
 [  **@column=**] **'***coluna***'**  
 É o nome da coluna a ser adicionada ou removida. *coluna* está **sysname**, com um padrão NULL. Se for NULL, todas as colunas serão publicadas.  
  
 [  **@operation=**] **'***operação***'**  
 Especifica se as colunas devem ser adicionadas ou removidas de um artigo. *operação* está **nvarchar (5)**, com um padrão de add. **Adicionar** marca a coluna para replicação. **Descartar** desmarca a coluna.  
  
 [  **@refresh_synctran_procs=**] *refresh_synctran_procs*  
 Especifica se os procedimentos armazenados com suporte para assinaturas de atualização imediata são gerados para corresponderem ao número de colunas replicadas. *refresh_synctran_procs* está **bit**, com um padrão de **1**. Se **1**, os procedimentos armazenados são gerados.  
  
 [  **@ignore_distributor =**] *ignore_distributor*  
 Indica se esse procedimento armazenado será executado sem conexão com o distribuidor. *ignore_distributor* está **bit**, com um padrão de **0**. Se **0**, o banco de dados deve ser habilitado para publicação e o cache de artigo deve ser atualizado para refletir as novas colunas replicadas por esse artigo. Se **1**, permite que colunas de artigos sejam descartadas para artigos que residem em um banco de dados não publicado; devem ser usados somente em situações de recuperação.  
  
 [  **@change_active =** ] *change_active*  
 Permite modificar as colunas em publicações que têm assinaturas. *change_active* é um **int** com um padrão de **0**. Se **0**, colunas não são modificadas. Se **1**, colunas podem ser adicionadas ou descartadas de artigos ativos que têm assinaturas.  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 Confirma que a ação tomada por esse procedimento armazenado pode invalidar um instantâneo existente. *force_invalidate_snapshot* é um **bit**, com um padrão de **0**.  
  
 **0** Especifica que as alterações no artigo fazem com que o instantâneo seja inválido. Se o procedimento armazenado detectar que a alteração requer um novo instantâneo, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** Especifica que as alterações no artigo podem invalidar o instantâneo ser inválida e se houver assinaturas existentes que exigem um novo instantâneo, dará permissão para o instantâneo existente seja marcado como obsoleto e um novo instantâneo seja gerado.  
  
 [ **@force_reinit_subscription =** ] *force_reinit_subscription*  
 Confirma que a ação tomada por esse procedimento armazenado pode exigir que as assinaturas existentes sejam reinicializadas. *force_reinit_subscription* é um **bit**, com um padrão de **0**.  
  
 **0** Especifica que as alterações no artigo fazem com que a assinatura seja reiniciada. Se o procedimento armazenado detectar que a alteração irá requerer assinaturas sejam reiniciadas, ocorrerá um erro e nenhuma alteração é feita. **1** Especifica que as alterações no artigo fazem com que as assinaturas existentes sejam reinicializadas e dá permissão para que ocorra a reinicialização da assinatura.  
  
 [  **@publisher=** ] **'***publisher***'**  
 Especifica um não[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador. *Publisher* está **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  *Publisher* não deve ser usado com um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
 [  **@internal=** ] **'***interno***'**  
 Somente para uso interno.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_articlecolumn** é usado em replicação de instantâneo e replicação transacional.  
  
 Apenas um artigo não assinado pode ser filtrado usando **sp_articlecolumn**.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlecolumn-transac_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_articlecolumn**.  
  
## <a name="see-also"></a>Consulte também  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Definir e modificar um filtro de coluna](../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)   
 [Filtrar os dados publicados](../../relational-databases/replication/publish/filter-published-data.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articleview &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
