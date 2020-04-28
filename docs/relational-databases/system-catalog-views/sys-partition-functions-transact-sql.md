---
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 410c52ff5a6e38e96db990713f8564c6463cfb80
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73981751"
---
# <a name="syspartition_functions-transact-sql"></a>sys.partition_functions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contém uma linha para cada função de partição no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome da função de partição. É exclusiva no banco de dados.|  
|**function_id**|**int**|ID da função de partição. É exclusiva no banco de dados.|  
|**type**|**char(2)**|Tipo de função.<br /><br /> R = Intervalo|  
|**type_desc**|**nvarchar(60)**|Tipo de função.<br /><br /> RANGE|  
|**fanout**|**int**|Número de partições criadas pela função.|  
|**boundary_value_on_right**|**bit**|Para particionamento de intervalo.<br /><br /> 1 = O valor de limite é incluído no intervalo à DIREITA do limite.<br /><br /> 0 = ESQUERDA.|  
|**is_system**||**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> 1 = O objeto é usado para fragmentos de índice de texto completo.<br /><br /> 0 = O objeto não é usado para fragmentos de índice de texto completo.|  
|**create_date**|**datetime**|Data em que a função foi criada.|  
|**modify_date**|**datetime**|Data em que a função foi modificada pela última vez por uma instrução ALTER.|  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de funções de partição &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys. partition_range_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)   
 [sys.partition_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)  
  
  
