---
title: server_event_notifications (Transact-SQL) | Microsoft Docs
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
- server_event_notifications
- sys.server_event_notifications
- sys.server_event_notifications_TSQL
- server_event_notifications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_notifications catalog view
ms.assetid: 1a83a044-3130-4551-95ca-162525846ff5
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7736946316131a6760d7bd9d9f2ab7b258b560ed
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33222117"
---
# <a name="sysservereventnotifications-transact-sql"></a>sys.server_event_notifications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada objeto de notificação de eventos no nível do servidor.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome da notificação de eventos do servidor. É exclusivo em todas as notificações de eventos no nível do servidor.|  
|**object_id**|**Int**|Número de identificação do objeto. É exclusivo dentro do **mestre** banco de dados.|  
|**parent_class**|**tinyint**|Classe do pai. Sempre é 100 = Servidor.|  
|**parent_class_desc**|**nvarchar(60)**|Descrição de classe do pai. Sempre é SERVER.|  
|**parent_id**|**Int**|Sempre é 0.|  
|**create_date**|**datetime**|Data de criação.|  
|**modify_date**|**datetime**|Data em que o objeto foi modificado pela última vez com o uso de uma instrução ALTER.|  
|**service_name**|**nvarchar(256)**|Nome do serviço de destino para o qual a notificação é enviada.|  
|**broker_instance**|**nvarchar(128)**|O agente de serviço no qual o serviço de destino nomeado está definido.|  
|**creator_sid**|**varbinary(85)**|SID do logon que está executando a instrução que cria a notificação de eventos. NULL se WITH FAN_IN não estiver especificado na definição de notificação de eventos.|  
|**principal_id**|**Int**|ID da entidade do servidor à qual isto pertence.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
