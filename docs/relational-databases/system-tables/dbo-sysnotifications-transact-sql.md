---
description: dbo.sysnotifications (Transact-SQL)
title: Notificações de dbo.sys(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8bcfd6b5b52a4f091337d55681be149ccd3f7900
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540342"
---
# <a name="dbosysnotifications-transact-sql"></a>dbo.sysnotifications (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada notificação.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|ID do alerta.|  
|**operator_id**|**int**|ID do operador ao qual esta notificação deve ser enviada.|  
|**notification_method**|**tinyint**|Método de notificação:<br /><br /> **1** = email<br /><br /> **2** = pager<br /><br /> **4**  =  **Netsend**<br /><br /> **7** = todos|  
  
  
