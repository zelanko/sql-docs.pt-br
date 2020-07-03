---
title: sp_mergearticlecolumn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergearticlecolumn
- sp_mergearticlecolumn_TSQL
helpviewer_keywords:
- sp_mergearticlecolumn
ms.assetid: b4f2b888-e094-4759-a472-d893638995eb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ccc8cb8b4f9390d7453287c584e1f30dfdb15683
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899335"
---
# <a name="sp_mergearticlecolumn-transact-sql"></a>sp_mergearticlecolumn (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Particiona uma publicação de mesclagem verticalmente. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_mergearticlecolumn [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @column = ] 'column'  
    [ , [ @operation = ] 'operation'   
    [ , [ @schema_replication = ] 'schema_replication' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]   
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação. A *publicação* é **sysname**, sem padrão.  
  
`[ @article = ] 'article'`É o nome do artigo na publicação. o *artigo* é **sysname**, sem padrão.  
  
`[ @column = ] 'column'`Identifica as colunas nas quais criar a partição vertical. a *coluna* é **sysname**, com um padrão de NULL. Se NULL e `@operation = N'add'`, todas as colunas da tabela de origem serão adicionadas ao artigo por padrão. a *coluna* não pode ser nula quando a *operação* está definida como **drop**. Para excluir colunas de um artigo, execute **sp_mergearticlecolumn** e especifique a *coluna* e `@operation = N'drop'` para cada coluna a ser removida do *artigo*especificado.  
  
`[ @operation = ] 'operation'`É o status de replicação. a *operação* é **nvarchar (4)**, com um padrão de adicionar. **Adicionar** marca a coluna para replicação. **drop** limpa a coluna.  
  
`[ @schema_replication = ] 'schema_replication'`Especifica que uma alteração de esquema será propagada quando o Agente de Mesclagem for executado. *schema_replication* é **nvarchar (5)**, com um padrão de false.  
  
> [!NOTE]  
>  Só há suporte para **false** para *schema_replication*.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`Habilita ou desabilita a capacidade de um instantâneo ser invalidado. *force_invalidate_snapshot* é um **bit**, com um padrão de **0**.  
  
 **0** especifica que as alterações no artigo de mesclagem não farão com que o instantâneo seja inválido.  
  
 **1** especifica que as alterações no artigo de mesclagem podem fazer com que o instantâneo seja inválido e, se esse for o caso, um valor de **1** dá permissão para que o novo instantâneo ocorra.  
  
`[ @force_reinit_subscription = ]force_reinit_subscription_`Habilita ou desabilita a capacidade de reinitializated a assinatura. *force_reinit_subscription* é um bit com um padrão de **0**.  
  
 **0** especifica que as alterações no artigo de mesclagem não farão com que a assinatura seja reinicializada.  
  
 **1** especifica que as alterações no artigo de mesclagem podem fazer com que a assinatura seja reinicializada e, se esse for o caso, um valor **1** dá permissão para que a reinicialização da assinatura ocorra.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_mergearticlecolumn** é usado na replicação de mesclagem.  
  
 Uma coluna de identidade não poderá ser descartada do artigo se o gerenciamento de intervalo de identidade automático estiver sendo usado. Para obter mais informações, consulte [Replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 Se um aplicativo definir uma nova partição vertical depois que o instantâneo inicial for criado, um novo instantâneo deverá ser gerado e reaplicado a casa assinatura. Instantâneos são aplicados quando o próximo agente de instantâneo, distribuição ou mesclagem agendado é executado.  
  
 Se o controle de linha for usado para detecção de conflitos (o padrão), a tabela de base poderá incluir no máximo 1.024 colunas, mas as colunas deverão ser filtradas do artigo de modo que seja publicado no máximo 246 colunas. Se o rastreamento de coluna for usado, a tabela base poderá incluir no máximo 246 colunas.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_AddMergeArticle](../../relational-databases/replication/codesnippet/tsql/sp-mergearticlecolumn-tr_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_mergearticlecolumn**.  
  
## <a name="see-also"></a>Consulte Também  
 [Definir e modificar um filtro de junção entre artigos de mesclagem](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Definir e modificar um filtro de linha parametrizado para um artigo de mesclagem](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [Filtrar dados publicados](../../relational-databases/replication/publish/filter-published-data.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
