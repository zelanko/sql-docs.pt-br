---
title: CREATE FULLTEXT STOPLIST (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STOPLIST_TSQL
- FULLTEXT STOPLIST
- STOPLIST
- FULLTEXT_STOPLIST_TSQL
- CREATE FULLTEXT STOPLIST
- CREATE_FULLTEXT_STOPLIST_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- stoplists [full-text search]
- CREATE FULLTEXT STOPLIST statement
- full-text search [SQL Server], stoplists
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 0669b1d0-46cc-4fac-8df7-5f7fa7af5db4
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f20341683bd9c22e5c133d0a4a52af2687641868
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="create-fulltext-stoplist-transact-sql"></a>CREATE FULLTEXT STOPLIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cria uma nova lista de palavras irrelevantes de texto completo no banco de dados atual.  
  
 As palavras irrelevantes são gerenciadas nos bancos de dados por meio de objetos chamados *listas de palavras irrelevantes* (stoplists). Uma lista de palavras irrelevantes é uma lista que, quando associada a um índice de texto completo, é aplicada às consultas de texto completo desse índice. Para obter mais informações, veja [Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes para pesquisa de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
> [!IMPORTANT]  
>  Somente há suporte para CREATE FULLTEXT STOPLIST, ALTER FULLTEXT STOPLIST e DROP FULLTEXT STOPLIST no nível de compatibilidade 100. Nos níveis de compatibilidade 80 e 90, essas instruções não têm suporte. No entanto, em todos os níveis de compatibilidade, a lista de palavras irrelevantes (stoplist) do sistema é associada automaticamente a novos índices de texto completo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE FULLTEXT STOPLIST stoplist_name  
[ FROM { [ database_name.]source_stoplist_name } | SYSTEM STOPLIST ]  
[ AUTHORIZATION owner_name ]  
;  
```  
  
## <a name="arguments"></a>Argumentos  
 *stoplist_name*  
 É o nome da lista de palavras irrelevantes. *stoplist_name* pode ter, no máximo, 128 caracteres. *stoplist_name* deve ser exclusivo entre todas as listas de palavras irrelevantes no banco de dados atual e estar em conformidade com as regras de identificadores.  
  
 *stoplist_name* será usado quando o índice de texto completo for criado.  
  
 *database_name*  
 É o nome do banco de dados em que a lista de palavras irrelevantes especificada por *source_stoplist_name* está localizada. Caso não seja especificado, *database_name* usará o banco de dados atual como padrão.  
  
 *source_stoplist_name*  
 Especifica que a nova lista de palavras irrelevantes é criada por meio de cópia de uma lista de palavras irrelevantes existente. Se o *source_stoplist_name* não existir ou se o usuário de banco de dados não tiver as permissões corretas, CREATE FULLTEXT STOPLIST falhará com um erro. Se qualquer idioma especificado nas palavras irrelevantes da lista de palavras irrelevantes de origem não estiver registrado no banco de dados atual, CREATE FULLTEXT STOPLIST terá êxito, mas serão retornados avisos e as palavras irrelevantes correspondentes não serão adicionadas.  
  
 SYSTEM STOPLIST  
 Especifica que a nova lista de palavras irrelevantes é criada com base na lista de palavras irrelevantes existente por padrão no [banco de dados Resource](../../relational-databases/databases/resource-database.md).  
  
 AUTHORIZATION *owner_name*  
 Especifica o nome de uma entidade do banco de dados que será a proprietária da lista de palavras irrelevantes. *owner_name* deve ser o nome de uma entidade da qual o usuário atual seja membro ou o usuário atual deve ter a permissão IMPERSONATE em *owner_name*. Se não estiver especificada, a propriedade será dada ao usuário atual.  
  
## <a name="remarks"></a>Remarks  
 O criador de uma lista de palavras irrelevantes é seu proprietário.  
  
## <a name="permissions"></a>Permissões  
 Para criar uma STOPLIST é necessário ter permissões CREATE FULLTEXT CATALOG. O proprietário da lista de palavras irrelevantes pode conceder a permissão CONTROL explicitamente em uma lista de palavras irrelevantes para permitir que os usuários adicionem e removam palavras e descartem a lista de palavras irrelevantes.  
  
> [!NOTE]  
>  O uso de uma lista de palavras irrelevantes com um índice de texto completo exige permissão REFERENCE.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-new-full-text-stoplist"></a>A. Criando uma nova lista de palavras irrelevantes de texto completo  
 O exemplo a seguir cria uma nova lista de palavras irrelevantes de texto completo denominada `myStoplist`.  
  
```  
CREATE FULLTEXT STOPLIST myStoplist;  
GO  
```  
  
### <a name="b-copying-a-full-text-stoplist-from-an-existing-full-text-stoplist"></a>B. Copiando uma lista de palavras irrelevantes de texto completo de uma lista de palavras irrelevantes de texto completo existente  
 O exemplo a seguir cria uma nova lista de palavras irrelevantes de texto completo denominada `myStoplist2` copiando uma lista de palavras irrelevantes do AdventureWorks existente denominada `Customers.otherStoplist`.  
  
```  
CREATE FULLTEXT STOPLIST myStoplist2 FROM AdventureWorks.otherStoplist;  
GO  
```  
  
### <a name="c-copying-a-full-text-stoplist-from-the-system-full-text-stoplist"></a>C. Copiando uma lista de palavras irrelevantes de texto completo da lista de palavras irrelevantes de texto completo do sistema  
 O exemplo a seguir cria uma nova lista de palavras irrelevantes de texto completo denominada `myStoplist3` copiando da lista de palavras irrelevantes do sistema.  
  
```  
CREATE FULLTEXT STOPLIST myStoplist3 FROM SYSTEM STOPLIST;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)   
 [DROP FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)   
 [Configurar e gerenciar palavras irrelevantes (stop words) e listas de palavras irrelevantes (stoplists) para a pesquisa de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)   
 [Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes para pesquisa de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
  
