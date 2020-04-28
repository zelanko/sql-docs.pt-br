---
title: sys. foreign_key_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.foreign_key_columns
- foreign_key_columns
- sys.foreign_key_columns_TSQL
- foreign_key_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.foreign_key_columns catalog view
ms.assetid: 7247f065-5441-4bcf-9f25-c84a03290dc6
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ad5bd8f5391e5903a6f9fd10e0cfb340cf4952b6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68133980"
---
# <a name="sysforeign_key_columns-transact-sql"></a>sys.foreign_key_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contém uma linha para cada coluna, ou conjunto de colunas, que inclui uma chave estrangeira.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**constraint_object_id**|**int**|ID da restrição FOREIGN KEY.|  
|**constraint_column_id**|**int**|ID da coluna ou conjunto de colunas, que compreende a chave estrangeira (*1.. n* em que n = número de colunas).|  
|**parent_object_id**|**int**|ID do pai da restrição, que é o objeto de referência.|  
|**parent_column_id**|**int**|ID da coluna pai, que é a coluna de referência.|  
|**referenced_object_id**|**int**|ID do objeto referenciado, que tem a chave candidata.|  
|**referenced_column_id**|**int**|ID da coluna referenciada (coluna da chave candidata).|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objetos &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
