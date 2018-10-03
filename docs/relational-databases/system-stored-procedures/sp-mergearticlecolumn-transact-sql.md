---
title: sp_mergearticlecolumn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_mergearticlecolumn
- sp_mergearticlecolumn_TSQL
helpviewer_keywords:
- sp_mergearticlecolumn
ms.assetid: b4f2b888-e094-4759-a472-d893638995eb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 479ac5e7d9a1d451ea489a3a43c0ff481a6a121f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47837010"
---
# <a name="spmergearticlecolumn-transact-sql"></a>sp_mergearticlecolumn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Particiona uma publicação de mesclagem verticalmente. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@publication =**] **'***publicação***'**  
 É o nome da publicação. *publicação* está **sysname**, sem padrão.  
  
 [  **@article =**] **'***artigo***'**  
 É o nome do artigo na publicação. *artigo* está **sysname**, sem padrão.  
  
 [  **@column =**] **'***coluna***'**  
 Identifica as colunas nas quais criar a partição vertical. *coluna* está **sysname**, com um padrão NULL. Se NULL e `@operation = N'add'`, todas as colunas da tabela de origem serão adicionadas ao artigo por padrão. *coluna* não pode ser NULL quando *operação* é definido como **drop**. Para excluir colunas de um artigo, execute **sp_mergearticlecolumn** e especifique *coluna* e `@operation = N'drop'` para cada coluna a ser removido especificado *artigo*.  
  
 [  **@operation =**] **'***operação***'**  
 É o status da replicação. *operação* está **nvarchar(4)**, com um padrão de ADD. **Adicionar** marca a coluna para replicação. **Descartar** limpa a coluna.  
  
 [  **@schema_replication=**] **'***schema_replication***'**  
 Especifica que uma alteração no esquema será propagada quando Agente de Mesclagem for executado. *schema_replication* está **nvarchar (5)**, com um padrão de FALSE.  
  
> [!NOTE]  
>  Somente **falsos** tem suporte para *schema_replication*.  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 Habilita ou desabilita a capacidade de ter um instantâneo invalidado. *force_invalidate_snapshot* é um **bit**, com um padrão de **0**.  
  
 **0** Especifica que as alterações no artigo de mesclagem não fará com que o instantâneo seja inválido.  
  
 **1** Especifica que as alterações no artigo de mesclagem podem invalidar o instantâneo ser inválido, e se esse for o caso, um valor de **1** dá permissão para a ocorrência do novo instantâneo.  
  
 [* *@force_reinit_subscription =] * * * force_reinit_subscription*  
 Habilita ou desabilita a capacidade de fazer com que a assinatura seja reinicializada. *force_reinit_subscription* é um pouco com um padrão de **0**.  
  
 **0** Especifica que as alterações no artigo de mesclagem não fará com que a assinatura seja reiniciada.  
  
 **1** Especifica que as alterações no artigo de mesclagem podem invalidar a assinatura seja reiniciada e se esse for o caso, um valor de **1** dá permissão para que ocorra a reinicialização da assinatura.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_mergearticlecolumn** é usado em replicação de mesclagem.  
  
 Uma coluna de identidade não poderá ser descartada do artigo se o gerenciamento de intervalo de identidade automático estiver sendo usado. Para obter mais informações, consulte [Replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 Se um aplicativo definir uma nova partição vertical depois que o instantâneo inicial for criado, um novo instantâneo deverá ser gerado e reaplicado a casa assinatura. Instantâneos são aplicados quando o próximo agente de instantâneo, distribuição ou mesclagem agendado é executado.  
  
 Se o controle de linha for usado para detecção de conflitos (o padrão), a tabela de base poderá incluir no máximo 1.024 colunas, mas as colunas deverão ser filtradas do artigo de modo que seja publicado no máximo 246 colunas. Se o rastreamento de coluna for usado, a tabela base poderá incluir no máximo 246 colunas.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_AddMergeArticle](../../relational-databases/replication/codesnippet/tsql/sp-mergearticlecolumn-tr_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_mergearticlecolumn**.  
  
## <a name="see-also"></a>Consulte também  
 [Define and Modify a Join Filter Between Merge Articles](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Definir e modificar um filtro de linha com parâmetros para um artigo de mesclagem](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [Filtrar os dados publicados](../../relational-databases/replication/publish/filter-published-data.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
