---
description: sys.parameter_type_usages (Transact-SQL)
title: sys. parameter_type_usages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.parameter_type_usages
- sys.parameter_type_usages_TSQL
- parameter_type_usages_TSQL
- parameter_type_usages
dev_langs:
- TSQL
helpviewer_keywords:
- sys.parameter_type_usages catalog view
ms.assetid: af0e167b-bffb-4525-84ec-3607f9268d3d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f20fbf0face7b4b99c7c2d5b5920139e68670052
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542497"
---
# <a name="sysparameter_type_usages-transact-sql"></a>sys.parameter_type_usages (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha para cada parâmetro que seja do tipo definido pelo usuário.  
  
> [!NOTE]  
>  Esta exibição não retorna linhas para parâmetros de procedimentos numerados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID do objeto ao qual pertence o parâmetro.|  
|**parameter_id**|**int**|ID do parâmetro. É exclusiva no objeto.|  
|**user_type_id**|**int**|ID do tipo definido pelo usuário.<br /><br /> Para retornar o nome do tipo, ingresse na exibição do catálogo [Sys. Types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) nesta coluna.|  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** . Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de tipos escalares &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
