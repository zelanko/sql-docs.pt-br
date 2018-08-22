---
title: sys.partition_range_values (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.partition_range_values
- partition_range_values_TSQL
- partition_range_values
- sys.partition_range_values_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.partition_range_values catalog view
ms.assetid: 9aee483e-61f3-4613-bec6-f084161f45ac
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: f7c5c646fd4cf5fd5f5f4e3220dc71ce725dfc23
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2018
ms.locfileid: "40394791"
---
# <a name="syspartitionrangevalues-transact-sql"></a>sys.partition_range_values (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contém uma linha para cada valor de limite de intervalo de uma função de partição do tipo R.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**function_id**|**int**|ID da função de partição para este valor de limite de intervalo.|  
|**boundary_id**|**int**|ID (de base 1 ordinal) da tupla de valor de limite, com limite mais à esquerda iniciando com um ID 1.|  
|**parameter_id**|**int**|ID do parâmetro da função à qual este valor corresponde. Os valores nesta coluna correspondem aos **parameter_id** coluna da **partition_parameters** exibição para qualquer determinado do catálogo **function_id**.|  
|**value**|**sql_variant**|O valor de limite real.|  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** . Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições do catálogo de função de partição &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.partition_functions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [sys. partition_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)  
  
  
