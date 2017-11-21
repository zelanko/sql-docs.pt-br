---
title: Cancelar a lista de propriedades de pesquisa (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_SEARCH_PROPERTY_LIST_TSQL
- DROP SEARCH PROPERTY LIST
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- DROP SEARCH PROPERTY LIST statement
- search property lists [SQL Server], dropping
- search property lists [SQL Server], deleting
ms.assetid: 7c7ce52a-6b77-4a1c-9abf-d5feb664bea8
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 970fd636239f6de212d667ef6ec22edfa182859c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="drop-search-property-list-transact-sql"></a>DROP SEARCH PROPERTY LIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Removerá uma lista de propriedades do banco de dados atual se a lista de propriedades de pesquisa não for associada atualmente com qualquer índice de texto completo no banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP SEARCH PROPERTY LIST property_list_name  
;  
```  
  
## <a name="arguments"></a>Argumentos  
 *property_list_name*  
 É o nome da lista de propriedades de pesquisa a ser removida. *property_list_name* é um identificador.  
  
 Para exibir os nomes das listas de propriedade existente, use o [registered_search_property_lists](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md) exibição do catálogo da seguinte maneira:  
  
```  
SELECT name FROM sys.registered_search_property_lists;  
```  
  
## <a name="remarks"></a>Comentários  
 Não é possível cancelar uma lista de propriedades de pesquisa de um banco de dados, enquanto a lista está associada a um índice de texto completo e as tentativas para fazer isso falham. Para remover uma lista de propriedades de pesquisa de um determinado índice de texto completo, use o [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) instrução e especifique a cláusula SET SEARCH PROPERTY LIST com off ou o nome de outra lista de propriedades de pesquisa.  
  
 **Para exibir a propriedade de lista em uma instância de servidor**  
  
-   [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
 **Para exibir a propriedade de lista associado com índices de texto completo**  
  
-   [sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)  
  
 **Para remover uma lista de propriedades de um índice de texto completo**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
##  <a name="Permissions"></a> Permissões  
 Requer a permissão CONTROL na lista de propriedades de pesquisa.  
  
> [!NOTE]  
>  O proprietário da lista de propriedades pode conceder permissões CONTROL à lista. Por padrão, o usuário que cria uma lista de propriedades de pesquisa é seu proprietário. O proprietário pode ser alterado usando o [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cancela a lista de propriedade `JobCandidateProperties` do banco de dados `AdventureWorks2012`.  
  
```  
DROP SEARCH PROPERTY LIST JobCandidateProperties;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER SEARCH PROPERTY LIST &#40; Transact-SQL &#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md)   
 [Criar lista de propriedades de pesquisa &#40; Transact-SQL &#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)   
 [Pesquisar propriedades de documento com listas de propriedades de pesquisa](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys. registered_search_properties &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)   
 [registered_search_property_lists &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
  

