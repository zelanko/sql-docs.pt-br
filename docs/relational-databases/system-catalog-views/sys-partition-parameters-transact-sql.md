---
title: sys. partition_parameters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 32fe257f14c1e085a43b4150ee933888a83d5d14
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68125336"
---
# <a name="syspartition_parameters-transact-sql"></a>sys.partition_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contém uma linha para cada parâmetro de uma função de partição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**function_id**|**int**|ID da função de partição à qual o parâmetro pertence.|  
|**parameter_id**|**int**|ID do parâmetro. É exclusiva dentro da função de partição, começando com 1.|  
|**system_type_id**|**tinyint**|ID do tipo de sistema do parâmetro. Corresponde à coluna **system_type_id** da exibição do catálogo **Sys. Types** .|  
|**max_length**|**smallint**|Comprimento máximo do parâmetro em bytes.|  
|**precisão**|**tinyint**|Precisão do parâmetro se for baseado em numeric; caso contrário, 0.|  
|**scale**|**tinyint**|Escala do parâmetro, se numérico; do contrário, 0.|  
|**collation_name**|**sysname**|Nome da ordenação do parâmetro, se for de caracteres; caso contrário, será NULL.|  
|**user_type_id**|**int**|A ID do tipo É exclusiva no banco de dados. Para tipos de dados do sistema, **user_type_id** = **system_type_id**.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de funções de partição &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys. partition_functions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [sys.partition_range_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)  
  
  
