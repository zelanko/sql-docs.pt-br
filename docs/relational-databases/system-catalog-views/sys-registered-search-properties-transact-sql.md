---
title: sys. registered_search_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.registered_search_properties
- registered_search_properties
- sys.registered_search_properties_TSQL
- registered_search_properties_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search properties [SQL Server]
- property searching [SQL Server], viewing registered properties
- search property lists [SQL Server], viewing registered properties
- sys.registered_search_properties catalog view
ms.assetid: 1b9a7a5c-8c05-4819-83c3-7487dd08fcf7
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 09b95722f47442b2d5d749d8ba36888fb9605f58
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717616"
---
# <a name="sysregistered_search_properties-transact-sql"></a>sys.registered_search_properties (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Contém uma linha para cada propriedade de pesquisa contida por qualquer lista de propriedades de pesquisa no banco de dados atual.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**property_list_id**|**int**|ID da lista de propriedades de pesquisa à qual esta propriedade pertence.|  
|**property_set_guid**|**uniqueidentifier**|GUID (identificador global exclusivo) que identifica o conjunto de propriedades ao qual a propriedade de pesquisa pertence.|  
|**property_int_id**|**int**|Inteiro que identifica esta propriedade de pesquisa dentro do conjunto de propriedades. **property_int_id** é exclusivo dentro do conjunto de propriedades.|  
|**property_name**|**nvarchar (64)**|Nome que identifica exclusivamente esta propriedade de pesquisa na lista de propriedades de pesquisa.<br /><br /> Observação: para pesquisar em uma propriedade, especifique esse nome de propriedade no predicado [Contains](../../t-sql/queries/contains-transact-sql.md) .|  
|**property_description**|**nvarchar(512)**|Descrição da propriedade.|  
|**property_id**|**int**|A ID de propriedade interna da propriedade de pesquisa na lista de propriedades de pesquisa identificada pelo valor **property_list_id** .<br /><br /> Quando uma determinada propriedade é adicionada a uma determinada lista de propriedades de pesquisa, o Mecanismo de Texto Completo registra a propriedade e atribui uma ID de propriedade interna que é específica àquela lista de propriedades a propriedade. A ID de propriedade interna, que é um inteiro, é exclusiva de uma determinada lista de propriedades de pesquisa. Se uma determinada propriedade for registrada para várias listas de propriedades de pesquisa, uma ID de propriedade interna diferente poderá ser atribuída para cada lista de propriedades de pesquisa.<br /><br /> Observação: a ID de propriedade interna é distinta do identificador inteiro de propriedade que é especificado ao adicionar a propriedade à lista de propriedades de pesquisa. Para obter mais informações, veja [Pesquisar propriedades de documento com listas de propriedades de pesquisa](../../relational-databases/search/search-document-properties-with-search-property-lists.md).<br /><br /> Para exibir todo o conteúdo relacionado à propriedade no índice de texto completo: <br />                  [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre listas de propriedades de pesquisa, veja [Pesquisar propriedades de documento com listas de propriedades de pesquisa](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
## <a name="permissions"></a>Permissões  
 A visibilidade dos metadados de propriedades de pesquisa é limitada aos metadados que estão em listas de propriedades de pesquisa de sua propriedade ou nas quais você recebeu a permissão REFERENCE.  
  
> [!NOTE]  
>  O proprietário da lista de propriedades de pesquisa pode conceder as permissões REFERENCE ou CONTROL na lista. Usuários com permissão CONTROL também podem conceder a permissão REFERENCE a outros usuários.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir lista todos os metadados de propriedades de pesquisa registradas.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.registered_search_properties;   
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER FULLTEXT INDEX &#40;&#41;Transact-SQL](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [sys. fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)   
 [Pesquisar propriedades de documento com listas de propriedades de pesquisa](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  
