---
description: sys.assembly_types (Transact-SQL)
title: sys. assembly_types (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- assembly_types
- sys.assembly_types
- sys.assembly_types_TSQL
- assembly_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assembly_types catalog view
ms.assetid: 35f0384f-7a6d-41b1-9461-f1406d68f317
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 06eb2eb4fe6b0983b798ea38fa98057be73af77a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545054"
---
# <a name="sysassembly_types-transact-sql"></a>sys.assembly_types (Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  Contém uma linha para cada tipo definido pelo usuário que está definido por um assembly CLR. O **Sys. assembly_types** a seguir aparece na lista de colunas herdadas (consulte [sys. Types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)) depois de **rule_object_id**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|ID do assembly a partir do qual este tipo foi criado.|  
|**assembly_class**|**sysname**|Nome da classe no assembly que define este tipo.|  
|**is_binary_ordered**|**bit**|A classificação dos bytes deste tipo é equivalente à classificação com o uso de operadores de comparação no tipo.|  
|**is_fixed_length**|**bit**|O comprimento do tipo é sempre o mesmo que max_length.|  
|**prog_id**|**nvarchar(40)**|ProgID do tipo, como exposto para COM.|  
|**assembly_qualified_name**|**nvarchar(4000)**|Nome do tipo qualificado pelo assembly. O nome está em um formato adequado para ser passado para Type.GetType().|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo de tipos escalares &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)  
  
  
