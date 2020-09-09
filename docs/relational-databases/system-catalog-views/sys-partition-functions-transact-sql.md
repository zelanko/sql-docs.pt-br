---
description: sys.partition_functions (Transact-SQL)
title: sys. partition_functions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.partition_functions_TSQL
- partition_functions
- sys.partition_functions
- partition_functions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.partition_functions catalog view
ms.assetid: 96515727-728b-4bea-804a-36ce915b8b75
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f0613fd963c527bcee8479cd0b8d16f70e7aa7fd
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537317"
---
# <a name="syspartition_functions-transact-sql"></a>sys.partition_functions (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Contém uma linha para cada função de partição no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome da função de partição. É exclusiva no banco de dados.|  
|**function_id**|**int**|ID da função de partição. É exclusiva no banco de dados.|  
|**tipo**|**char(2)**|Tipo de função.<br /><br /> R = Intervalo|  
|**type_desc**|**nvarchar(60)**|Tipo de função.<br /><br /> RANGE|  
|**fanout**|**int**|Número de partições criadas pela função.|  
|**boundary_value_on_right**|**bit**|Para particionamento de intervalo.<br /><br /> 1 = O valor de limite é incluído no intervalo à DIREITA do limite.<br /><br /> 0 = ESQUERDA.|  
|**is_system**||**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> 1 = O objeto é usado para fragmentos de índice de texto completo.<br /><br /> 0 = O objeto não é usado para fragmentos de índice de texto completo.|  
|**create_date**|**datetime**|Data em que a função foi criada.|  
|**modify_date**|**datetime**|Data em que a função foi modificada pela última vez por uma instrução ALTER.|  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** . Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de funções de partição &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.partition_range_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)   
 [sys.partition_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)  
  
  
