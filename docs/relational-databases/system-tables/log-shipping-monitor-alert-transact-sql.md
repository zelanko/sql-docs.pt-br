---
description: log_shipping_monitor_alert (Transact-SQL)
title: log_shipping_monitor_alert (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_alert
- log_shipping_monitor_alert_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_alert system table
ms.assetid: 1c775e48-9898-4149-b9d1-04d465f23438
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5a171ba3bce8b7e657b99f71c16df6bfe33db4bc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460371"
---
# <a name="log_shipping_monitor_alert-transact-sql"></a>log_shipping_monitor_alert (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Armazena a identificação do trabalho de alerta para envio de logs. Essa tabela é armazenada no banco de dados **msdb** .   
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**alert_job_id**|**uniqueidentifier**|O agente de identificação do trabalho de alerta para envio de logs.do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [&#41;&#40;Transact-SQL de sp_add_log_shipping_alert_job ](../../relational-databases/system-stored-procedures/sp-add-log-shipping-alert-job-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_log_shipping_alert_job ](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-alert-job-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_log_shipping_alert_job ](../../relational-databases/system-stored-procedures/sp-help-log-shipping-alert-job-transact-sql.md)   
 [Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
