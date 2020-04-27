---
title: sys. remote_service_bindings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c326a5dd3a964209af0cc4834b91bca9071da9e2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67904578"
---
# <a name="sysremote_service_bindings-transact-sql"></a>sys.remote_service_bindings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esta exibição do catálogo contém uma linha para cada associação de serviço remoto. 
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome desta associação de serviço remoto. Não é NULLABLE.|  
|**remote_service_binding_id**|**int**|ID desta associação de serviço remoto. Não é NULLABLE.|  
|**principal_id**|**int**|ID da entidade de banco de dados proprietária desta associação de serviço remoto. É NULLABLE.|  
|**remote_service_name**|**nvarchar(256)**|Nome do serviço remoto ao qual esta associação se aplica. É NULLABLE.|  
|**service_contract_id**|**int**|ID do contrato ao qual esta associação se aplica. Um valor 0 é um curinga que indica que esta associação se aplica a todos os contratos para o serviço. Não é NULLABLE.|  
|**remote_principal_id**|**int**|ID do usuário especificado na associação de serviço remoto. O Service Broker usa um certificado de propriedade deste usuário para comunicar-se com o serviço especificado nos contratos especificados. É NULLABLE.|  
|**is_anonymous_on**|**bit**|Esta associação de serviço remoto utiliza a segurança ANONYMOUS. A identidade do usuário que inicia a conversa não é fornecida ao serviço de destino. Não é NULLABLE.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
