---
title: trigger_events (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trigger_events_TSQL
- trigger_events
- sys.trigger_events
- sys.trigger_events_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trigger_events catalog view
ms.assetid: 92540447-131c-491c-b033-c064c7d950e1
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0071b7c0f955befba458a41ce813a8aff5aabe8c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47748934"
---
# <a name="systriggerevents-transact-sql"></a>sys.trigger_events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Contém uma linha por evento para a qual um gatilho é acionado.  
  
> [!NOTE]  
>  **trigger_events** não se aplica às notificações de eventos.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**\<Colunas herdadas de sys. Events >**|Não aplicável|Herda de **object_id**, **tipo**, **type_desc** colunas da [Events](../../relational-databases/system-catalog-views/sys-events-transact-sql.md).|  
|**is_first**|**bit**|O gatilho é marcado para ser o primeiro a ser acionado para este evento.|  
|**is_last**|**bit**|O gatilho é marcado para ser o último a ser acionado para este evento.|  
|**event_group_type**|**int**|Grupo de eventos no qual o gatilho é criado, ou NULL quando não é criado em um grupo de eventos.|  
|**event_group_type_desc**|**nvarchar(60)**|Descrição do grupo de eventos no qual o gatilho é criado, ou NULL quando não é criado em um grupo de eventos.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições do catálogo do objeto &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
