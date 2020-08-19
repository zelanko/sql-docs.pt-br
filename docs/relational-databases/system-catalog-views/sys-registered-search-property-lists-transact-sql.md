---
description: sys.registered_search_property_lists (Transact-SQL)
title: sys. registered_search_property_lists (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- registered_search_property_lists_TSQL
- sys.registered_search_property_lists
- registered_search_property_lists
- sys.registered_search_property_lists_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- sys.registered_search_property_lists catalog view
- search property lists [SQL Server], viewing
ms.assetid: 630d4caa-9bea-4cd3-a5b1-01098b0855fc
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 9137345d642f1bc599ace1645cd5e441b927c4fd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447831"
---
# <a name="sysregistered_search_property_lists-transact-sql"></a>sys.registered_search_property_lists (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada lista de propriedades de pesquisa no banco de dados atual.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**property_list_id**|**int**|ID da lista de propriedades.|  
|**name**|**sysname**|O nome da lista de propriedades.|  
|**create_date**|**datetime**|A data em que a lista de propriedades foi criada.|  
|**modify_date**|**datetime**|A data da última modificação da lista de propriedades por uma instrução ALTER.|  
|**principal_id**|**int**|O proprietário da lista de propriedades.|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações, veja [Pesquisar propriedades de documento com listas de propriedades de pesquisa](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
## <a name="permissions"></a>Permissões  
 A visibilidade dos metadados nas listas de propriedades de pesquisa é limitada aos metadados que estão em listas de propriedades de pesquisa de sua propriedade ou nas quais você recebeu a permissão REFERENCE.  
  
> [!NOTE]  
>  O proprietário da lista de propriedades de pesquisa pode conceder as permissões REFERENCE ou CONTROL na lista. Usuários com permissão CONTROL também podem conceder a permissão REFERENCE a outros usuários.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir exibe a ID e o nome das listas de propriedades de pesquisa no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
SELECT property_list_id, name FROM sys.registered_search_property_lists;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)  
  
  
