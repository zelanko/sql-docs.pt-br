---
title: sp_addmergefilter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergefilter
- sp_addmergefilter_TSQL
helpviewer_keywords:
- sp_addmergefilter
ms.assetid: 4c118cb1-2008-44e2-a797-34b7dc34d6b1
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0ba0e2384ec63d29d3a5030c0b018998896dc8cb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68769176"
---
# <a name="sp_addmergefilter-transact-sql"></a>sp_addmergefilter (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Adiciona um novo filtro de mesclagem para criar uma partição com base em uma junção com outra tabela. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addmergefilter [ @publication = ] 'publication'   
        , [ @article = ] 'article'   
        , [ @filtername = ] 'filtername'   
        , [ @join_articlename = ] 'join_articlename'   
        , [ @join_filterclause = ] join_filterclause  
    [ , [ @join_unique_key = ] join_unique_key ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @filter_type = ] filter_type ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação na qual o filtro de mesclagem está sendo adicionado. a *publicação* é **sysname**, sem padrão.  
  
`[ @article = ] 'article'`É o nome do artigo no qual o filtro de mesclagem está sendo adicionado. o *artigo* é **sysname**, sem padrão.  
  
`[ @filtername = ] 'filtername'`É o nome do filtro. *FilterName* é um parâmetro obrigatório. *FilterName*é **sysname**, sem padrão.  
  
`[ @join_articlename = ] 'join_articlename'`É o artigo pai para o qual o artigo filho, especificado pelo *artigo*, deve ser Unido usando a cláusula de junção especificada por *join_filterclause*, a fim de determinar as linhas no artigo filho que atendem ao critério de filtro do filtro de mesclagem. *join_articlename* é **sysname**, sem padrão. O artigo deve estar na publicação fornecida pela *publicação*.  
  
`[ @join_filterclause = ] join_filterclause`É a cláusula de junção que deve ser usada para ingressar no artigo filho especificado pelo *artigo*e pelo artigo pai especificado por *join_article*, para determinar as linhas qualificando o filtro de mesclagem. *join_filterclause* é **nvarchar (1000)**.  
  
`[ @join_unique_key = ] join_unique_key`Especifica se a junção entre o artigo *do artigo filho e o*artigo pai *join_article*é um-para-muitos, um-para-um, muitos para um ou muitos para muitos. *join_unique_key* é **int**, com um padrão de 0. **0** indica uma junção muitos para um ou muitos para muitos. **1** indica uma junção um-para-um ou um-para-muitos. Esse valor é **1** quando as colunas de junção formam uma chave exclusiva em *join_article*, ou se *join_filterclause* estiver entre uma chave estrangeira no *artigo* e uma chave primária em *join_article*.  
  
> [!CAUTION]  
>  Somente defina esse parâmetro como **1** se você tiver uma restrição na coluna de junção na tabela subjacente para o artigo pai que garante a exclusividade. Se *join_unique_key* for definido como **1** incorretamente, pode ocorrer não convergência de dados.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`O reconhece que a ação executada por esse procedimento armazenado pode invalidar um instantâneo existente. *force_invalidate_snapshot* é um **bit**, com um padrão **0**.  
  
 **0** especifica que as alterações no artigo de mesclagem não farão com que o instantâneo seja inválido. Se o procedimento armazenado detectar que a alteração requer um novo instantâneo, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** especifica que as alterações no artigo de mesclagem podem fazer com que o instantâneo seja inválido e, se houver assinaturas existentes que exijam um novo instantâneo, concederá permissão para que o instantâneo existente seja marcado como obsoleto e um novo instantâneo gerado.  
  
`[ @force_reinit_subscription = ] force_reinit_subscription`Reconhece que a ação executada por este procedimento armazenado pode exigir que as assinaturas existentes sejam reinicializadas. *force_reinit_subscription* é um **bit**, com um padrão de 0.  
  
 **0** especifica que as alterações no artigo de mesclagem não farão com que a assinatura seja reinicializada. Se o procedimento armazenado detectar que a alteração irá requerer que as assinaturas existentes sejam reiniciadas, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** especifica que as alterações no artigo de mesclagem farão com que as assinaturas existentes sejam reinicializadas e concede a permissão para que a reinicialização da assinatura ocorra.  
  
`[ @filter_type = ] filter_type`Especifica o tipo de filtro que está sendo adicionado. *filter_type* é **tinyint**e pode ser um dos valores a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**1**|Somente filtro de junção. Necessário para dar [!INCLUDE[ssEW](../../includes/ssew-md.md)] suporte a assinantes.|  
|**2**|Somente relação de registro lógico.|  
|**Beta**|Relação de filtro de junção e registro lógico.|  
  
 Para obter mais informações, consulte [Agrupar alterações a linhas relacionadas com registros lógicos](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addmergefilter** é usado na replicação de mesclagem.  
  
 **sp_addmergefilter** só pode ser usada com artigos de tabela. Artigos de exibição e exibição indexada não têm suporte.  
  
 Esse procedimento também pode ser usado para adicionar uma relação lógica entre dois artigos que podem ou não ter um filtro de junção entre eles. *filter_type* é usado para especificar se o filtro de mesclagem que está sendo adicionado é um filtro de junção, uma relação lógica ou ambos.  
  
 Para usar registros lógicos, a publicação e os artigos devem atender a vários requisitos. Para obter mais informações, consulte [Agrupar alterações a linhas relacionadas com registros lógicos](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
 Geralmente, essa opção é usada para um artigo que tem uma referência de chave estrangeira para uma tabela de chave primária publicada, e, a tabela da chave primária tem um filtro definido nesse artigo. O subconjunto de linhas de chave primária é usado para determinar as linhas da chave estrangeira que são replicadas para o Assinante.  
  
 Você não pode adicionar um filtro de junção entre dois artigos publicados quando as tabelas de origem de ambos os artigos compartilham o mesmo nome de objeto de tabela. Nesse caso, mesmo que ambas as tabelas sejam de propriedade de esquemas diferentes e tenham nomes de artigo exclusivos, a criação do filtro de junção irá falhar.  
  
 Quando um filtro de linha e um filtro de junção com parâmetros são usados no mesmo artigo de tabela, a replicação determinará se uma linha pertence a uma partição de Assinante. Ele faz isso avaliando a função de filtragem ou o filtro de junção (usando o operador [or](../../t-sql/language-elements/or-transact-sql.md) ), em vez de avaliar a interseção entre as duas condições (usando o operador [and](../../t-sql/language-elements/and-transact-sql.md) ).  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_addmergefilter](../../relational-databases/replication/codesnippet/tsql/sp-addmergefilter-transa_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_addmergefilter**.  
  
## <a name="see-also"></a>Consulte Também  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Definir e modificar um filtro de junção entre artigos de mesclagem](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [&#41;&#40;Transact-SQL de sp_changemergefilter](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropmergefilter](../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpmergefilter](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
