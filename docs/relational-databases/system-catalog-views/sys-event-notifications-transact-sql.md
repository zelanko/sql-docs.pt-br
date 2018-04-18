---
title: event_notifications (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- event_notifications_TSQL
- event_notifications
- sys.event_notifications_TSQL
- sys.event_notifications
dev_langs:
- TSQL
helpviewer_keywords:
- sys.event_notifications catalog view
ms.assetid: 136a76ee-2b35-4418-ab46-fda2d51f7d99
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ebcff95c7cc4e36756985936cbdf4a6c8b927752
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="syseventnotifications-transact-sql"></a>sys.event_notifications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada objeto que é uma notificação de eventos, com **sys.objects.type** = EN.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome da notificação de eventos.|  
|**object_id**|**Int**|Número de identificação do objeto. É exclusivo em um banco de dados.|  
|**parent_class**|**tinyint**|Classe do pai.<br /><br /> 0 = Banco de dados<br /><br /> 1 = objeto ou coluna|  
|**parent_class_desc**|**nvarchar(60)**|DATABASE<br /><br /> OBJECT_OR_COLUMN|  
|**parent_id**|**Int**|ID diferente de zero do objeto pai.<br /><br /> 0 = A classe pai é o banco de dados.|  
|**create_date**|**datetime**|Data de criação.|  
|**modify_date**|**datetime**|Sempre é igual a **create_date**.|  
|**service_name**|**nvarchar(256)**|Nome do serviço de destino para o qual a notificação é enviada.|  
|**broker_instance**|**nvarchar(128)**|Instância de agente para a qual a notificação é enviada.|  
|**principal_id**|**Int**|ID da entidade de banco de dados que é o proprietário desta notificação de eventos.|  
|**creator_sid**|**varbinary(85)**|SID do logon que criou a notificação de eventos.<br /><br /> Será NULL se a opção FAN_IN não for especificada.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
