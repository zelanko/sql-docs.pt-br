---
description: sys.function_order_columns (Transact-SQL)
title: sys. function_order_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- function_order_columns
- sys.function_order_columns_TSQL
- function_order_columns_TSQL
- sys.function_order_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.function_order_columns catalog view
ms.assetid: 29287973-3125-4d35-8ca9-92cb45828854
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5c7ac555630f4472e5cf58ad9017cdb03643ae2b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546786"
---
# <a name="sysfunction_order_columns-transact-sql"></a>sys.function_order_columns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha por coluna que faz parte de uma expressão de **ordem** de uma função com valor de tabela de tempo de execução de linguagem Common (CLR).  

  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID do objeto (função CLR com valor de tabela) no qual a ordem é definida.|  
|**order_column_id**|**int**|ID da coluna de pedido. **order_column_id** só é exclusiva no **object_id**.<br /><br /> **order_column_id** representa a posição desta coluna na ordenação.|  
|**column_id**|**int**|ID da coluna em **object_id**.<br /><br /> **column_id** só é exclusiva no **object_id**.|  
|**is_descending**|**bit**|1 = coluna de ordem tem uma direção de classificação decrescente.<br /><br /> 0 = coluna de ordem tem uma direção de classificação crescente.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
