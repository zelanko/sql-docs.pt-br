---
title: sys.assembly_types (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- assembly_types
- sys.assembly_types
- sys.assembly_types_TSQL
- assembly_types_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.assembly_types catalog view
ms.assetid: 35f0384f-7a6d-41b1-9461-f1406d68f317
caps.latest.revision: "22"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 211cb9f89fe2e84b6a8a21dd8268551df6a2e97c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysassemblytypes-transact-sql"></a>sys.assembly_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Contém uma linha para cada tipo definido pelo usuário que está definido por um assembly CLR. O seguinte **sys.assembly_types** aparecem na lista de colunas herdadas (consulte [Types &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)) após **rule_object_id**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|ID do assembly a partir do qual este tipo foi criado.|  
|**assembly_class**|**sysname**|Nome da classe no assembly que define este tipo.|  
|**is_binary_ordered**|**bit**|A classificação dos bytes deste tipo é equivalente à classificação com o uso de operadores de comparação no tipo.|  
|**is_fixed_length**|**bit**|O comprimento do tipo é sempre o mesmo que max_length.|  
|**prog_id**|**nvarchar (40)**|ProgID do tipo, como exposto para COM.|  
|**assembly_qualified_name**|**nvarchar(4000)**|Nome do tipo qualificado pelo assembly. O nome está em um formato adequado para ser passado para Type.GetType().|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Escalar tipos de exibições de catálogo &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)  
  
  
