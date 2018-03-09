---
title: partition_parameters (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ea75798552d0521204e063663566b08b36a5797b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="syspartitionparameters-transact-sql"></a>sys.partition_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Contém uma linha para cada parâmetro de uma função de partição.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**function_id**|**int**|ID da função de partição à qual o parâmetro pertence.|  
|**parameter_id**|**int**|ID do parâmetro. É exclusiva dentro da função de partição, começando com 1.|  
|**system_type_id**|**tinyint**|ID do tipo de sistema do parâmetro. Corresponde ao **system_type_id** coluna o **Types** exibição do catálogo.|  
|**max_length**|**smallint**|Comprimento máximo do parâmetro em bytes.|  
|**precisão**|**tinyint**|Precisão do parâmetro se tiver base numérica; Caso contrário, 0.|  
|**escala**|**tinyint**|Escala do parâmetro, se numérico; do contrário, 0.|  
|**collation_name**|**sysname**|Nome do agrupamento do parâmetro, se for de caracteres; caso contrário, será NULL.|  
|**user_type_id**|**int**|A ID do tipo É exclusiva no banco de dados. Para tipos de dados do sistema, **user_type_id** = **system_type_id**.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições do catálogo de função de partição &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [partition_functions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [sys.partition_range_values &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)  
  
  
