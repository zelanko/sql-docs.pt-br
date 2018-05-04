---
title: partition_parameters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- partition_parameters_TSQL
- partition_parameters
- sys.partition_parameters_TSQL
- sys.partition_parameters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.partition_parameters catalog view
ms.assetid: 2012ed9d-3ea3-4c29-9b78-dfa54a392dce
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d829b581083cdb434270a58aa276404050011882
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="syspartitionparameters-transact-sql"></a>sys.partition_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Contém uma linha para cada parâmetro de uma função de partição.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**function_id**|**Int**|ID da função de partição à qual o parâmetro pertence.|  
|**parameter_id**|**Int**|ID do parâmetro. É exclusiva dentro da função de partição, começando com 1.|  
|**system_type_id**|**tinyint**|ID do tipo de sistema do parâmetro. Corresponde ao **system_type_id** coluna o **Types** exibição do catálogo.|  
|**max_length**|**smallint**|Comprimento máximo do parâmetro em bytes.|  
|**precisão**|**tinyint**|Precisão do parâmetro se tiver base numérica; Caso contrário, 0.|  
|**scale**|**tinyint**|Escala do parâmetro, se numérico; do contrário, 0.|  
|**collation_name**|**sysname**|Nome do agrupamento do parâmetro, se for de caracteres; caso contrário, será NULL.|  
|**user_type_id**|**Int**|A ID do tipo É exclusiva no banco de dados. Para tipos de dados do sistema, **user_type_id** = **system_type_id**.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições do catálogo de função de partição &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.partition_functions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [sys.partition_range_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)  
  
  
