---
title: masked_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/25/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.masked_columns
- masked_columns_tsql
- sys.masked_columns_tsql
- masked_columns
helpviewer_keywords:
- sys.masked_columns catalog view
ms.assetid: 671577e4-d757-4b8d-9aa9-0fc8d51ea9ca
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 432ea847081c8f0060954efdd6e7f2beea1a592d
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37998038"
---
# <a name="sysmaskedcolumns-transact-sql"></a>masked_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Use o **masked_columns** exibição para consultar colunas de tabela que têm uma função aplicada a eles de mascaramento de dados dinâmicos. Essa exibição herda valores da exibição **sys.columns** . Ela retorna todas as colunas na exibição **sys.columns** , mais as colunas **is_masked** e **masking_function** , indicando se a coluna é mascarada e, em caso positivo, qual função de mascaramento foi definida. Essa exibição só mostra colunas com uma função de máscara aplicada.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|ID do objeto ao qual esta coluna pertence.|  
|nome|**sysname**|Nome da coluna. É exclusiva no objeto.|  
|column_id|**int**|ID da coluna. É exclusiva no objeto.<br /><br /> Os IDs de coluna podem não ser sequenciais.|  
|**masked_columns** retorna muitas colunas mais herdadas de **sys. Columns**.|vários|Ver [Columns &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) para obter mais definições de coluna.|  
|is_masked|**bit**|Indica se a coluna é mascarada. 1 indica mascarado.|  
|masking_function|**nvarchar(4000)**|A função de mascaramento para a coluna.|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="permissions"></a>Permissões  
 Essa exibição retorna informações sobre tabelas em que o usuário tem algum tipo de permissão na tabela ou se o usuário tem a permissão VIEW ANY DEFINITION.  
  
## <a name="example"></a>Exemplo  
 A consulta a seguir junções **masked_columns** à **sys. Tables** retornar informações sobre todas as colunas de mascarado.  
  
```  
SELECT tbl.name as table_name, c.name AS column_name, c.is_masked, c.masking_function  
FROM sys.masked_columns AS c  
JOIN sys.tables AS tbl   
    ON c.object_id = tbl.object_id  
WHERE is_masked = 1;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Mascaramento de dados dinâmicos](../../relational-databases/security/dynamic-data-masking.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
