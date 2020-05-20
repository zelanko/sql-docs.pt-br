---
title: sys. type_assembly_usages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.type_assembly_usages
- sys.type_assembly_usages_TSQL
- type_assembly_usages_TSQL
- type_assembly_usages
dev_langs:
- TSQL
helpviewer_keywords:
- sys.type_assembly_usages catalog view
ms.assetid: 79b8bf25-6e4e-4a07-ae93-7a4e44f65171
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d66d9e82c3d0b0d5d555e32fe4239decbe52e429
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833870"
---
# <a name="systype_assembly_usages-transact-sql"></a>sys.type_assembly_usages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha por tipo para referência de assembly.  
  

  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**user_type_id**|**int**|ID do tipo<br /><br /> Para retornar o nome do tipo, ingresse na exibição do catálogo [Sys. Types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) nesta coluna.|  
|**assembly_id**|**int**|ID do assembly|  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de tipos escalares &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
