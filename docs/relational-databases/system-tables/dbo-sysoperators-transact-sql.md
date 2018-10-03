---
title: dbo.sysoperators (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysoperators
- dbo.sysoperators
- dbo.sysoperators_TSQL
- sysoperators_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysoperators system table
ms.assetid: c2afa20c-b15f-46ca-ae74-2eb65909409e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3796714cbdfb55900447bf23904136ac5abefa9c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47678903"
---
# <a name="dbosysoperators-transact-sql"></a>dbo.sysoperators (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada operador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identificador de operador.|  
|**name**|**sysname**|Nome do operador.|  
|**habilitado**|**tinyint**|Estado de notificações alertas (Booliano). Se **1**, esse operador pode receber notificações quando ocorre um alerta.|  
|**email_address**|**nvarchar(100)**|Endereço de email deste operador.|  
|**last_email_date**|**int**|Data em que este operador recebeu a última notificação de alerta por e-mail.|  
|**last_email_time**|**int**|Hora do dia em que este operador recebeu a última notificação de alerta por e-mail.|  
|**pager_address**|**nvarchar(100)**|Endereço de pager deste operador.|  
|**last_pager_date**|**int**|Data em que este operador recebeu a última notificação de alerta pelo pager.|  
|**last_pager_time**|**int**|Hora do dia em que este operador recebeu a última notificação de alerta pelo pager.|  
|**weekday_pager_start_time**|**int**|Hora de um dia da semana (segunda a sexta-feira) a partir da qual este operador está disponível para receber notificações de alerta pelo pager.|  
|**weekday_pager_end_time**|**int**|Hora de um dia da semana (segunda a sexta-feira) a partir da qual este operador não está disponível para receber notificações de alerta pelo pager.|  
|**saturday_pager_start_time**|**int**|Hora do sábado a partir da qual este operador está disponível para receber uma notificação de alerta pelo pager.|  
|**saturday_pager_end_time**|**int**|Hora do sábado a partir da qual este operador não está disponível para receber uma notificação de alerta pelo pager.|  
|**sunday_pager_start_time**|**int**|Hora do domingo a partir da qual este operador está disponível para receber uma notificação de alerta pelo pager.|  
|**sunday_pager_end_time**|**int**|Hora do domingo a partir da qual este operador não está disponível para receber uma notificação de alerta pelo pager.|  
|**pager_days**|**tinyint**|Bitmask que representa os dias da semana nos quais este operador está disponível para receber uma notificação de alerta pelo pager.|  
|**netsend_address**|**nvarchar(100)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**last_netsend_date**|**int**|Data em que a última mensagem de rede foi enviada para o identificador de operador especificado.|  
|**last_netsend_time**|**int**|Hora em que a última mensagem de rede foi enviada para o identificador de operador especificado.|  
|**category_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas do SQL Server Agent &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
  
  
