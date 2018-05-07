---
title: dbo.sysnotifications (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dbo.sysnotifications_TSQL
- sysnotifications
- sysnotifications_TSQL
- dbo.sysnotifications
dev_langs:
- TSQL
helpviewer_keywords:
- sysnotifications system table
ms.assetid: c5150d18-e8b7-48a7-ada7-77c583af6e41
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7683c41b4c10d1f96cd84d3a9c4377161a452595
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="dbosysnotifications-transact-sql"></a>dbo.sysnotifications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada notificação.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**alert_id**|**Int**|ID do alerta.|  
|**operator_id**|**Int**|ID do operador ao qual esta notificação deve ser enviada.|  
|**notification_method**|**tinyint**|Método de notificação:<br /><br /> **1** = email<br /><br /> **2** = pager<br /><br /> **4** = **netsend**<br /><br /> **7** = All|  
  
  
