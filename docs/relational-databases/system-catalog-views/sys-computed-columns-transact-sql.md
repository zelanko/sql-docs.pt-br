---
title: sys. computed_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.computed_columns_TSQL
- sys.computed_columns
- computed_columns_TSQL
- computed_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.computed_columns catalog view
ms.assetid: c962c619-e18f-4315-9251-8d9862462299
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9e55274d1e6dfa34a3cfb92317bb4f205cfdd964
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68109570"
---
# <a name="syscomputed_columns-transact-sql"></a>sys.computed_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contém uma linha para cada coluna encontrada em **Sys. Columns** que é uma coluna computada.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**\<Colunas herdadas>**||A exibição **Sys. computed_columns** retorna todas as colunas na exibição **Sys. Columns** . Ela também retorna as colunas adicionais descritas abaixo. Para obter uma descrição das colunas que a exibição **Sys. computed_columns** herda de **Sys. Columns**, consulte [Sys. columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md). O valor da coluna **IS_COMPUTED** é sempre definido como 1 na exibição **Sys. computed_columns** .|  
|**defini**|**nvarchar(max)**|Texto SQL que define essa coluna computada.|  
|**uses_database_collation**|**bit**|1 = A definição de coluna depende da ordenação padrão do banco de dados para a avaliação correta; caso contrário, será 0. Tal dependência impede a alteração da ordenação padrão do banco de dados.|  
|**is_persisted**|**bit**|A coluna computada é persistente.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objetos &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
