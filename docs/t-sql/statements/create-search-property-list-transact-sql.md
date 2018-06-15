---
title: CREATE SEARCH PROPERTY LIST (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE_SEARCH_PROPERTY_LIST_TSQL
- CREATE SEARCH
- CREATE_SEARCH_TSQL
- CREATE_SEARCH_PROPERTY_TSQL
- CREATE SEARCH PROPERTY
- CREATE SEARCH PROPERTY LIST
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search property lists [SQL Server], creating
- CREATE SEARCH PROPERTY LIST statement
ms.assetid: 5440cbb8-3403-4d27-a2f9-8e1f5a1bc12b
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: b22be6ddca31451698865c0e23a91ac23d4eb357
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33075673"
---
# <a name="create-search-property-list-transact-sql"></a>CREATE SEARCH PROPERTY LIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Cria uma nova lista de propriedades de pesquisa. Uma lista de propriedades de pesquisa é usada para especificar uma ou mais propriedades de pesquisa que você queira incluir em um índice de texto completo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
CREATE SEARCH PROPERTY LIST new_list_name  
   [ FROM [ database_name. ] source_list_name ]  
   [ AUTHORIZATION owner_name ]  
;  
```  
  
## <a name="arguments"></a>Argumentos  
 *new_list_name*  
 É o nome da nova lista de propriedades de pesquisa. *new_list_name* é um identificador com um máximo de 128 caracteres. *new_list_name* deve ser exclusivo entre todas as listas de propriedades no banco de dados atual e estar em conformidade com as regras de identificadores. *new_list_name* será usado quando o índice de texto completo for criado.  
  
 *database_name*  
 É o nome do banco de dados em que a lista de propriedades especificada por *source_list_name* está localizada. Caso não seja especificado, *database_name* usará o banco de dados atual como padrão.  
  
 *database_name* precisa especificar o nome de um banco de dados existente. O logon da conexão atual deve ser associado a uma ID de usuário existente no banco de dados especificado por *database_name*. Você também deve ter as [permissões](#Permissions) obrigatórias no banco de dados.  
  
 *source_list_name*  
 Especifica que a nova lista de propriedades é criada pela cópia de uma lista de propriedades existente do *database_name*. Se *source_list_name* não existir, CREATE SEARCH PROPERTY LIST falhará com um erro. As propriedades de pesquisa em *source_list_name* são herdadas por *new_list_name*.  
  
 AUTHORIZATION *owner_name*  
 Especifica o nome de um usuário ou uma função para ser o proprietário da lista de propriedades. *owner_name* precisa ser o nome de uma função da qual o usuário atual é membro ou o usuário atual precisa ter a permissão IMPERSONATE no *owner_name*. Se não estiver especificada, a propriedade será dada ao usuário atual.  
  
> [!NOTE]  
>  O proprietário pode ser alterado usando a instrução [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="remarks"></a>Remarks  
  
> [!NOTE]  
>  Para obter informações sobre listas de propriedades em geral, consulte [Pesquisar propriedades do documento com listas de propriedades de pesquisa](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
 Por padrão, uma nova lista de propriedades de pesquisa está vazia e você deve alterá-la para adicionar manualmente uma ou mais propriedades de pesquisa. Alternativamente, você pode copiar uma lista de propriedades de pesquisa existente. Nesse caso, a nova lista herda as propriedades de pesquisa de sua origem, mas você pode alterar a nova lista para adicionar ou remover propriedades de pesquisa. Qualquer propriedade na lista de propriedades de pesquisa no momento da próxima população completa será incluída no índice de texto completo.  
  
 Uma instrução CREATE SEARCH PROPERTY LIST falha sob qualquer uma destas condições:  
  
-   Se o banco de dados especificado por *database_name* não existe.  
  
-   Se a lista especificada por *source_list_name* não existe.  
  
-   Se você não tiver as permissões corretas.  
  
 **Para adicionar ou remover propriedades de uma lista**  
  
-   [ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md)  
  
-   **Para remover uma lista de propriedades**  
  
-   [DROP SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-search-property-list-transact-sql.md)  
  
##  <a name="Permissions"></a> Permissões  
 Requer permissões CREATE FULLTEXT CATALOG no banco de dados atual e permissões REFERENCES em qualquer banco de dados do qual você copiar uma lista de propriedades de origem.  
  
> [!NOTE]  
>  A permissão REFERENCES é necessária para associar a lista a um índice de texto completo. A permissão CONTROL é necessária para adicionar e remover propriedades ou remover a lista. O proprietário da lista de propriedades pode conceder as permissões REFERENCES ou CONTROL na lista. Usuários com permissão CONTROL também podem conceder a permissão REFERENCES a outros usuários.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-an-empty-property-list-and-associating-it-with-an-index"></a>A. Criando uma lista de propriedades vazia e associando-a a um índice  
 O exemplo a seguir cria uma nova lista de propriedades de pesquisa denominada `DocumentPropertyList`. Em seguida, o exemplo usa uma instrução [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) para associar a nova lista de propriedades ao índice de texto completo da tabela `Production.Document` no banco de dados `AdventureWorks`, sem iniciar uma população.  
  
> [!NOTE]  
>  Para obter um exemplo que adiciona várias propriedades de pesquisa predefinidas conhecidas a essa lista de propriedades de pesquisa, consulte [ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md). Depois de adicionar propriedades de pesquisa à lista, o administrador de banco de dados deverá usar outra instrução ALTER FULLTEXT INDEX com a cláusula START FULL POPULATION.  
  
```  
CREATE SEARCH PROPERTY LIST DocumentPropertyList;  
GO  
USE AdventureWorks2012;  
ALTER FULLTEXT INDEX ON Production.Document   
   SET SEARCH PROPERTY LIST DocumentPropertyList  
   WITH NO POPULATION;   
GO   
```  
  
### <a name="b-creating-a-property-list-from-an-existing-one"></a>B. Criando uma lista de propriedades com base em uma lista existente  
 O exemplo a seguir cria uma nova lista de propriedades de pesquisa, `JobCandidateProperties`, com base na lista criada pelo Exemplo A, `DocumentPropertyList`, que é associado a um índice de texto completo no banco de dados `AdventureWorks2012`. Em seguida, o exemplo utiliza uma instrução ALTER FULLTEXT INDEX para associar a nova lista de propriedades com o índice de texto completo da tabela `HumanResources.JobCandidate` no banco de dados `AdventureWorks2012`. Essa instrução ALTER FULLTEXT INDEX inicia uma população completa, que é o comportamento padrão da cláusula SET SEARCH PROPERTY LIST.  
  
```  
CREATE SEARCH PROPERTY LIST JobCandidateProperties 
FROM AdventureWorks2012.DocumentPropertyList;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate   
   SET SEARCH PROPERTY LIST JobCandidateProperties;  
GO  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md)   
 [DROP SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-search-property-list-transact-sql.md)   
 [sys.registered_search_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)   
 [Pesquisar propriedades de documento com listas de propriedades de pesquisa](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [Localizar GUIDs do conjunto de propriedades e IDs de inteiro de propriedade para propriedades de pesquisa](../../relational-databases/search/find-property-set-guids-and-property-integer-ids-for-search-properties.md)  
  
  
