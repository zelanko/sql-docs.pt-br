---
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 44a5c374b585661421bfa22273eece46512eb2e4
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82823373"
---
# <a name="sysassembly_types-transact-sql"></a>sys.assembly_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

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
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo de tipos escalares &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)  
  
  
