---
title: service_contracts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- service_contracts_TSQL
- sys.service_contracts_TSQL
- sys.service_contracts
- service_contracts
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_contracts catalog view
ms.assetid: 787dd47e-4210-439d-9c4a-57a727a0dbd8
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e58e0995d1aae2ce167a0ab0c5b5757c3a05612b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysservicecontracts-transact-sql"></a>sys.service_contracts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esta exibição do catálogo contém uma linha para cada contrato no banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do contrato, exclusivo no banco de dados. Não é NULLABLE.|  
|**service_contract_id**|**Int**|Identificador do contrato. Não é NULLABLE.|  
|**principal_id**|**Int**|Identificador para o principal de banco de dados que possui esse contrato. É NULLABLE.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
