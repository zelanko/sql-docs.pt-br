---
title: remote_service_bindings (Transact-SQL) | Microsoft Docs
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
- sys.remote_service_bindings_TSQL
- remote_service_bindings_TSQL
- remote_service_bindings
- sys.remote_service_bindings
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_service_bindings catalog view
ms.assetid: 4e1a885d-eed1-4993-9c87-e6fd781f437d
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: b51b1ad09e3b1dd3252178e45934fafa46d4e688
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33181512"
---
# <a name="sysremoteservicebindings-transact-sql"></a>sys.remote_service_bindings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esta exibição do catálogo contém uma linha para cada associação de serviço remoto. 
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome desta associação de serviço remoto. Não é NULLABLE.|  
|**remote_service_binding_id**|**Int**|ID desta associação de serviço remoto. Não é NULLABLE.|  
|**principal_id**|**Int**|ID da entidade de banco de dados proprietária desta associação de serviço remoto. É NULLABLE.|  
|**remote_service_name**|**nvarchar(256)**|Nome do serviço remoto ao qual esta associação se aplica. É NULLABLE.|  
|**service_contract_id**|**Int**|ID do contrato ao qual esta associação se aplica. Um valor 0 é um curinga que indica que esta associação se aplica a todos os contratos para o serviço. Não é NULLABLE.|  
|**remote_principal_id**|**Int**|ID do usuário especificado na associação de serviço remoto. O Service Broker usa um certificado de propriedade deste usuário para comunicar-se com o serviço especificado nos contratos especificados. É NULLABLE.|  
|**is_anonymous_on**|**bit**|Esta associação de serviço remoto utiliza a segurança ANONYMOUS. A identidade do usuário que inicia a conversa não é fornecida ao serviço de destino. Não é NULLABLE.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
